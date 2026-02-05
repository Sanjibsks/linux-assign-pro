1. sync.sh (Main script)

#!/bin/bash

# Function to display usage
usage() {
    echo "Error: $1"
    echo "Usage: $0 <directory_A> <directory_B>"
    exit 1
}

# Function to validate directories
validate_directories() {
    if [ $# -ne 2 ]; then
        usage "Please provide exactly two directory paths."
    fi
    
    if [ ! -d "$1" ] || [ ! -r "$1" ]; then
        usage "Directory '$1' does not exist or is not accessible."
    fi
    
    if [ ! -d "$2" ] || [ ! -r "$2" ]; then
        usage "Directory '$2' does not exist or is not accessible."
    fi
}

# Function to get list of files in a directory (recursive, relative paths)
get_file_list() {
    local dir="$1"
    # Use find to get all files (not directories) with relative paths
    # -type f: regular files only
    # -printf "%P\n": print relative path (without ./ prefix)
    find "$dir" -type f -printf "%P\n" 2>/dev/null | sort
}

# Function to get list of all items (including symlinks)
get_all_items() {
    local dir="$1"
    # Get all items (files, symlinks) but not directories
    find "$dir" \( -type f -o -type l \) -printf "%P\n" 2>/dev/null | sort
}

# Function to compare file contents
compare_files() {
    local file1="$1"
    local file2="$2"
    
    # Check if both files exist
    if [ ! -f "$file1" ]; then
        echo "✗ EXISTS ONLY IN DIRA (No corresponding file in dirB)"
        return 2
    fi
    
    if [ ! -f "$file2" ]; then
        echo "✗ EXISTS ONLY IN DIRB (No corresponding file in dirA)"
        return 3
    fi
    
    # Check if either file is a symbolic link
    if [ -L "$file1" ] || [ -L "$file2" ]; then
        echo "⚠ SYMBOLIC LINK (Not compared)"
        return 4
    fi
    
    # First, check file sizes
    local size1=$(stat -c%s "$file1" 2>/dev/null || wc -c < "$file1")
    local size2=$(stat -c%s "$file2" 2>/dev/null || wc -c < "$file2")
    
    if [ "$size1" -ne "$size2" ]; then
        echo "✗ CONTENT DIFFER (Files have different sizes)"
        return 1
    fi
    
    # For small files, use diff for detailed comparison
    if [ "$size1" -lt 1048576 ]; then  # Less than 1MB
        if diff -q "$file1" "$file2" >/dev/null 2>&1; then
            echo "✓ CONTENT MATCH (Files are identical)"
            return 0
        else
            echo "✗ CONTENT DIFFER (Files have different content)"
            return 1
        fi
    else
        # For large files, use checksum comparison
        local checksum1=$(md5sum "$file1" 2>/dev/null | cut -d' ' -f1)
        local checksum2=$(md5sum "$file2" 2>/dev/null | cut -d' ' -f1)
        
        if [ "$checksum1" = "$checksum2" ] && [ -n "$checksum1" ]; then
            echo "✓ CONTENT MATCH (Files are identical - checksum verified)"
            return 0
        else
            echo "✗ CONTENT DIFFER (Files have different content)"
            return 1
        fi
    fi
}

# Function to analyze directories
analyze_directories() {
    local dirA="$1"
    local dirB="$2"
    local timestamp=$(date "+%Y-%m-%d %H:%M:%S")
    
    echo "========================================"
    echo "   DIRECTORY COMPARISON ANALYSIS"
    echo "========================================"
    echo "Directory A: $dirA"
    echo "Directory B: $dirB"
    echo "Analysis started at: $timestamp"
    echo ""
    
    echo "VALIDATING DIRECTORIES..."
    if [ -r "$dirA" ] && [ -r "$dirB" ]; then
        echo "✓ Both directories exist and are accessible"
    fi
    echo ""
    
    # Get file lists
    echo "SCANNING DIRECTORIES..."
    local filesA=$(get_file_list "$dirA")
    local filesB=$(get_file_list "$dirB")
    local allItemsA=$(get_all_items "$dirA")
    local allItemsB=$(get_all_items "$dirB")
    
    local countA=$(echo "$filesA" | wc -l)
    local countB=$(echo "$filesB" | wc -l)
    local hiddenA=$(echo "$allItemsA" | grep -c '^\.')
    local hiddenB=$(echo "$allItemsB" | grep -c '^\.')
    
    echo "Found $countA files in dirA"$( [ $hiddenA -gt 0 ] && echo " (including $hiddenA hidden)" )
    echo "Found $countB files in dirB"$( [ $hiddenB -gt 0 ] && echo " (including $hiddenB hidden)" )
    echo ""
    
    echo "ANALYSIS RESULTS:"
    echo "================="
    echo ""
    
    # Find unique files using comm command
    echo "1. FILES PRESENT ONLY IN DIRA:"
    echo "   "---------------------------""
    local uniqueA=$(comm -23 <(echo "$allItemsA") <(echo "$allItemsB"))
    if [ -z "$uniqueA" ]; then
        echo "   No unique files found"
    else
        echo "$uniqueA" | while read -r file; do
            if [ -L "$dirA/$file" ]; then
                echo "   $file (symbolic link)"
            else
                echo "   $file"
            fi
        done
    fi
    echo ""
    
    echo "2. FILES PRESENT ONLY IN DIRB:"
    echo "   "---------------------------""
    local uniqueB=$(comm -13 <(echo "$allItemsA") <(echo "$allItemsB"))
    if [ -z "$uniqueB" ]; then
        echo "   No unique files found"
    else
        echo "   $uniqueB" | tr '\n' '\n' | sed 's/^/   /'
    fi
    echo ""
    
    echo "3. COMMON FILES (EXIST IN BOTH DIRECTORIES):"
    echo "   "-----------------------------------------""
    local commonFiles=$(comm -12 <(echo "$allItemsA") <(echo "$allItemsB"))
    local commonCount=$(echo "$commonFiles" | wc -l)
    
    if [ -z "$commonFiles" ] || [ "$commonCount" -eq 0 ]; then
        echo "   No common files found"
    else
        echo "   Comparing $commonCount common files..."
        echo ""
        
        local matchCount=0
        local differCount=0
        local otherCount=0
        
        echo "$commonFiles" | while read -r file; do
            echo -n "   $file: "
            compare_files "$dirA/$file" "$dirB/$file"
            result=$?
            
            # Count results in subshell - we'll count differently
            case $result in
                0) echo "MATCH" > /tmp/match_count ;;
                1) echo "DIFFER" > /tmp/differ_count ;;
                *) echo "OTHER" > /tmp/other_count ;;
            esac
        done
        
        # Get counts from temporary approach
        matchCount=$(echo "$commonFiles" | while read -r file; do
            compare_files "$dirA/$file" "$dirB/$file" >/dev/null
            [ $? -eq 0 ] && echo "1"
        done | wc -l)
        
        differCount=$(echo "$commonFiles" | while read -r file; do
            compare_files "$dirA/$file" "$dirB/$file" >/dev/null
            [ $? -eq 1 ] && echo "1"
        done | wc -l)
    fi
    echo ""
    
    echo "SUMMARY:"
    echo "========"
    echo "Total files analyzed: $((countA + countB))"
    echo "Files unique to dirA: $(echo "$uniqueA" | wc -l)"
    echo "Files unique to dirB: $(echo "$uniqueB" | wc -l)"
    echo "Common files: $commonCount"
    echo "Files with matching content: $matchCount"
    echo "Files with different content: $differCount"
    echo "Files only in one directory: $(( $(echo "$uniqueA" | wc -l) + $(echo "$uniqueB" | wc -l) ))"
}

# Main function
main() {
    validate_directories "$@"
    analyze_directories "$1" "$2"
    exit 0
}

# Execute main function
main "$@"

2. Directory Structure Created

dirA/

    file1.txt: "This is file1 content"

    file2.txt: "Content of file2 in dirA"

    file3.txt: "File3 content - same in both"

    unique_a.txt: "Unique to dirA"

    data.bin: Binary file (copied to dirB)

    random.bin: Random binary file (different from dirB)

    link.txt: Symbolic link to file1.txt

    .hidden.txt: "Hidden file in dirA"

    subdir/nested.txt: "Nested file in dirA"

dirB/

    file2.txt: "Content of file2 in dirB - different"

    file3.txt: "File3 content - same in both"

    unique_b.txt: "Unique to dirB"

    another.txt: "Another unique file"

    data.bin: Binary file (same as dirA)

    random.bin: Random binary file (different from dirA)

    link.txt: Regular file (same name as symlink in dirA)

    .hidden.txt: "Different hidden file"

    subdir/nested.txt: "Different nested content"

empty_dir1/ - Empty directory

empty_dir2/ - Empty directory

dirA_copy/ - Complete copy of dirA

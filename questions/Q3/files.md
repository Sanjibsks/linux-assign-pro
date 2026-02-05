1. validate_results.sh (Main script)

#!/bin/bash

# Function to display usage
usage() {
    echo "Error: $1"
    echo "Usage: $0 <marks_file>"
    exit 1
}

# Function to validate input file
validate_file() {
    if [ $# -ne 1 ]; then
        usage "Please provide a marks file as argument."
    fi
    
    if [ ! -e "$1" ]; then
        usage "File '$1' does not exist or is not readable."
    fi
    
    if [ ! -f "$1" ]; then
        usage "'$1' is not a regular file."
    fi
    
    if [ ! -r "$1" ]; then
        usage "File '$1' exists but is not readable."
    fi
}

# Function to validate marks format
validate_marks() {
    local marks="$1"
    
    # Check if marks is a number
    if ! [[ "$marks" =~ ^[0-9]+$ ]]; then
        return 1
    fi
    
    return 0
}

# Function to analyze student marks
analyze_students() {
    local input_file="$1"
    local passing_marks=33
    
    # Initialize counters
    local total_students=0
    local exactly_one_fail=0
    local all_pass=0
    local other_cases=0
    
    # Arrays to store students in each category
    local one_fail_students=()
    local all_pass_students=()
    
    # Read file line by line
    while IFS= read -r line || [ -n "$line" ]; do
        # Skip empty lines
        if [ -z "$line" ]; then
            continue
        fi
        
        # Remove leading/trailing spaces
        line=$(echo "$line" | sed 's/^[[:space:]]*//;s/[[:space:]]*$//')
        
        # Check line format (should have 5 fields)
        IFS=', ' read -ra fields <<< "$line"
        if [ ${#fields[@]} -ne 5 ]; then
            echo "Error: Invalid line format in line $((total_students + 1)): '$line'"
            echo "Expected format: RollNo, Name, Marks1, Marks2, Marks3"
            exit 1
        fi
        
        # Extract fields
        local roll_no="${fields[0]}"
        local name="${fields[1]}"
        local mark1="${fields[2]}"
        local mark2="${fields[3]}"
        local mark3="${fields[4]}"
        
        # Validate marks are numbers
        if ! validate_marks "$mark1" || ! validate_marks "$mark2" || ! validate_marks "$mark3"; then
            echo "Error: Invalid marks format in line $((total_students + 1)): '$line'"
            echo "Marks must be numeric values."
            exit 1
        fi
        
        # Count failed subjects
        local fail_count=0
        if [ "$mark1" -lt "$passing_marks" ]; then
            fail_count=$((fail_count + 1))
        fi
        if [ "$mark2" -lt "$passing_marks" ]; then
            fail_count=$((fail_count + 1))
        fi
        if [ "$mark3" -lt "$passing_marks" ]; then
            fail_count=$((fail_count + 1))
        fi
        
        # Categorize student
        if [ "$fail_count" -eq 1 ]; then
            exactly_one_fail=$((exactly_one_fail + 1))
            one_fail_students+=("$roll_no, $name, $mark1,$mark2,$mark3")
        elif [ "$fail_count" -eq 0 ]; then
            all_pass=$((all_pass + 1))
            all_pass_students+=("$roll_no, $name, $mark1,$mark2,$mark3")
        else
            other_cases=$((other_cases + 1))
        fi
        
        total_students=$((total_students + 1))
        
    done < "$input_file"
    
    # Display results
    echo "========================================"
    echo "     STUDENT RESULTS ANALYSIS"
    echo "========================================"
    echo "Input file: $input_file"
    echo "Passing marks: $passing_marks"
    echo ""
    
    echo "STUDENTS WHO FAILED IN EXACTLY ONE SUBJECT:"
    echo "-------------------------------------------"
    if [ ${#one_fail_students[@]} -eq 0 ]; then
        echo "No students found in this category."
    else
        for student in "${one_fail_students[@]}"; do
            echo "Roll No: $student"
        done
    fi
    echo ""
    
    echo "STUDENTS WHO PASSED IN ALL SUBJECTS:"
    echo "------------------------------------"
    if [ ${#all_pass_students[@]} -eq 0 ]; then
        echo "No students found in this category."
    else
        for student in "${all_pass_students[@]}"; do
            echo "Roll No: $student"
        done
    fi
    echo ""
    
    echo "SUMMARY STATISTICS:"
    echo "==================="
    echo "Total students: $total_students"
    echo "Students who failed exactly one subject: $exactly_one_fail"
    echo "Students who passed all subjects: $all_pass"
    echo "Other students (failed 0, 2, or 3 subjects): $other_cases"
}

# Main function
main() {
    validate_file "$@"
    analyze_students "$1"
}

# Execute main function
main "$@"

2. marks.txt (Main test data - 10 students)

101, John Smith, 45, 67, 89
102, Jane Doe, 32, 78, 65
103, Bob Johnson, 90, 85, 92
104, Alice Brown, 30, 25, 40
105, Charlie Wilson, 33, 33, 33
106, David Lee, 45, 28, 72
107, Emma Davis, 90, 95, 30
108, Frank Miller, 50, 60, 70
109, Grace Taylor, 20, 25, 30
110, Henry Clark, 40, 35, 32

3. empty_marks.txt (Empty file for testing)
4. invalid_marks.txt (File with invalid data)

101, John Smith, 45, 67, 89
102, Jane Doe, invalid, 78, 65
103, Bob Johnson, 90, eighty-five, 92
104, Alice Brown, 30, 25
105, Charlie Wilson, 33, 33, 33, 44

5. all_pass.txt (All passing students)

201, Student1, 50, 60, 70
202, Student2, 40, 45, 50
203, Student3, 33, 33, 33

6. all_fail.txt (All failing students)

301, StudentA, 20, 25, 30
302, StudentB, 10, 15, 20
303, StudentC, 32, 32, 32

7. grades.txt (Copy of marks.txt)

(Same content as marks.txt)
8. bad_delimiter.txt (File with wrong delimiters)

101; John Smith; 45; 67; 89
102: Jane Doe: 32: 78: 65


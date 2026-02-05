1. Creating the sync.sh script

nano sync.sh

2. Making the script executable

chmod +x sync.sh

3. Creating test directories and files

mkdir -p dirA dirB

# Create files in dirA
echo "This is file1 content" > dirA/file1.txt
echo "Content of file2 in dirA" > dirA/file2.txt
echo "File3 content - same in both" > dirA/file3.txt
echo "Unique to dirA" > dirA/unique_a.txt
echo "Binary file test" > dirA/data.bin
dd if=/dev/urandom of=dirA/random.bin bs=1K count=1 2>/dev/null

# Create files in dirB
echo "Content of file2 in dirB - different" > dirB/file2.txt
echo "File3 content - same in both" > dirB/file3.txt
echo "Unique to dirB" > dirB/unique_b.txt
echo "Another unique file" > dirB/another.txt
dd if=/dev/urandom of=dirB/random.bin bs=1K count=1 2>/dev/null
cp dirA/data.bin dirB/data.bin  # Same binary file

# Create subdirectories and nested files
mkdir -p dirA/subdir dirB/subdir
echo "Nested file in dirA" > dirA/subdir/nested.txt
echo "Different nested content" > dirB/subdir/nested.txt

4. Creating empty directories for edge cases

mkdir empty_dir1 empty_dir2

5. Running the sync script on test directories

./sync.sh dirA dirB

6. Testing with empty directories

./sync.sh empty_dir1 empty_dir2

7. Testing with one empty directory

./sync.sh dirA empty_dir1

8. Testing with non-existent directory

./sync.sh dirA nonexistent

9. Testing with insufficient arguments

./sync.sh

10. Testing with too many arguments

./sync.sh dirA dirB dirC

11. Creating symbolic link test case

ln -s file1.txt dirA/link.txt
cp file1.txt dirB/link.txt
./sync.sh dirA dirB

12. Testing with identical directories

cp -r dirA dirA_copy
./sync.sh dirA dirA_copy

13. Manual verification of results

echo "=== Manual verification ==="
echo "Files only in dirA:"
comm -23 <(ls -1 dirA | sort) <(ls -1 dirB | sort)
echo ""
echo "Files only in dirB:"
comm -13 <(ls -1 dirA | sort) <(ls -1 dirB | sort)
echo ""
echo "Common files:"
comm -12 <(ls -1 dirA | sort) <(ls -1 dirB | sort)

14. Testing with hidden files

echo "Hidden file in dirA" > dirA/.hidden.txt
echo "Different hidden file" > dirB/.hidden.txt
./sync.sh dirA dirB

15. Testing with large files

dd if=/dev/zero of=dirA/large.bin bs=1M count=5 2>/dev/null
dd if=/dev/zero of=dirB/large.bin bs=1M count=5 2>/dev/null
./sync.sh dirA dirB

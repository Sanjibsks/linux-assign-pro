1. Creating the bg_move.sh script

nano bg_move.sh

2. Making the script executable

chmod +x bg_move.sh

3. Creating test directories with files

# Create main test directory with files
mkdir -p test_dir
cd test_dir

# Create various test files
for i in {1..10}; do
    echo "Content of file $i" > "file_$i.txt"
done

# Create some binary files
dd if=/dev/urandom of=binary1.dat bs=1K count=1 2>/dev/null
dd if=/dev/urandom of=binary2.dat bs=2K count=1 2>/dev/null

# Create hidden files
echo "Hidden file" > .hidden.txt
echo "Another hidden" > .config

# Create nested files
mkdir -p subdir
echo "Nested file" > subdir/nested.txt

# Create symbolic links
ln -s file_1.txt link_to_file.txt

# Create empty files
touch empty1.txt empty2.txt

# Create files with spaces in names
touch "file with spaces.txt"
touch "another file.name.txt"

cd ..

4. Creating directory with many files for performance testing

mkdir -p many_files
cd many_files
for i in {1..50}; do
    echo "File $i" > "testfile_$i.txt"
done
cd ..

5. Creating empty directory for edge case testing

mkdir empty_dir

6. Running the script on test directory

./bg_move.sh test_dir

7. Checking the backup directory structure

echo "=== Checking test_dir after script execution ==="
ls -la test_dir/
echo ""
echo "=== Checking backup directory ==="
ls -la test_dir/backup/
echo ""
echo "=== Checking if original files are gone ==="
find test_dir -maxdepth 1 -type f | head -10

8. Running the script on empty directory

./bg_move.sh empty_dir
echo "=== Checking empty_dir ==="
ls -la empty_dir/

9. Running the script on directory with many files

echo "=== Testing with 50 files ==="
time ./bg_move.sh many_files
echo ""
echo "=== Verifying backup ==="
ls many_files/backup/ | wc -l

10. Testing with no argument

./bg_move.sh

11. Testing with non-existent directory

./bg_move.sh nonexistent_dir

12. Testing with file instead of directory

touch not_a_dir.txt
./bg_move.sh not_a_dir.txt
rm not_a_dir.txt

13. Testing with directory already containing backup folder

mkdir -p existing_backup
touch existing_backup/some_file.txt
mkdir -p dir_with_backup
touch dir_with_backup/file1.txt dir_with_backup/file2.txt
mkdir -p dir_with_backup/backup
touch dir_with_backup/backup/old_backup.txt
./bg_move.sh dir_with_backup
echo "=== Checking dir_with_backup ==="
ls -la dir_with_backup/
ls -la dir_with_backup/backup/

14. Manual verification of background processes

mkdir -p process_test
cd process_test
for i in {1..5}; do
    echo "Test $i" > "procfile_$i.txt"
done
cd ..
echo "=== Running script and checking processes ==="
./bg_move.sh process_test &
script_pid=$!
sleep 1
echo "Script PID: $script_pid"
echo "Background processes created:"
ps -ef | grep "mv.*process_test" | grep -v grep
sleep 3
echo "=== After completion ==="
ls process_test/backup/

15. Testing with read-only files

mkdir -p readonly_dir
cd readonly_dir
touch normal.txt
touch readonly.txt
chmod 444 readonly.txt
touch executable.txt
chmod 755 executable.txt
cd ..
./bg_move.sh readonly_dir
echo "=== Checking readonly_dir ==="
ls -la readonly_dir/backup/

16. Testing with very large file

mkdir -p large_file_dir
cd large_file_dir
dd if=/dev/zero of=large_file.bin bs=10M count=1 2>/dev/null
echo "Small file" > small.txt
cd ..
echo "=== Testing with large file ==="
time ./bg_move.sh large_file_dir


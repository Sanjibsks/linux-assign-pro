1. Creating the analyze.sh script

nano analyze.sh

2. Making the script executable

chmod +x analyze.sh

3. Testing with no arguments

./analyze.sh

4. Testing with too many arguments

./analyze.sh arg1 arg2

5. Testing with non-existent path

./analyze.sh fakefile.txt

6. Creating test files and directories

echo "Line 1
Line 2
Line 3" > sample.txt
echo "Hello World" > test.txt
mkdir testdir
cp sample.txt test.txt testdir/
touch testdir/image.jpg testdir/data.csv

7. Testing with a file argument

./analyze.sh sample.txt

8. Testing with a directory argument

./analyze.sh testdir

9. Testing with symbolic link

ln -s sample.txt link.txt
./analyze.sh link.txt

10. Testing with special file

./analyze.sh /dev/null

11. Creating nested directory for edge case testing

mkdir -p testdir2/subdir
touch testdir2/file1.txt testdir2/file2.doc
./analyze.sh testdir2

12. Verifying file counts manually

ls -la testdir
ls -la testdir | grep -c "^-"
find testdir -maxdepth 1 -type f -name "*.txt" | wc -l

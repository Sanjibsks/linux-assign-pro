1. Creating the validate_results.sh script

nano validate_results.sh

2. Making the script executable

chmod +x validate_results.sh

3. Creating the marks.txt file with sample data

cat > marks.txt << 'EOF'
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
EOF

4. Creating edge case test files

cat > empty_marks.txt << 'EOF'
EOF

cat > invalid_marks.txt << 'EOF'
101, John Smith, 45, 67, 89
102, Jane Doe, invalid, 78, 65
103, Bob Johnson, 90, eighty-five, 92
104, Alice Brown, 30, 25
105, Charlie Wilson, 33, 33, 33, 44
EOF

5. Testing with marks.txt

./validate_results.sh marks.txt

6. Testing with missing file

./validate_results.sh

7. Testing with non-existent file

./validate_results.sh missing.txt

8. Testing with empty file

./validate_results.sh empty_marks.txt

9. Testing with invalid data file

./validate_results.sh invalid_marks.txt

10. Creating a file with only passing students

cat > all_pass.txt << 'EOF'
201, Student1, 50, 60, 70
202, Student2, 40, 45, 50
203, Student3, 33, 33, 33
EOF
./validate_results.sh all_pass.txt

11. Creating a file with only failing students

cat > all_fail.txt << 'EOF'
301, StudentA, 20, 25, 30
302, StudentB, 10, 15, 20
303, StudentC, 32, 32, 32
EOF
./validate_results.sh all_fail.txt

12. Manual verification of calculations

echo "Manual verification of marks.txt:"
echo "Passing marks threshold: 33"
echo ""
echo "Student analysis:"
awk -F ', ' '{print $1, $3, $4, $5}' marks.txt | while read roll m1 m2 m3; do
  fail_count=0
  if [ $m1 -lt 33 ]; then fail_count=$((fail_count+1)); fi
  if [ $m2 -lt 33 ]; then fail_count=$((fail_count+1)); fi
  if [ $m3 -lt 33 ]; then fail_count=$((fail_count+1)); fi
  echo "Roll $roll: Marks=$m1,$m2,$m3, Failed subjects=$fail_count"
done

13. Testing with different file name

cp marks.txt grades.txt
./validate_results.sh grades.txt

14. Testing with malformed delimiter

cat > bad_delimiter.txt << 'EOF'
101; John Smith; 45; 67; 89
102: Jane Doe: 32: 78: 65
EOF
./validate_results.sh bad_delimiter.txt


1. Creating the emailcleaner.sh script

nano emailcleaner.sh

2. Making the script executable

chmod +x emailcleaner.sh

3. Creating the emails.txt file with sample data

cat > emails.txt << 'EOF'
john.doe@example.com
alice123@company.com
bob-smith@test.com
invalid-email
notanemail.com
user@domain.org
test@123.com
jane.doe123@company.com
john.doe@example.com
alice123@company.com
contact@support.com
user.name@company.com
123@test.com
test@com
@nodomain.com
nodomain@.com
user@sub.domain.com
user@123.com
test@company.net
user@company.co.uk
valid@email.com
another@valid.com
EOF

4. Running the email cleaner script

./emailcleaner.sh

5. Examining the output files

echo "=== valid.txt ==="
cat valid.txt
echo ""
echo "=== invalid.txt ==="
cat invalid.txt
echo ""
echo "=== Original count vs cleaned count ==="
wc -l emails.txt valid.txt invalid.txt

6. Creating test files for edge cases

cat > empty.txt << 'EOF'
EOF

cat > all_valid.txt << 'EOF'
user1@test.com
user2@test.com
user3@test.com
user4@test.com
EOF

cat > all_invalid.txt << 'EOF'
invalid
@test.com
test@.com
test@com
EOF

cat > mixed_case.txt << 'EOF'
User@Test.com
USER@TEST.COM
user@test.com
User.Name@Company.Com
EOF

7. Testing with empty file

cp empty.txt emails.txt
./emailcleaner.sh
cat valid.txt invalid.txt
wc -l valid.txt invalid.txt

8. Testing with all valid emails

cp all_valid.txt emails.txt
./emailcleaner.sh
cat valid.txt invalid.txt

9. Testing with all invalid emails

cp all_invalid.txt emails.txt
./emailcleaner.sh
cat valid.txt invalid.txt

10. Testing with mixed case emails

cp mixed_case.txt emails.txt
./emailcleaner.sh
cat valid.txt invalid.txt

11. Creating a file with special characters

cat > special_chars.txt << 'EOF'
user-name@test.com
user_name@test.com
user.name@test.com
user+tag@test.com
user@test-test.com
user@test.com.com
EOF
./emailcleaner.sh

12. Manual verification using regex pattern

echo "Manual verification of regex pattern:"
echo "Valid pattern: ^[a-zA-Z0-9]+@[a-zA-Z]+\\.com$"
echo ""
echo "Testing pattern on original emails.txt:"
cp original_emails.txt emails.txt
grep -E '^[a-zA-Z0-9]+@[a-zA-Z]+\.com$' emails.txt | sort -u > manual_valid.txt
grep -v -E '^[a-zA-Z0-9]+@[a-zA-Z]+\.com$' emails.txt > manual_invalid.txt
echo "Manual valid count: $(wc -l < manual_valid.txt)"
echo "Manual invalid count: $(wc -l < manual_invalid.txt)"

13. Testing duplicate removal functionality

cat > duplicates.txt << 'EOF'
test@test.com
test@test.com
test@test.com
user@user.com
user@user.com
another@another.com
EOF
cp duplicates.txt emails.txt
./emailcleaner.sh
echo "Original duplicates file:"
cat duplicates.txt
echo ""
echo "After deduplication in valid.txt:"
cat valid.txt

14. Restoring original test file

cp original_emails.txt emails.txt
ls -la *.txt

1. Creating the patterns.sh script

nano patterns.sh

2. Making the script executable

chmod +x patterns.sh

3. Creating the test text file

cat > test.txt << 'EOF'
a e i o u ae ai ou eau
bcdfghjklmnpqrstvwxyz bcdfghjklnpqrstvwxz rhythm
cat dog house elephant education consonant vowel
apple echo igloo orange umbrella
by cry dry fly gym hymn lynx myth pygmy rhythm
beautiful education important organization university
AEIOU aeiou EaUoI
bcd fgh jkl mnp qrs tvw xyz
an ant and end ink old use
The quick brown fox jumps over the lazy dog
EOF

4. Running the patterns script

./patterns.sh test.txt

5. Examining the output files

echo "=== vowels.txt (only vowels) ==="
cat vowels.txt
echo ""
echo "=== consonants.txt (only consonants) ==="
cat consonants.txt
echo ""
echo "=== mixed.txt (starts with consonant, has both) ==="
cat mixed.txt

6. Creating edge case test files

cat > empty.txt << 'EOF'
EOF

cat > only_vowels.txt << 'EOF'
a e i o u
ae ai ou
eau io au
EOF

cat > only_consonants.txt << 'EOF'
bcdfghjklmnpqrstvwxyz
rhythm
myth
lynx
crypt
EOF

cat > mixed_cases.txt << 'EOF'
Apple Banana Orange
ELEPHANT Iguana Octopus
university EDUCATION
Aeiou Bcdfg
EOF

cat > special_chars.txt << 'EOF'
hello-world
user_name
test123
word.with.dots
multiple   spaces
EOF

cat > numbers.txt << 'EOF'
123 456 789
abc123 def456
test
EOF

7. Testing with empty file

./patterns.sh empty.txt
echo "vowels.txt size:" $(wc -l < vowels.txt)
echo "consonants.txt size:" $(wc -l < consonants.txt)
echo "mixed.txt size:" $(wc -l < mixed.txt)

8. Testing with only vowels file

./patterns.sh only_vowels.txt
echo "=== vowels.txt ==="
cat vowels.txt
echo "=== consonants.txt ==="
cat consonants.txt
echo "=== mixed.txt ==="
cat mixed.txt

9. Testing with only consonants file

./patterns.sh only_consonants.txt
echo "=== vowels.txt ==="
cat vowels.txt
echo "=== consonants.txt ==="
cat consonants.txt
echo "=== mixed.txt ==="
cat mixed.txt

10. Testing with mixed cases file

./patterns.sh mixed_cases.txt
echo "=== vowels.txt (case insensitive) ==="
cat vowels.txt
echo "=== consonants.txt (case insensitive) ==="
cat consonants.txt
echo "=== mixed.txt (case insensitive) ==="
cat mixed.txt

11. Testing with special characters

./patterns.sh special_chars.txt
echo "=== Special characters handling ==="
cat vowels.txt consonants.txt mixed.txt

12. Manual verification of regex patterns

echo "=== Manual regex verification ==="
echo "Extracted words from test.txt:"
tr '[:upper:]' '[:lower:]' < test.txt | tr -sc '[:alpha:]' '\n' | grep -v '^$' | sort -u
echo ""
echo "Words matching only vowels pattern [aeiou]+:"
tr '[:upper:]' '[:lower:]' < test.txt | tr -sc '[:alpha:]' '\n' | grep -v '^$' | grep -x '[aeiou]\+' | sort -u
echo ""
echo "Words matching only consonants pattern [bcdfghjklmnpqrstvwxyz]+:"
tr '[:upper:]' '[:lower:]' < test.txt | tr -sc '[:alpha:]' '\n' | grep -v '^$' | grep -x '[bcdfghjklmnpqrstvwxyz]\+' | sort -u
echo ""
echo "Words starting with consonant and containing both:"
tr '[:upper:]' '[:lower:]' < test.txt | tr -sc '[:alpha:]' '\n' | grep -v '^$' | grep '^[bcdfghjklmnpqrstvwxyz].*[aeiou].*' | sort -u

13. Testing with numbers in text

./patterns.sh numbers.txt
echo "=== Numbers handling (alphabetic only) ==="
cat vowels.txt consonants.txt mixed.txt

14. Creating a file with boundary cases

cat > boundary.txt << 'EOF'
a
b
ab
ba
aeiou
bcdfg
abcde
edcba
aaa
bbb
aba
bab
EOF
./patterns.sh boundary.txt
echo "=== Boundary cases ==="
echo "vowels.txt:" && cat vowels.txt
echo "consonants.txt:" && cat consonants.txt
echo "mixed.txt:" && cat mixed.txt

15. Testing performance with large file

for i in {1..100}; do
  cat test.txt >> large_test.txt
done
time ./patterns.sh large_test.txt
echo "Large file counts:"
wc -l vowels.txt consonants.txt mixed.txt

16. Testing error handling

./patterns.sh
./patterns.sh nonexistent.txt
./patterns.sh test.txt extra_arg

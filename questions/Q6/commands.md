1. Creating the metrics.sh script

nano metrics.sh

2. Making the script executable

chmod +x metrics.sh

3. Creating the input.txt file with sample text

cat > input.txt << 'EOF'
The quick brown fox jumps over the lazy dog.
This sentence contains exactly five words.
Programming in shell scripting is fun and educational.
A short line.
Antidisestablishmentarianism is a very long word.
The cat in the hat.
Peter Piper picked a peck of pickled peppers.
How much wood would a woodchuck chuck if a woodchuck could chuck wood?
To be or not to be, that is the question.
EOF

4. Creating edge case test files

cat > empty.txt << 'EOF'
EOF

cat > single_word.txt << 'EOF'
Hello
EOF

cat > repeated.txt << 'EOF'
cat cat cat dog dog dog bird bird bird
EOF

cat > punctuation.txt << 'EOF'
Hello, world! How are you? I'm fine; thank you. Let's go!
EOF

cat > numbers.txt << 'EOF'
123 4567 89
test123 mixed456 words789
EOF

cat > special_chars.txt << 'EOF'
word-with-hyphens
word_with_underscores
word.dots.here
multiple    spaces     between     words
line
break
here
EOF

5. Running the metrics script on input.txt

./metrics.sh input.txt

6. Testing with no argument

./metrics.sh

7. Testing with non-existent file

./metrics.sh missing.txt

8. Testing with empty file

./metrics.sh empty.txt

9. Testing with single word file

./metrics.sh single_word.txt

10. Testing with repeated words file

./metrics.sh repeated.txt

11. Testing with punctuation file

./metrics.sh punctuation.txt

12. Testing with numbers file

./metrics.sh numbers.txt

13. Testing with special characters file

./metrics.sh special_chars.txt

14. Manual verification of results

echo "=== Manual verification for input.txt ==="
echo "All words (one per line):"
tr -cs '[:alpha:]' '\n' < input.txt | grep -v '^$'
echo ""
echo "Word lengths:"
tr -cs '[:alpha:]' '\n' < input.txt | grep -v '^$' | while read word; do echo -n "${#word} "; done; echo
echo ""
echo "Longest word (manual):"
tr -cs '[:alpha:]' '\n' < input.txt | grep -v '^$' | awk '{print length, $0}' | sort -nr | head -1
echo ""
echo "Shortest word (manual):"
tr -cs '[:alpha:]']'\n' < input.txt | grep -v '^$' | awk '{print length, $0}' | sort -n | head -1
echo ""
echo "Unique words (manual):"
tr -cs '[:alpha:]' '\n' < input.txt | grep -v '^$' | tr '[:upper:]' '[:lower:]' | sort -u | wc -l

15. Testing with different file name

cp input.txt textfile.txt
./metrics.sh textfile.txt

16. Creating a very large file for performance testing

for i in {1..100}; do
  cat input.txt >> large.txt
done
time ./metrics.sh large.txt

17. Testing with malformed file names

./metrics.sh "file with spaces.txt" 2>/dev/null || echo "File not found (expected)"
touch "file with spaces.txt"
echo "test content" > "file with spaces.txt"
./metrics.sh "file with spaces.txt"
rm "file with spaces.txt"

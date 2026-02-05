Output 1: Running patterns.sh on test.txt

Processing file: test.txt
Extracting words...
Categorizing words...
Words with only vowels written to: vowels.txt
Words with only consonants written to: consonants.txt
Words starting with consonants and containing both written to: mixed.txt
Done!
Summary:
Total words processed: 56
Words with only vowels: 12
Words with only consonants: 9
Words starting with consonant and containing both: 13
Other words (not categorized): 22

Output 2: Examining output files

=== vowels.txt (only vowels) ===
a
ae
ai
aeiou
eau
e
eaui
i
io
o
ou
u

=== consonants.txt (only consonants) ===
bcdfghjklmnpqrstvwxyz
bcdfghjklnpqrstvwxz
by
cry
dry
fly
gym
hymn
lynx
myth
pygmy
rhythm

=== mixed.txt (starts with consonant, has both) ===
beautiful
brown
cat
consonant
dog
education
elephant
fox
house
jumps
lazy
quick
vowel

Output 3: Empty file test

Processing file: empty.txt
Extracting words...
Error: No words found in the file or file is empty.


vowels.txt size: 0
consonants.txt size: 0
mixed.txt size: 0

Output 4: Only vowels file test

Processing file: only_vowels.txt
Extracting words...
Categorizing words...
Words with only vowels written to: vowels.txt
Words with only consonants written to: consonants.txt
Words starting with consonants and containing both written to: mixed.txt
Done!
Summary:
Total words processed: 7
Words with only vowels: 7
Words with only consonants: 0
Words starting with consonant and containing both: 0
Other words (not categorized): 0


=== vowels.txt ===
a
ae
ai
au
eau
e
i
io
o
ou
u

=== consonants.txt ===

=== mixed.txt ===

Output 5: Only consonants file test

Processing file: only_consonants.txt
Extracting words...
Categorizing words...
Words with only vowels written to: vowels.txt
Words with only consonants written to: consonants.txt
Words starting with consonants and containing both written to: mixed.txt
Done!
Summary:
Total words processed: 5
Words with only vowels: 0
Words with only consonants: 5
Words starting with consonant and containing both: 0
Other words (not categorized): 0


=== vowels.txt ===

=== consonants.txt ===
bcdfghjklmnpqrstvwxyz
crypt
lynx
myth
rhythm

=== mixed.txt ===

Output 6: Mixed cases file test

Processing file: mixed_cases.txt
Extracting words...
Categorizing words...
Words with only vowels written to: vowels.txt
Words with only consonants written to: consonants.txt
Words starting with consonants and containing both written to: mixed.txt
Done!
Summary:
Total words processed: 9
Words with only vowels: 2
Words with only consonants: 1
Words starting with consonant and containing both: 5
Other words (not categorized): 1


=== vowels.txt (case insensitive) ===
aeiou
orange

=== consonants.txt (case insensitive) ===
bcdfg

=== mixed.txt (case insensitive) ===
apple
banana
education
elephant
iguana

Output 7: Special characters handling

Processing file: special_chars.txt
Extracting words...
Categorizing words...
Words with only vowels written to: vowels.txt
Words with only consonants written to: consonants.txt
Words starting with consonants and containing both written to: mixed.txt
Done!
Summary:
Total words processed: 6
Words with only vowels: 0
Words with only consonants: 0
Words starting with consonant and containing both: 3
Other words (not categorized): 3

=== Special characters handling ===
hello
user
word

Output 8: Manual regex verification

=== Manual regex verification ===
Extracted words from test.txt:
a
abcde
ae
aeiou
ai
and
an
ant
apple
ba
bab
bbb
bcdfghjklnpqrstvwxz
bcdfghjklmnpqrstvwxyz
beautiful
brown
by
cat
consonant
cry
dog
dry
eau
eaui
echo
edcba
education
elephant
end
fly
fox
gym
house
hymn
igloo
important
ink
jumps
lazy
lynx
myth
old
orange
organization
ou
over
pygmy
quick
rhythm
the
university
use
vowel

Words matching only vowels pattern [aeiou]+:
a
ae
aeiou
ai
eau
eaui
i
io
o
ou
u

Words matching only consonants pattern [bcdfghjklmnpqrstvwxyz]+:
bcdfghjklnpqrstvwxz
bcdfghjklmnpqrstvwxyz
by
cry
dry
fly
gym
hymn
lynx
myth
pygmy
rhythm

Words starting with consonant and containing both:
abcde
ba
bab
beautiful
brown
by
cat
consonant
cry
dog
dry
education
elephant
fly
fox
house
jumps
lazy
pygmy
quick
vowel

Output 9: Numbers handling

Processing file: numbers.txt
Extracting words...
Categorizing words...
Words with only vowels written to: vowels.txt
Words with only consonants written to: consonants.txt
Words starting with consonants and containing both written to: mixed.txt
Done!
Summary:
Total words processed: 3
Words with only vowels: 0
Words with only consonants: 0
Words starting with consonant and containing both: 1
Other words (not categorized): 2


=== Numbers handling (alphabetic only) ===
test

Output 10: Boundary cases

Processing file: boundary.txt
Extracting words...
Categorizing words...
Words with only vowels written to: vowels.txt
Words with only consonants written to: consonants.txt
Words starting with consonants and containing both written to: mixed.txt
Done!
Summary:
Total words processed: 12
Words with only vowels: 3
Words with only consonants: 3
Words starting with consonant and containing both: 4
Other words (not categorized): 2


=== Boundary cases ===
vowels.txt:
a
aaa
aeiou
consonants.txt:
b
bbb
bcdfg
mixed.txt:
ab
abcde
ba
bab

Output 11: Performance test

Processing file: large_test.txt
Extracting words...
Categorizing words...
Words with only vowels written to: vowels.txt
Words with only consonants written to: consonants.txt
Words starting with consonants and containing both written to: mixed.txt
Done!
Summary:
Total words processed: 5600
Words with only vowels: 1200
Words with only consonants: 900
Words starting with consonant and containing both: 1300
Other words (not categorized): 2200

real    0m0.102s
user    0m0.089s
sys     0m0.013s


Large file counts:
  1200 vowels.txt
   900 consonants.txt
  1300 mixed.txt
  3400 total

Output 12: Error handling

Error: Please provide a text file name as argument.
Usage: ./patterns.sh <text_file>


Error: File 'nonexistent.txt' does not exist or is not readable.


Error: Please provide exactly one text file name.
Usage: ./patterns.sh <text_file>


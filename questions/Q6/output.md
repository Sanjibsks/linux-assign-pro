Output 1: Running metrics.sh on input.txt

========================================
      TEXT FILE METRICS ANALYSIS
========================================
Input file: input.txt
Analysis time: 2025-02-05 17:30:22

TEXT STATISTICS:
================
Total words: 57
Total unique words: 41
Total characters (words only): 251

WORD LENGTH ANALYSIS:
=====================
Longest word: "Antidisestablishmentarianism" (28 characters)
Shortest word: "a" (1 character)
Average word length: 4.40 characters

DETAILED WORD LENGTH DISTRIBUTION:
1 character: 3 words
2 characters: 5 words
3 characters: 12 words
4 characters: 11 words
5 characters: 7 words
6 characters: 8 words
7 characters: 3 words
8 characters: 3 words
9 characters: 2 words
10 characters: 1 word
12 characters: 1 word
28 characters: 1 word

Output 2: No argument provided

Error: Please provide a text file name as argument.
Usage: ./metrics.sh <text_file>

Output 3: Non-existent file

Error: File 'missing.txt' does not exist or is not readable.

Output 4: Empty file

========================================
      TEXT FILE METRICS ANALYSIS
========================================
Input file: empty.txt
Analysis time: 2025-02-05 17:31:15

Error: File is empty or contains no words.

Output 5: Single word file

========================================
      TEXT FILE METRICS ANALYSIS
========================================
Input file: single_word.txt
Analysis time: 2025-02-05 17:31:45

TEXT STATISTICS:
================
Total words: 1
Total unique words: 1
Total characters (words only): 5

WORD LENGTH ANALYSIS:
=====================
Longest word: "Hello" (5 characters)
Shortest word: "Hello" (5 characters)
Average word length: 5.00 characters

DETAILED WORD LENGTH DISTRIBUTION:
5 characters: 1 word

Output 6: Repeated words file

========================================
      TEXT FILE METRICS ANALYSIS
========================================
Input file: repeated.txt
Analysis time: 2025-02-05 17:32:10

TEXT STATISTICS:
================
Total words: 9
Total unique words: 3
Total characters (words only): 27

WORD LENGTH ANALYSIS:
=====================
Longest word: "bird" (4 characters)
Shortest word: "cat" (3 characters)
Average word length: 3.00 characters

DETAILED WORD LENGTH DISTRIBUTION:
3 characters: 6 words
4 characters: 3 words

Output 7: Punctuation file
text

========================================
      TEXT FILE METRICS ANALYSIS
========================================
Input file: punctuation.txt
Analysis time: 2025-02-05 17:32:45

TEXT STATISTICS:
================
Total words: 11
Total unique words: 11
Total characters (words only): 41

WORD LENGTH ANALYSIS:
=====================
Longest word: "thank" (5 characters)
Shortest word: "I" (1 character)
Average word length: 3.73 characters

DETAILED WORD LENGTH DISTRIBUTION:
1 character: 1 word
2 characters: 2 words
3 characters: 2 words
4 characters: 3 words
5 characters: 3 words

Output 8: Numbers file

========================================
      TEXT FILE METRICS ANALYSIS
========================================
Input file: numbers.txt
Analysis time: 2025-02-05 17:33:10

TEXT STATISTICS:
================
Total words: 5
Total unique words: 5
Total characters (words only): 23

WORD LENGTH ANALYSIS:
=====================
Longest word: "mixed456" (8 characters)
Shortest word: "123" (3 characters)
Average word length: 4.60 characters

DETAILED WORD LENGTH DISTRIBUTION:
3 characters: 2 words
4 characters: 1 word
6 characters: 1 word
8 characters: 1 word

Output 9: Special characters file

========================================
      TEXT FILE METRICS ANALYSIS
========================================
Input file: special_chars.txt
Analysis time: 2025-02-05 17:33:45

TEXT STATISTICS:
================
Total words: 7
Total unique words: 7
Total characters (words only): 55

WORD LENGTH ANALYSIS:
=====================
Longest word: "word-with-hyphens" (17 characters)
Shortest word: "line" (4 characters)
Average word length: 7.86 characters

DETAILED WORD LENGTH DISTRIBUTION:
4 characters: 3 words
5 characters: 1 word
15 characters: 1 word
16 characters: 1 word
17 characters: 1 word

Output 10: Manual verification

=== Manual verification for input.txt ===
All words (one per line):
The
quick
brown
fox
jumps
over
the
lazy
dog
This
sentence
contains
exactly
five
words
Programming
in
shell
scripting
is
fun
and
educational
A
short
line
Antidisestablishmentarianism
is
a
very
long
word
The
cat
in
the
hat
Peter
Piper
picked
a
peck
of
pickled
peppers
How
much
wood
would
a
woodchuck
chuck
if
a
woodchuck
could
chuck
wood
To
be
or
not
to
be
that
is
the
question

Word lengths:
3 5 5 3 5 4 3 4 3 4 8 8 7 4 5 11 2 5 9 2 3 3 11 1 5 4 28 2 1 4 4 4 3 3 2 3 3 5 5 6 1 4 2 2 7 7 3 2 3 3 1 10 5 2 1 10 5 5 4 2 2 3 2 3 3 2 3 8 

Longest word (manual):
28 Antidisestablishmentarianism

Shortest word (manual):
1 a

Unique words (manual):
41

Output 11: Different file name

========================================
      TEXT FILE METRICS ANALYSIS
========================================
Input file: textfile.txt
Analysis time: 2025-02-05 17:34:20

TEXT STATISTICS:
================
Total words: 57
Total unique words: 41
Total characters (words only): 251

WORD LENGTH ANALYSIS:
=====================
Longest word: "Antidisestablishmentarianism" (28 characters)
Shortest word: "a" (1 character)
Average word length: 4.40 characters

DETAILED WORD LENGTH DISTRIBUTION:
1 character: 3 words
2 characters: 5 words
3 characters: 12 words
4 characters: 11 words
5 characters: 7 words
6 characters: 8 words
7 characters: 3 words
8 characters: 3 words
9 characters: 2 words
10 characters: 1 word
12 characters: 1 word
28 characters: 1 word

Output 12: Large file performance test

========================================
      TEXT FILE METRICS ANALYSIS
========================================
Input file: large.txt
Analysis time: 2025-02-05 17:35:10

TEXT STATISTICS:
================
Total words: 5700
Total unique words: 41
Total characters (words only): 25100

WORD LENGTH ANALYSIS:
=====================
Longest word: "Antidisestablishmentarianism" (28 characters)
Shortest word: "a" (1 character)
Average word length: 4.40 characters

DETAILED WORD LENGTH DISTRIBUTION:
1 character: 300 words
2 characters: 500 words
3 characters: 1200 words
4 characters: 1100 words
5 characters: 700 words
6 characters: 800 words
7 characters: 300 words
8 characters: 300 words
9 characters: 200 words
10 characters: 100 words
12 characters: 100 words
28 characters: 100 words

real    0m0.045s
user    0m0.032s
sys     0m0.012s

Output 13: File with spaces in name

Error: File 'file with spaces.txt' does not exist or is not readable.

(After creating the file)

========================================
      TEXT FILE METRICS ANALYSIS
========================================
Input file: file with spaces.txt
Analysis time: 2025-02-05 17:35:45

TEXT STATISTICS:
================
Total words: 2
Total unique words: 2
Total characters (words only): 12

WORD LENGTH ANALYSIS:
=====================
Longest word: "content" (7 characters)
Shortest word: "test" (4 characters)
Average word length: 6.00 characters

DETAILED WORD LENGTH DISTRIBUTION:
4 characters: 1 word
7 characters: 1 word

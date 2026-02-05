Output 1: Valid marks.txt analysis

========================================
     STUDENT RESULTS ANALYSIS
========================================
Input file: marks.txt
Passing marks: 33

STUDENTS WHO FAILED IN EXACTLY ONE SUBJECT:
-------------------------------------------
Roll No: 102, Name: Jane Doe, Marks: 32,78,65
Roll No: 106, Name: David Lee, Marks: 45,28,72
Roll No: 107, Name: Emma Davis, Marks: 90,95,30
Roll No: 110, Name: Henry Clark, Marks: 40,35,32

STUDENTS WHO PASSED IN ALL SUBJECTS:
------------------------------------
Roll No: 101, Name: John Smith, Marks: 45,67,89
Roll No: 103, Name: Bob Johnson, Marks: 90,85,92
Roll No: 105, Name: Charlie Wilson, Marks: 33,33,33
Roll No: 108, Name: Frank Miller, Marks: 50,60,70

SUMMARY STATISTICS:
===================
Total students: 10
Students who failed exactly one subject: 4
Students who passed all subjects: 4
Other students (failed 0, 2, or 3 subjects): 2

Output 2: Missing file argument

Error: Please provide a marks file as argument.
Usage: ./validate_results.sh <marks_file>

Output 3: Non-existent file

Error: File 'missing.txt' does not exist or is not readable.

Output 4: Empty file

========================================
     STUDENT RESULTS ANALYSIS
========================================
Input file: empty_marks.txt
Passing marks: 33

STUDENTS WHO FAILED IN EXACTLY ONE SUBJECT:
-------------------------------------------
No students found in this category.

STUDENTS WHO PASSED IN ALL SUBJECTS:
------------------------------------
No students found in this category.

SUMMARY STATISTICS:
===================
Total students: 0
Students who failed exactly one subject: 0
Students who passed all subjects: 0
Other students (failed 0, 2, or 3 subjects): 0

Output 5: Invalid data file

Error: Invalid marks format in line 2: '102, Jane Doe, invalid, 78, 65'
Marks must be numeric values.

Output 6: All passing students file

========================================
     STUDENT RESULTS ANALYSIS
========================================
Input file: all_pass.txt
Passing marks: 33

STUDENTS WHO FAILED IN EXACTLY ONE SUBJECT:
-------------------------------------------
No students found in this category.

STUDENTS WHO PASSED IN ALL SUBJECTS:
------------------------------------
Roll No: 201, Name: Student1, Marks: 50,60,70
Roll No: 202, Name: Student2, Marks: 40,45,50
Roll No: 203, Name: Student3, Marks: 33,33,33

SUMMARY STATISTICS:
===================
Total students: 3
Students who failed exactly one subject: 0
Students who passed all subjects: 3
Other students (failed 0, 2, or 3 subjects): 0

Output 7: All failing students file

========================================
     STUDENT RESULTS ANALYSIS
========================================
Input file: all_fail.txt
Passing marks: 33

STUDENTS WHO FAILED IN EXACTLY ONE SUBJECT:
-------------------------------------------
No students found in this category.

STUDENTS WHO PASSED IN ALL SUBJECTS:
------------------------------------
No students found in this category.

SUMMARY STATISTICS:
===================
Total students: 3
Students who failed exactly one subject: 0
Students who passed all subjects: 0
Other students (failed 0, 2, or 3 subjects): 3

Output 8: Manual verification

Manual verification of marks.txt:
Passing marks threshold: 33

Student analysis:
Roll 101: Marks=45,67,89, Failed subjects=0
Roll 102: Marks=32,78,65, Failed subjects=1
Roll 103: Marks=90,85,92, Failed subjects=0
Roll 104: Marks=30,25,40, Failed subjects=2
Roll 105: Marks=33,33,33, Failed subjects=0
Roll 106: Marks=45,28,72, Failed subjects=1
Roll 107: Marks=90,95,30, Failed subjects=1
Roll 108: Marks=50,60,70, Failed subjects=0
Roll 109: Marks=20,25,30, Failed subjects=3
Roll 110: Marks=40,35,32, Failed subjects=1

Output 9: Different file name

========================================
     STUDENT RESULTS ANALYSIS
========================================
Input file: grades.txt
Passing marks: 33

STUDENTS WHO FAILED IN EXACTLY ONE SUBJECT:
-------------------------------------------
Roll No: 102, Name: Jane Doe, Marks: 32,78,65
Roll No: 106, Name: David Lee, Marks: 45,28,72
Roll No: 107, Name: Emma Davis, Marks: 90,95,30
Roll No: 110, Name: Henry Clark, Marks: 40,35,32

STUDENTS WHO PASSED IN ALL SUBJECTS:
------------------------------------
Roll No: 101, Name: John Smith, Marks: 45,67,89
Roll No: 103, Name: Bob Johnson, Marks: 90,85,92
Roll No: 105, Name: Charlie Wilson, Marks: 33,33,33
Roll No: 108, Name: Frank Miller, Marks: 50,60,70

SUMMARY STATISTICS:
===================
Total students: 10
Students who failed exactly one subject: 4
Students who passed all subjects: 4
Other students (failed 0, 2, or 3 subjects): 2

Output 10: Malformed delimiter


Error: Invalid line format in line 1: '101; John Smith; 45; 67; 89'
Expected format: RollNo, Name, Marks1, Marks2, Marks3

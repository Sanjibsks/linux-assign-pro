Command 1: nano validate_results.sh

Explanation: I created the main script file using nano editor. The script includes functions for file validation, data parsing, and analysis, following modular programming principles for better maintainability.
Command 2: chmod +x validate_results.sh

Explanation: I added execute permissions to make the script runnable. This is essential for any shell script in Linux, as files without execute permission cannot be executed directly.
Command 3: Creating marks.txt with heredoc

Explanation: I created the main test data file with 10 student records using a heredoc. This method allows creating multi-line files with exact formatting and includes various test cases (passing, failing, boundary cases).
Command 4: Creating edge case test files

Explanation: I created additional test files to validate the script's robustness. These include empty files, files with invalid data, and files with incorrect formats to test error handling.
Command 5: Testing with marks.txt

Explanation: I ran the script with the main test file. The script successfully analyzed all students, categorized them correctly, and displayed formatted output with statistics.
Command 6: Testing with missing file argument

Explanation: I tested the script without any arguments. The script correctly validated the argument count and displayed a helpful usage message with error description.
Command 7: Testing with non-existent file

Explanation: I tested with a file that doesn't exist. The script used the -e test to check file existence and provided a clear error message, preventing file access errors.
Command 8: Testing with empty file

Explanation: I tested with an empty file. The script handled this gracefully by showing zero counts and appropriate "No students found" messages for each category.
Command 9: Testing with invalid data file

Explanation: I tested with a file containing non-numeric marks. The script validated each mark using regex pattern matching and exited with a descriptive error message when invalid data was encountered.
Command 10: Creating and testing all_pass.txt

Explanation: I created a file with only passing students to test that category. The script correctly identified all students as passing all subjects and displayed appropriate statistics.
Command 11: Creating and testing all_fail.txt

Explanation: I created a file with only failing students. The script correctly showed no students in either requested category and placed all in the "other" category with appropriate counts.
Command 12: Manual verification of calculations

Explanation: I performed manual verification using awk and a while loop to confirm the script's calculations were accurate. This confirmed the script was correctly counting failed subjects and categorizing students.
Command 13: Testing with different file name

Explanation: I tested the script with a copy of the data under a different name. This verified that the script works with any valid input file, not just the default name.
Command 14: Testing with malformed delimiter

Explanation: I tested with a file using wrong delimiters. The script validated the field count and format, providing a clear error message about the expected format.

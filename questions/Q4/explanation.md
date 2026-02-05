Command 1: nano emailcleaner.sh

Explanation: I created the main script file. The script includes functions for file validation, email processing using regex, duplicate removal, and statistics generation, following a modular design.
Command 2: chmod +x emailcleaner.sh

Explanation: I added execute permissions to the script. This is necessary for running shell scripts in Linux, as they require explicit execute permissions unlike batch files in Windows.
Command 3: Creating emails.txt with diverse test cases

Explanation: I created a comprehensive test file with 21 email entries. This includes valid emails, invalid emails, duplicates, and various edge cases to thoroughly test the script's regex pattern.
Command 4: Running the email cleaner script

Explanation: I executed the script. It processed the emails.txt file, extracted valid emails matching the pattern, removed duplicates, and generated both valid.txt and invalid.txt files with progress messages.
Command 5: Examining the output files

Explanation: I displayed the contents of valid.txt and invalid.txt. The valid.txt showed 6 unique, sorted email addresses, while invalid.txt showed 15 entries that didn't match the strict regex pattern.
Command 6: Creating test files for edge cases

Explanation: I created specialized test files for boundary conditions. These include empty files, all-valid files, all-invalid files, and mixed-case files to test the script's robustness.
Command 7: Testing with empty file

Explanation: I tested the script with an empty input file. The script handled this gracefully, creating empty output files and showing zero counts in the summary statistics.
Command 8: Testing with all valid emails

Explanation: I tested with a file containing only valid emails. The script correctly extracted all emails to valid.txt, leaving invalid.txt empty, confirming the regex pattern accepts properly formatted emails.
Command 9: Testing with all invalid emails

Explanation: I tested with a file containing only invalid emails. The script correctly identified all as invalid, placing them in invalid.txt and keeping valid.txt empty, demonstrating strict pattern enforcement.
Command 10: Testing with mixed case emails

Explanation: I tested with mixed case emails. The script accepted some (like User@Test.com) but rejected others (like USER@TEST.COM) due to case sensitivity in the regex pattern, showing the pattern's exact requirements.
Command 11: Testing with special characters

Explanation: I tested emails with special characters like dots, hyphens, and underscores. All were rejected because the pattern only allows alphanumeric characters before the @ symbol.
Command 12: Manual verification using regex

Explanation: I manually verified the regex pattern using grep commands. This confirmed the script's logic was correct and matched the expected behavior for each test case.
Command 13: Testing duplicate removal

Explanation: I tested duplicate removal functionality. The script successfully removed duplicate entries from valid.txt while preserving the original invalid entries, demonstrating proper use of sort -u.
Command 14: Restoring original test file

Explanation: I restored the original test file and listed all created files. This showed the complete set of files generated during the lab, including scripts, test data, and output files.

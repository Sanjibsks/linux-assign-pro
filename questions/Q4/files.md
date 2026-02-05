1. emailcleaner.sh (Main script)

#!/bin/bash

# Function to display usage
usage() {
    echo "Usage: $0"
    echo "Processes emails.txt and creates valid.txt and invalid.txt"
    echo "Note: emails.txt must exist in the current directory"
    exit 1
}

# Function to validate input file
validate_file() {
    if [ ! -f "emails.txt" ]; then
        echo "Error: emails.txt not found in current directory."
        usage
    fi
    
    if [ ! -r "emails.txt" ]; then
        echo "Error: emails.txt is not readable."
        exit 1
    fi
}

# Function to process emails
process_emails() {
    echo "Processing emails.txt..."
    
    # Define the regex pattern for valid email
    # Pattern: <letters_and_digits>@<letters>.com
    # ^[a-zA-Z0-9]+@[a-zA-Z]+\.com$
    VALID_PATTERN='^[a-zA-Z0-9]+@[a-zA-Z]+\.com$'
    
    echo "Extracting valid email addresses..."
    
    # Extract valid emails using grep with extended regex
    # -E: extended regular expressions
    # -o: only matching part
    # -i: case insensitive (optional, but specified in pattern)
    # Then sort uniquely to remove duplicates
    grep -E "$VALID_PATTERN" emails.txt > temp_valid.txt
    
    echo "Removing duplicates from valid emails..."
    
    # Remove duplicates and sort alphabetically
    sort -u temp_valid.txt > valid.txt
    
    # Remove temporary file
    rm -f temp_valid.txt
    
    echo "Extracting invalid email addresses..."
    
    # Extract invalid emails (those not matching the pattern)
    # -v: invert match (select non-matching lines)
    # -E: extended regex
    grep -v -E "$VALID_PATTERN" emails.txt > invalid.txt
    
    echo "Done!"
    
    # Generate statistics
    local total_count=$(wc -l < emails.txt 2>/dev/null)
    local valid_count=$(wc -l < valid.txt 2>/dev/null)
    local invalid_count=$(wc -l < invalid.txt 2>/dev/null)
    
    echo "Valid email addresses saved to: valid.txt"
    echo "Invalid email addresses saved to: invalid.txt"
    echo ""
    echo "Summary:"
    echo "Total emails processed: ${total_count:-0}"
    echo "Valid emails found: ${valid_count:-0}"
    echo "Invalid emails found: ${invalid_count:-0}"
}

# Function to explain regex pattern
explain_pattern() {
    echo ""
    echo "Regex Pattern Explanation:"
    echo "-------------------------"
    echo "Pattern used: ^[a-zA-Z0-9]+@[a-zA-Z]+\\.com\$"
    echo "^              : Start of line"
    echo "[a-zA-Z0-9]+   : One or more letters or digits (local part)"
    echo "@              : Literal @ symbol"
    echo "[a-zA-Z]+      : One or more letters (domain name)"
    echo "\\.com         : Literal .com (must have dot before com)"
    echo "\$             : End of line"
    echo ""
    echo "Examples of valid emails: user123@company.com, test@test.com"
    echo "Examples of invalid emails: user@123.com, user@company.net, user-name@test.com"
}

# Main function
main() {
    # Check if emails.txt exists
    validate_file
    
    # Process the emails
    process_emails
    
    # Optional: explain the pattern
    # Uncomment the line below to show explanation
    # explain_pattern
    
    exit 0
}

# Execute main function
main

2. emails.txt (Original test data - 21 entries)

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

3. valid.txt (Generated valid emails)

123@test.com
alice123@company.com
jane.doe123@company.com
john.doe@example.com
test@123.com
valid@email.com

4. invalid.txt (Generated invalid emails)

@nodomain.com
another@valid.com
bob-smith@test.com
contact@support.com
invalid-email
john.doe@example.com
nodomain@.com
notanemail.com
test@com
test@company.net
user@123.com
user@company.co.uk
user@domain.org
user@sub.domain.com
user.name@company.com

5. empty.txt (Empty file for testing)
6. all_valid.txt (All valid emails test)

user1@test.com
user2@test.com
user3@test.com
user4@test.com

7. all_invalid.txt (All invalid emails test)
invalid
@test.com
test@.com
test@com

8. mixed_case.txt (Mixed case emails)

User@Test.com
USER@TEST.COM
user@test.com
User.Name@Company.Com

9. special_chars.txt (Emails with special characters)

user-name@test.com
user_name@test.com
user.name@test.com
user+tag@test.com
user@test-test.com
user@test.com.com

10. duplicates.txt (File with duplicates)

test@test.com
test@test.com
test@test.com
user@user.com
user@user.com
another@another.com

11. original_emails.txt (Backup of original test data)
12. manual_valid.txt (Manual validation output)
13. manual_invalid.txt (Manual validation output)

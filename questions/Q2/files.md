1. log_analyzer.sh (Main script)
bash

#!/bin/bash

# Function to display usage
usage() {
    echo "Error: $1"
    echo "Usage: $0 <logfile>"
    exit 1
}

# Function to validate the log file
validate_file() {
    if [ $# -ne 1 ]; then
        usage "Please provide exactly one log file name."
    fi
    
    if [ ! -e "$1" ]; then
        usage "File '$1' does not exist or is not readable."
    fi
    
    if [ ! -f "$1" ]; then
        usage "'$1' is not a regular file."
    fi
    
    if [ ! -r "$1" ]; then
        usage "File '$1' exists but is not readable."
    fi
}

# Function to analyze the log file
analyze_log() {
    local logfile="$1"
    local report_file="$2"
    
    # Initialize counters
    local total_entries=0
    local info_count=0
    local warning_count=0
    local error_count=0
    
    # Get current date and time for report
    local current_date=$(date +%Y-%m-%d)
    local current_time=$(date +%H:%M:%S)
    
    # Count total entries
    total_entries=$(wc -l < "$logfile")
    
    # Count by log level (case-insensitive)
    info_count=$(grep -c -i " INFO " "$logfile")
    warning_count=$(grep -c -i " WARNING " "$logfile")
    error_count=$(grep -c -i " ERROR " "$logfile")
    
    # Get most recent ERROR message
    local recent_error=""
    if [ $error_count -gt 0 ]; then
        recent_error=$(grep -i " ERROR " "$logfile" | tail -1)
    else
        recent_error="N/A (No ERROR messages found)"
    fi
    
    # Generate report
    {
        echo "========================================"
        echo "       LOG FILE ANALYSIS REPORT"
        echo "========================================"
        echo "File analyzed: $logfile"
        echo "Analysis date: $current_date"
        echo "Analysis time: $current_time"
        echo ""
        echo "SUMMARY STATISTICS:"
        echo "==================="
        echo "Total log entries: $total_entries"
        echo "INFO messages: $info_count"
        echo "WARNING messages: $warning_count"
        echo "ERROR messages: $error_count"
        echo ""
        echo "ERROR ANALYSIS:"
        echo "==============="
        echo "Most recent ERROR message:"
        echo "$recent_error"
    } | tee /dev/tty > "$report_file"
    
    echo ""
    echo "Report saved to: $report_file"
}

# Main script execution
main() {
    # Validate input
    validate_file "$@"
    
    local logfile="$1"
    local current_date=$(date +%Y-%m-%d)
    local report_file="logsummary_${current_date}.txt"
    
    # Analyze log file
    analyze_log "$logfile" "$report_file"
    
    exit 0
}

# Execute main function
main "$@"

2. sample.log (Sample log file - 10 entries)

2025-01-12 10:15:22 INFO System started
2025-01-12 10:16:01 ERROR Disk not found
2025-01-12 10:16:45 WARNING High memory usage
2025-01-12 10:17:10 ERROR Network timeout
2025-01-12 10:18:00 INFO Backup completed
2025-01-12 10:19:30 ERROR Permission denied
2025-01-12 10:20:15 INFO User login successful
2025-01-12 10:21:45 WARNING CPU usage at 85%
2025-01-12 10:22:30 ERROR Database connection failed
2025-01-12 10:23:00 INFO Cache cleared

3. empty.log (Empty log file for testing)

(0 bytes, no content)
4. malformed.log (Log file with invalid entries)

2025-01-12 10:15:22 INFO System started
INVALID FORMAT
2025-01-12 10:16:01 ERROR Disk not found
2025-01-12 10:16:45
WARNING High memory usage

5. no_errors.log (Log file with no ERROR entries)

2025-01-12 10:15:22 INFO System started
2025-01-12 10:16:45 WARNING High memory usage
2025-01-12 10:18:00 INFO Backup completed

6. logsummary_2025-02-05.txt (Generated report file)

(Content matches terminal output format)

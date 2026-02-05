1. Creating the log_analyzer.sh script

nano log_analyzer.sh

2. Making the script executable
chmod +x log_analyzer.sh

3. Creating a sample log file for testing

cat > sample.log << 'EOF'
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
EOF

4. Creating an empty log file for edge case testing

touch empty.log

5. Testing with no argument

./log_analyzer.sh

6. Testing with non-existent file

./log_analyzer.sh nonexistent.log

7. Testing with unreadable file

touch unreadable.log
chmod 000 unreadable.log
./log_analyzer.sh unreadable.log
chmod 644 unreadable.log
rm unreadable.log

8. Testing with valid log file

./log_analyzer.sh sample.log

9. Testing with empty log file

./log_analyzer.sh empty.log

10. Creating a malformed log file

cat > malformed.log << 'EOF'
2025-01-12 10:15:22 INFO System started
INVALID FORMAT
2025-01-12 10:16:01 ERROR Disk not found
2025-01-12 10:16:45
WARNING High memory usage
EOF
./log_analyzer.sh malformed.log

11. Creating a log file with no ERROR messages

cat > no_errors.log << 'EOF'
2025-01-12 10:15:22 INFO System started
2025-01-12 10:16:45 WARNING High memory usage
2025-01-12 10:18:00 INFO Backup completed
EOF
./log_analyzer.sh no_errors.log

12. Testing manual verification of counts

wc -l sample.log
grep -c "INFO" sample.log
grep -c "WARNING" sample.log
grep -c "ERROR" sample.log

13. Checking generated report file

ls -la logsummary_*.txt
cat logsummary_2025-02-05.txt

14. Testing with multiple files (invalid case)

./log_analyzer.sh sample.log empty.log

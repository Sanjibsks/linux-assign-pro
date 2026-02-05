1. Creating the signal handling C program
nano signal_demo.c

2. Creating a Makefile for compilation

nano Makefile

3. Compiling the program

make

or

gcc -o signal_demo signal_demo.c

4. Running the signal handling demonstration

./signal_demo

5. Testing in the background to monitor processes

./signal_demo &
DEMO_PID=$!
echo "Main program PID: $DEMO_PID"
sleep 2
ps -eo pid,ppid,cmd | grep -E "(signal_demo|PID)" | grep -v grep

6. Sending signals manually to test handling

# Start program in background
./signal_demo &
DEMO_PID=$!
echo "Program PID: $DEMO_PID"

# Send SIGTERM after 2 seconds
sleep 2
echo "Sending SIGTERM to PID $DEMO_PID"
kill -TERM $DEMO_PID

# Wait and check if still running
sleep 1
ps -p $DEMO_PID > /dev/null && echo "Program still running" || echo "Program terminated"

7. Creating a version with different signal handlers

nano signal_advanced.c
gcc -o signal_advanced signal_advanced.c
./signal_advanced

8. Testing with signal masking and blocking

nano signal_block.c
gcc -o signal_block signal_block.c
./signal_block

9. Monitoring signals with strace

strace -e signal -f ./signal_demo 2>&1 | grep -E "(SIGTERM|SIGINT|kill)"

10. Testing error cases and edge conditions

# Create a program that handles invalid signals
nano signal_error.c
gcc -o signal_error signal_error.c
./signal_error

11. Testing with multiple concurrent signals

nano signal_concurrent.c
gcc -o signal_concurrent signal_concurrent.c
./signal_concurrent

12. Creating a script to run comprehensive tests

nano run_signal_tests.sh
chmod +x run_signal_tests.sh
./run_signal_tests.sh

13. Testing signal handling in child processes

nano signal_child.c
gcc -o signal_child signal_child.c
./signal_child

14. Using different signal sending methods

# Start program
./signal_demo &
PID=$!

# Send SIGTERM using different methods
kill -TERM $PID
kill -15 $PID  # SIGTERM is signal 15
pkill -TERM signal_demo

# Send SIGINT using different methods
kill -INT $PID
kill -2 $PID   # SIGINT is signal 2
pkill -INT signal_demo

15. Checking signal dispositions

# Check default signal handling
trap -l
kill -l

# Check signal handling for current shell
trap

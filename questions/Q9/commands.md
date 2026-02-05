. Creating the C program file

nano zombie_prevent.c

2. Creating a Makefile for easier compilation

nano Makefile

3. Compiling the C program

make

or

gcc -o zombie_prevent zombie_prevent.c

4. Running the program to demonstrate zombie prevention

./zombie_prevent 5

5. Running with different number of child processes

./zombie_prevent 3
./zombie_prevent 8

6. Testing with invalid arguments

./zombie_prevent
./zombie_prevent 0
./zombie_prevent -2
./zombie_prevent abc

7. Creating a program that creates zombies (for comparison)

nano zombie_create.c

8. Compiling and running the zombie creator

gcc -o zombie_create zombie_create.c
./zombie_create 3 &
sleep 2
ps aux | grep -E "(zombie|defunct)"
kill %1

9. Monitoring processes while program runs
bash

# Terminal 1: Run the program
./zombie_prevent 4 &

# Terminal 2: Monitor processes
watch -n 0.5 'ps -eo pid,ppid,state,cmd | grep -E "(zombie_prevent|defunct)" | grep -v grep'

10. Creating a script to run multiple tests

nano run_tests.sh
chmod +x run_tests.sh
./run_tests.sh

11. Checking the process tree

# Run program in background
./zombie_prevent 3 &
# Get the parent PID
sleep 1
pstree -p $(pgrep zombie_prevent)

12. Testing with waitpid() options

nano waitpid_demo.c
gcc -o waitpid_demo waitpid_demo.c
./waitpid_demo 4

13. Creating a program with signal handling for zombie prevention

nano signal_zombie.c
gcc -o signal_zombie signal_zombie.c
./signal_zombie 3

14. Stress testing with many child processes

time ./zombie_prevent 50

15. Checking system limits

ulimit -u
ulimit -n


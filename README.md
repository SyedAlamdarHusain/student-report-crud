[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/_fBs5sT8)

# Compile

```bash
make
```

# Running The Program:

## First run the PrimaryLikesServer as:

```bash
./PrimaryLikesServer
```

## Run ParentProcess on a separate terminal as:

```bash
./ParentProcess
```

## Real-Time Log Monitoring (Optional):

To monitor log output in real-time while the PrimaryLikesServer and ParentProcess are running in separate terminals, you can use the tail -f command, as described in the project documentation:
```bash
tail -f /tmp/PrimaryLikesLog
``` 

# Submission Date:

Project Submitted on November 7 (Five Days Extra Credit): The date to pull from GitHub in your README is November 7.


# Implementation:
First I implemented ParentProcess to fork 10 child processes, then I implemented sockets by passing a single like between ParentProcess and PrimaryLikesServer once that was successful, I implemented Likeserver function where each LikesServer is forked one second before the previous child and sends a random number of likes between 0 and 42 to PrimaryLikesServer over 5 minutes with  1 to 5 random interval, finally once the data was transfer back I implemented bi-directional connection by having PrimaryLikesServer responding back to LikesServer based on if data transfer was successful.

# Things to notice:

## ParentProcess Status

The /tmp/ParentProcessStatus should be open as:
```bash
cat /tmp/ParentProcessStatus
```
The log file contains the starting time of each child fork and the ending time along with the status code 0 indicating success and 1 indicating failure. The log file also contains any connection or receive error that a LikesServer gets and the likeserver number it came from.

## PrimaryLikesLog

The /tmp/PrimaryLikesLog should be open as:
```bash
cat /tmp/PrimaryLikesLog
```
The log file contains each successful like sent from LikesServer to PrimaryLikesServer and the total-like-counter that is updated after each like sent. If invalid data is passed it simply logs "Invalid data" followed by the data passed and doesn't increment the total likes.

## LikesServerLog

The /tmp/LikesServer should be open as:
```bash
cat /tmp/LikesServer0
```
The like server log file contains the number of likes sent in its running period and the return code from the IPS to the PrimaryLikesServer with 0 if successful and 1 if it was unsuccessful for each like sent. The like server log file also logs specific errors received by the like server. 




[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/xR-cYv8r)
# project1
Answer these questions please:
Tell me what this project is about?
Tell me how your thought process for completing the project?
Any issues you came across?

## Project Info

The code implements a simple linux shell to perform basic linux commands. The shell allows users to enter commands and executes them. The shell code provides features such as handling the "exit" command with optional status exit and processing the /proc command by displaying contents from the proc filesystem. Furthermore, the shell code provide history command feature to store all the commands the user enters in a hidden file called .421sh and displays the 10 most recent command when the user enters "history" command in user prompt from that hidden file.

## Thought Process

My thought process for completing this project was to complete the project in parts. First, I focused on obtaining the `user_prompt_loop`. After completing that, I moved on to parsing and execution. Once these stages were finished, I proceeded to work on the `proc` command system. I then implemented the history command functionality. When the core functionality was fully developed, I tackled the exit shell command by freeing all allocated memory. 

## Issues that I came across and the ways I solved it
During this process, I encountered an issue where the `free` command failed to execute when exiting, leading to a memory leak. To address this, I made the command a global variable. Another memory leak issue occurred when I entered an invalid command, and the forked process was terminated, leaving memory still reachable. To solve this problem, I implemented `free` memory just before the process termination.

## Assumptions in the Code

- The `proc` command should be executed simply as `proc` rather than `/proc` as initially indicated in the Project 1 file's output. Therefore, for the `environ`, `status`, and `sched` commands, `proc` can be used in the following format: `proc /pid/environ`. As for the `cpuinfo` and `loadavg` commands, they can be executed as `proc /cpuinfo` or `proc cpuinfo`. 
- The `history` command would show the most recent commands from the bottom, as it is done in bash.
- The PID receieved from running the top command which is shown after running `top &` on the background from another terminal can be run as usual. However, any other PID which isn't from top command may need to be run as `sudo` to grant access priviledge for the program to read from proc file.
- The proc shows error message to invalid proc command as "Unable to open the proc file". This error can be due to both an invalid command for proc as well due to access priviledge for proc file that wasn't able to open due to not having root privilege.
- Exit command that is run with a status displays the status that code existed from. Whereas an invalid command for exit shows as error message that there was a invalid argument for exit. 

## Extra Credit

- Project was Submitted on Oct 10 (5 days - 5 points). 

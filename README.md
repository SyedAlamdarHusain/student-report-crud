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

# Challenges and Solution

One of the issues I came across was that after exiting PrimaryLikesServer the log file would not have all the logs written to it. So resolve this, I created a helper function to handle ctr + c exit for PrimaryLikesServer to cleanup and close the file to make all the logs is written to the log file and nothing is lost. Another issue was whenever an child likeserver failed it resulted in a memory leak. To solve, this I made sure whenever LikesServer exits I close the log file to avoid the memory leak.

# Things to notice:

## ParentProcess Status

The /tmp/ParentProcessStatus should be open as:
```bash
cat /tmp/ParentProcessStatus
```
The log file contains the starting time of each child fork and the ending time along with the status code 0 indicating success and 1 indicating failure. The program except that whenever a likeserver fails it exit with return code of 1 as noted in project doc and terminates before it runtime of 5 minutes.  The log file also contains any connection or receive error that a LikesServer gets and the likeserver number it came from.

## PrimaryLikesLog

The /tmp/PrimaryLikesLog should be open as:
```bash
cat /tmp/PrimaryLikesLog
```
The log file contains each successful like sent from LikesServer to PrimaryLikesServer and the total-like-counter that is updated after each like sent. If invalid data is passed it simply logs "Invalid data" followed by the data passed and doesn't increment the total likes. Since PrimaryLikesServer runs indefinitely it can accept connection from multiple runs of ParentProcess and have logs of each of them.

## LikesServerLog

The /tmp/LikesServer should be open as:
```bash
cat /tmp/LikesServer0
```

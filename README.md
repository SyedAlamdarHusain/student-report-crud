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

To monitor real-time log output while the PrimaryLikesServer and ParentProcess run in separate terminals, the tail -f command can be used in a separate terminal as:

```bash
tail -f /tmp/PrimaryLikesLog
``` 

# Submission Date:

Project Submitted with Five Days of Extra Credit: The GitHub pull date is November 7.


# Implementation:

First I implemented the ParentProcess to fork ten child processes. After that, I introduced socket communication by transferring a single "like" between the ParentProcess and PrimaryLikesServer. Upon successfully accomplishing this, I implemented the Likeserver function where each LikesServer is forked one second after the previous child and sends a random number of likes between 0 and 42 to PrimaryLikesServer over 5 minute time-period with 1 to 5 random intervals. Finally, once the data was transferred back, I implemented a bi-directional connection by having PrimaryLikesServer respond to LikesServer with 1 if the transfer was successful and 0 if it was unsuccessful.

# Challenges and Solution

One issue I encountered was that, after exiting PrimaryLikesServer, not all the logs were written to the log file. To address this, I created a helper function to handle Ctrl+C exits for PrimaryLikesServer, ensuring proper cleanup and file closure to ensure that all logs are written to the file without any data loss. Another issue was related to memory leaks which resulted when a chold-like server failed. To resolve this, I implemented a procedure to close the log file whenever a LikesServer process exits, preventing memory leaks.

# Things to notice:

## ParentProcess Status

The /tmp/ParentProcessStatus should be open as:
```bash
cat /tmp/ParentProcessStatus
```
The ParentProcessStatus log file includes the start time of each child fork, the end time, and status codes (0 indicating success and 1 indicating failure). The program ensures that when a Likeserver fails, it exits with a return code of 1, as specified in the project documentation, and terminates before its scheduled 5-minute runtime. The log file also records any connection or receive errors encountered by LikesServers with its corresponding Likeserver number.

## PrimaryLikesLog

The /tmp/PrimaryLikesLog should be open as:
```bash
cat /tmp/PrimaryLikesLog
```
The PrimaryLikesLog file records every successful "like" sent from LikesServer to PrimaryLikesServer, along with the total-like-counter, which is updated after each "like" is sent. If invalid data is provided, it simply logs "Invalid data" followed by the data, without incrementing the total likes. As PrimaryLikesServer runs indefinitely, it can accept connections from multiple runs of ParentProcess and maintain logs for each of them in the PrimaryLikesLog file.

## LikesServerLog

The /tmp/LikesServer should be open as:
```bash
cat /tmp/LikesServer0
```
The Likeserver log file includes the number of likes sent during its running period and the return code from the IPS to the PrimaryLikesServer, which is 0 for successful and 1 for unsuccessful "like" transmissions. The Likeserver log file also logs specific errors received by the Likeserver.

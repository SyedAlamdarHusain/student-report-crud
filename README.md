# Guide to Compile, Load, Unload, and Run the Module

## Compile

```bash
make
```

## Loading the module

```bash
sudo insmod blackjack.ko
```

## Writing to the character device

Any of these formats could be used to write to the blackjack

```bash
echo "Reset" > /dev/blackjack
```

```bash
echo "Shuffle" > /dev/blackjack
```

```bash
echo "Hit" > /dev/blackjack
```

### Both Hold or No command could be used in reponse to Not wanting to add another card to player hand

```bash
echo "No" > /dev/blackjack
```

```bash
echo "Hold" > /dev/blackjack
```

### When choosing to keep the same deck, the user is required to shuffle

```bash
echo "Shuffle" > /dev/blackjack
```

### When choosing to not keep the same deck, the user is required to reset

```bash
echo "Reset" > /dev/blackjack
```

## Reading from the character device

```bash
cat /dev/blackjack
```

## Unloading the module

```bash
sudo rmmod blackjack
```


# Implementation:

First I implemented the basic module to be able to load and unloaded. Once it was working, I moved to implement basic read and write function that provides ability to read and write to character device. Then I moved on implementing basic helper function to reset and shuffle cards. Then I moved to implementing deal function by dealing two cards to player and dealer. Then I moved on implementing HIT to add cards to player, then finally I moved on to HOLD function to implement Dealer's gameplay. Finally, once i was done with basic functionality, I moved on adding functionality for the types of card and then on handling aces. Finally, I moved on implementing winning condition. Once first round was implemented. I implemented functionality for second round when user chooses to use a new desk where I reset the game and then implemented functionality to next rounds where user chooses to play with the same deck by setting player and healer points to zero. Finally, when the basic game was done, I implemented error checking for invalid response and invalid commands.


# Challenges and Solutions:

The biggest challenges I was facing was that I wasn't able to add character without using mknod. To resolve this, I implemented READ, WRITE function for the module by  using.mode that helped me load the module without mknod and able the make the module being able read and write by user without need to have root/owner privileges. Next, the biggest challenge was making sure user enter correct command for each response. To tackle, I implemented bool variables that check each condition and set to true or false when they are done or needed to make sure each valid command is entered only when it's needed.






# Guide to compile, load, unload and read the character device:


# Reading from the character device

```bash
cat /dev/magic8ball
```


# Unloading the module

```bash
sudo rmmod magic8ball
```

# Compile

```bash
make
```

# Loading the module

```bash
sudo insmod magic8ball.ko
```

# Reading from the character device

```bash
cat /dev/magic8ball
```

# Unloading the module

```bash
sudo rmmod magic8ball
```

# Implementation:

First I implemented the basic module to be able to load and unloaded. Once it was working, I moved to implement basic read that provides user ability to read from the character device. Then I moved on implementing for the module to randomize the responses each time the user opens and tries to read from the character device

# Challenges and Solutions:

The biggest challenges I was facing was that I wasn't able to add character without using mknod. To resolve this, I implemented READ for the module by using ".mode" that helped me load the module without mknod and able the make the module being able read by user without need to have root/owner privileges.


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

Project Submitted with Five Days of Extra Credit: The GitHub pull date is November 7(Last Commit on November 7).


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

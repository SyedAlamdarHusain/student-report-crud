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

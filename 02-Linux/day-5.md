## Basic Commands (continue)

16. Combining Commands with Pipes
o When combining multiple commands using pipes, what can go wrong if one of the 
commands in the chain fails? How does the shell handle errors in such cases?

17. File Descriptors
o Explain what happens when you redirect output to a file that is already open. What 
will be the contents of the file after the command executes? How can you append 
to a file instead of overwriting it?

18. Using Wildcards
o If you use a wildcard to delete files, how can you ensure that only the intended files 
are affected? What precautions should you take before executing such a 
command?

19. Environment Variables
o If you set an environment variable in your session and then start a new terminal 
session, will the variable still be available? How can you make environment 
variables persist across sessions

20. Recovering Deleted Files
o After using a command to delete a file, how can you recover it if you realize it was 
deleted by mistake? What methods can be used to prevent permanent data loss?

21. Impact of Sleep Command
o If you run a command that includes a sleep command, how might this impact other 
processes running in the terminal or system? Can you cancel the sleep once it's 
initiated?

22. Using dd Command
o What are the potential risks of using a command to copy a disk image without 
specifying the correct target? What safety measures can you take to avoid data 
loss?

23. Changing Directories
o If you attempt to change into a directory that doesn’t exist, what will happen? How 
can you check for the existence of a directory before attempting to navigate into it?

24. File Ownership and Permissions
o If you copy a file from one directory to another where the user does not have write 
permission, what happens to the file's ownership? How can you maintain the 
original file's permissions during the copy?

25. System Shutdown
o If you schedule a command to run at a specific time but the system shuts down 
before the command executes, what will happen to that scheduled command? 
How can you manage commands that need to run after a reboot


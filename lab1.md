# Lab 1 Report

## cd command

1. No arguments
   
![Image](cd_noarg.png)

Working directory: /home (home directory). 

There was no output because when we do the cd command with no argument, there is no directory given to change to so we stay in the same directory and no change occurs.
This is not technically an error since the command still processes--it's just that there's no directory change since no argument was given.

---
2. Directory

![Image](cd_dir.png)

Working directory: /home (home directory).

We get sent to the lecture1 directory because we gave `lecture1` as an argument, allowing us to change directories properly. This is reflected in the terminal in line 2, as shown here: `[user@sahara ~/lecture1]`. 
This is not an error.

---
3. File

![Image](cd_file_error.png)

Working directory: /home/lecture1

The output is something like an error message saying Hello.java is not a directory. The cd command is meant specifically to change our current working directory, so this error makes sense, since files are different from directories/folders. A file, unlike a directory/folder, is not really a path we can go to in order to access other relative files (as files can't contain other files or folders).  



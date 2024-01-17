# Lab 1 Report

## cd command

1: No arguments
   
![Image](cd_noarg.png)

Working directory: /home (home directory). 

There was no output because when we do the cd command with no argument, there is no directory given to change to so we stay in the same directory and no change occurs.
This is not technically an error since the command still processes--it's just that there's no directory change since no argument was given.

---
2: Directory

![Image](cd_dir.png)

Working directory: /home (home directory).

We get sent to the lecture1 directory because we gave `lecture1` as an argument, allowing us to change directories properly. This is reflected in the terminal in line 2, as shown here: `[user@sahara ~/lecture1]`. 
This is not an error.

---
3: File

![Image](cd_file_error.png)

Working directory: /home/lecture1

The output is something like an error message saying Hello.java is not a directory. The cd command is meant specifically to change our current working directory, so a file argument would naturally cause an error due to files being different from directories/folders. A file, unlike a directory, is not exactly a path we can go to in order to access other relative files/folders (since files can't contain other files/folders).

## ls command

1: No arguments
   
![Image](ls_noarg.png)

Working directory: /home/lecture1

The output of the ls command with no arguments is every file and directory within /home/lecture1 (the working directory). Basically, it lists all the files/folders within the current working directory. The output is not an error.

---
2: Directory

![Image](ls_dir_msg.png)

---
3: File

![Image](ls_file_hello.png)

## cat command

1: No arguments

![Image](cat_noarg_error.png)

---
2: Directory

![Image](cat_dir_msg.png)

---
3: File
![Image](cat_file_hello.png)



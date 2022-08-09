[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![made-with-Markdown](https://img.shields.io/badge/Made%20with-Markdown-1f425f.svg)](http://commonmark.org)

# Simple shell

![Simple shell](https://i.imgur.com/9m8edhj.jpg)

# Table of Contents
- [Description](#description)
- [File Structure](#file-structure)
- [System and Library calls](#system-and-library-calls)
- [Installation](#installation)
- [Example of Use](#example-of-use)
- [Authors](#authors)

## Description
The Simple Shell is a simple UNIX command interpreter written entirely in C. The program runs based on bash commands obtained from the input stream by the user.
Any text seperated by a any number of spaces, tabs or a combination of both is considered to be an argument.
The respective command typed by the user is then parsed and executed as if in a UNIX shell.

**Basic lifetime of a shell**
1. Startup the shell
2. Wait for user input
3. Parse user input
4. Execute the command and return the result
4. Go back to step 2
* You could terminate the shell anytime, just type in the prompt the `exit` command or `Ctrl-D` which is interpreted as an end-of-file `EOF`

## File structure
This table contains a brief description of the working files of the project, click on the names to get the source code.

| File | Content | Description |
| --- | --- | --- |
| [main.h](main.h) | <pre>header of the project</pre> | <pre>Contain the structure, prototypes, macros and<br>external variable of the project.</pre> |
| [main_loop.c](main_loop.c) | <pre>int main();</pre> | <pre>Main loop, recieve input from the Command Line Interface<br>parse and execute it.</pre> |
| [tokenizers.c](tokenizers.c) | <pre>char **hsh_tokenizer();<br>char **tokenizer_path();</pre> | <pre>Split the input string into a array of tokens.<br>Split the environment variable PATH into an array of tokens.</pre> |
| [validators.c](validators.c) | <pre>char *validate_input();<br>int validate_spaces();</pre> | <pre>Validate if PATH exists<br>Validate spaces, tabs and line breaks.</pre> |
| [executors.c](executors.c) | <pre>int hsh_execute();<br>int hsh_execute_builtins();</pre> | <pre>Fork process and replace the child with a new program.<br>Choose from an array of builtin functions.</pre> |
| [builtin_functions.c](builtin_functions.c) | <pre>int hsh_cd();<br>int hsh_setenv();<br>int hsh_unsetenv();<br>int hsh_env();<br>int hsh_exit();</pre> | <pre>Change directory.<br>Change or add and environment variable.<br>Delete an environment variable from the environment.<br>Print the environment variables list.<br>Terminate the main loop and exit the shell.</pre> |
| [helper_functions.c](helper_functions.c) | <pre>void sigintH();<br>char *str_concat();<br>void *_realloc();</pre> | <pre>Handles SIGINT (CTRL + C).<br>Concatenate two strings.<br>Reallocate a memory block.</pre> |

## System and Library calls
This table lists all the System calls `2` and Library calls `3` used in this project, you could read more by clicking on their respective manual pages. 

| Name | Manual page | Brief description |
| --- | --- | --- |
| `access` | <pre>[man 2 access](https://man7.org/linux/man-pages/man2/access.2.html)</pre> | access() checks whether the calling process can access the file pathname.  If pathname is a symbolic link, it is dereferenced. |
| `chdir` | <pre>[man 2 chdir](https://man7.org/linux/man-pages/man2/chdir.2.html)</pre> | chdir() changes the current working directory of the calling process to the directory specified in one of its parameters. |
| `execve` | <pre>[man 2 execve](https://man7.org/linux/man-pages/man2/execve.2.html)</pre> | execve() allows a process to execute another program. |
| `exit` | <pre>[man 3 exit](https://man7.org/linux/man-pages/man3/exit.3.html)</pre> | exit() causes normal process termination. |
| `fork` | <pre>[man 2 fork](https://man7.org/linux/man-pages/man2/fork.2.html)</pre> | fork() creates a new process by duplicating the calling process. The new process is referred to as the child process. The calling process is referred to as the parent process. |
| `free` | <pre>[man 3 free](https://man7.org/linux/man-pages/man3/malloc.3.html)</pre> | free() frees the memory space from the heap, which must have been returned by a previous call to malloc(), calloc(), or realloc(). |
| `getcwd` | <pre>[man 3 getcwd](https://man7.org/linux/man-pages/man3/getcwd.3.html)</pre> | getcwd() copies an absolute pathname of the current working directory. |
| `getenv` | <pre>[man 3 getenv](https://man7.org/linux/man-pages/man3/secure_getenv.3.html)</pre> | getenv() searches the environment list to find the requested environment variable. |
| `getline` | <pre>[man 3 getline](https://man7.org/linux/man-pages/man3/getline.3.html)</pre> | getline() reads an entire line from input, storing the address of the buffer containing the text into a pointer. |
| `isatty` | <pre>[man 3 isatty](https://www.man7.org/linux/man-pages/man3/isatty.3.html)</pre> | isatty() tests whether a file descriptor refers to a terminal. |
| `malloc` | <pre>[man 3 malloc](https://man7.org/linux/man-pages/man3/malloc.3.html)</pre> | malloc() dynamically allocates a single large block of memory with the specified size. |
| `perror` | <pre>[man 3 perror](https://man7.org/linux/man-pages/man3/sys_nerr.3.html)</pre> | perror() produces a message on standard error describing the last error encountered during a call to a system or library function. |
| `signal` | <pre>[man 2 signal](https://man7.org/linux/man-pages/man2/signal.2.html)</pre> | signal() sets a function to handle signal i.e. a signal handler with signal number, or the address of a programmer-defined function. |
| `strtok` | <pre>[man 3 strtok](https://man7.org/linux/man-pages/man3/strtok.3.html)</pre> | strtok() breaks a string into a sequence of zero or more nonempty tokens. |
| `waitpid` | <pre>[man 2 waitpid](https://man7.org/linux/man-pages/man2/wait.2.html)</pre> | waitpid() suspends execution of the calling thread until a child specified by pid argument has changed state. |
| `fprintf` | <pre>[man 3 fprintf](https://man7.org/linux/man-pages/man3/printf.3.html)</pre> | fprintf() sends formatted output to a stream. |
| `setenv` | <pre>[man 3 setenv](https://man7.org/linux/man-pages/man3/setenv.3.html)</pre> | setenv() adds a variable to the environment. |
| `unsetenv` | <pre>[man 3 unsetenv](https://man7.org/linux/man-pages/man3/setenv.3.html)</pre> | unsetenv() deletes a variable from the environment. |
| `write` | <pre>[man 2 write](https://man7.org/linux/man-pages/man2/write.2.html)</pre> | write() writes to a file descriptor. |

## Installation

First, clone this repository to your local machine:

```
$ git clone https://github.com/schambig/holbertonschool-simple_shell
```

Then, go to the repository folder:

```
$ cd holbertonschool-simple_shell
```

Compile it with the following command:

```
$ gcc -Wall -Werror -Wextra -pedantic *.c -o hsh
```

Now you can run the shell in interactive mode:

```
$ ./hsh
```

Or you can run it in non-interactive mode:

```
$ echo "ls -la" | ./hsh
```

## Example of Use
Run the executable in your terminal after compiling:
```
#(ಠ_ಠ)->$ ls
AUTHORS              executors.c         hsh     main_loop.c         README.md     validators.c
builtin_functions.c  helper_functions.c  main.h  man_1_simple_shell  tokenizers.c
#(ಠ_ಠ)->$ pwd
/root/githubRepos/holbertonschool-simple_shell
#(ಠ_ಠ)->$
```

```
#(ಠ_ಠ)->$ ls -la
total 72
drwxr-xr-x  3 root root   232 Aug  7 23:01 .
drwxr-xr-x 14 root root  4096 Aug  8 12:22 ..
-rw-r--r--  1 root root   216 Aug  7 19:00 AUTHORS
-rw-r--r--  1 root root  4215 Aug  7 23:00 builtin_functions.c
-rw-r--r--  1 root root  2456 Aug  7 23:00 executors.c
drwxr-xr-x  8 root root   201 Aug  7 23:00 .git
-rw-r--r--  1 root root  1567 Aug  7 23:00 helper_functions.c
-rwxr-xr-x  1 root root 22744 Aug  7 23:01 hsh
-rw-r--r--  1 root root  1919 Aug  7 23:00 main.h
-rw-r--r--  1 root root  1782 Aug  7 23:00 main_loop.c
-rw-r--r--  1 root root  3703 Aug  7 18:58 man_1_simple_shell
-rw-r--r--  1 root root    29 Aug  7 18:36 README.md
-rw-r--r--  1 root root  2517 Aug  7 23:00 tokenizers.c
-rw-r--r--  1 root root  1749 Aug  7 23:00 validators.c
#(ಠ_ಠ)->$
```

## Authors
| [<img src="https://avatars.githubusercontent.com/u/98305125?v=4" width=115><br><sub> Johana Herrera </sub>](https://github.com/Johana-RHP) | [<img src="https://avatars.githubusercontent.com/u/103861356?v=4" width=115><br><sub> Drixner Condor </sub>](https://github.com/Drixner) | [<img src="https://avatars.githubusercontent.com/u/98289735?v=4" width=115><br><sub> Salomón Chambi </sub>](https://github.com/schambig) |
| :---: | :---: | :---: |

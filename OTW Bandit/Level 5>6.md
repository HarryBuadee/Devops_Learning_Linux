# Bandit Level 5 → Level 6

## Level Goal

The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:

human-readable
1033 bytes in size
not executable

Actions taken : 

```bash
bandit5@bandit:~$ ls
inhere
bandit5@bandit:~$ cd inhere/
bandit5@bandit:~/inhere$ find . -type f -size 1033c ! -executable
#I used the command above to find the file which had the size 1033 bytes not excuetbale and is humnan readable.
./maybehere07/.file2
bandit5@bandit:~/inhere$ cat ./maybehere07/.file2 HWasnPhtq9AVKe0dmk45nxy20cvUa6EG

```

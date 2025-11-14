# Bandit Level 2 → Level 3

##Level Goal

The password for the next level is stored in a file called --spaces in this filename-- located in the home directory

Actions taken:


````bash
bandit3@bandit:~$ ls
inhere
bandit3@bandit:~$ file inhere/
inhere/: directory
bandit3@bandit:~$ cd inhere/
bandit3@bandit:~/inhere$ ls
bandit3@bandit:~/inhere$ ls -a
.  ..  ...Hiding-From-You
bandit3@bandit:~/inhere$ cat ...Hiding-From-You
2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ



````


## Bandit Level 3 → Level 4

#Level Goal

The password for the next level is stored in a hidden file in the inhere directory.

Actions taken:

After getting into inhere directoy and using the ls command nothing appeared. I used the ls -a command which shown the hidden file.

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
bandit3@bandit:~/inhere$


````

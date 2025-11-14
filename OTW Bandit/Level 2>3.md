# Bandit Level 2 → Level 3

##Level Goal

The password for the next level is stored in a file called --spaces in this filename-- located in the home directory

Actions taken:

- The filename starts with -, so the shell thinks it’s an option. Therefore I used ./ makes the shell treat it as a file in the current directory, so cat reads it properly.
- The filename has spaces, so I put it in quotes to keep it as one argument. Without quotes, the shell would split it into separate words.
  
  
````bash
bandit2@bandit:~$ ls
--spaces in this filename--
bandit2@bandit:~$ cat "./--spaces in this filename--"
MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
bandit2@bandit:~$

````


# Bandit Level 7 → Level 8

## Level Goal

The password for the next level is stored in the file data.txt next to the word millionth

Actions taken:

```bash
bandit7@bandit:~$ ls
data.txt
bandit7@bandit:~$ grep "millionth" data.txt | awk '{print $2}'
dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
bandit7@bandit:~$
```

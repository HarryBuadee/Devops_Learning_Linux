# Bandit Level 13 → Level 14

## Level Goal
The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. 
Look at the commands that logged you into previous bandit levels, and find out how to use the key for this level.


`````
bandit13@bandit:~$ ls
sshkey.private
bandit13@bandit:~$ ls -l
total 4
-rw-r----- 1 bandit14 bandit13 1679 Oct 14 09:26 sshkey.private
bandit13@bandit:~$ chmod 600 sshkey.private
chmod: changing permissions of 'sshkey.private': Operation not permitted

bandit13@bandit:~$
`````

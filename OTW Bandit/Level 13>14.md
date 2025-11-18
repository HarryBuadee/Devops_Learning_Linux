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
`````
- I tried changing the permissions that I could read and write the sshkey,private file but the operation
  was not permitted:
`````
bandit13@bandit:~$ chmod 600 sshkey.private
chmod: changing permissions of 'sshkey.private': Operation not permitted
bandit13@bandit:~$
`````
I used the command 'cat' to display the key and copy it to notepad.
and then exited the bandit leel
bandit13@bandit:~$ cat sshkey.private
bandit13@bandit:~$ exit

- Created a text file named mykey and copied the key to it.

~ vim mykey


➜  ~ ssh -i ~/mykey -p 2220 bandit14@bandit.labs.overthewire.org
                         _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

backend: gibson-0
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Permissions 0644 for '/home/harry/mykey' are too open.
It is required that your private key files are NOT accessible by others.
This private key will be ignored.
Load key "/home/harry/mykey": bad permissions
bandit14@bandit.labs.overthewire.org's password:
Permission denied, please try again.
bandit14@bandit.labs.overthewire.org's password:
Permission denied, please try again.
bandit14@bandit.labs.overthewire.org's password:
bandit14@bandit.labs.overthewire.org: Permission denied (publickey,password).



bandit14@bandit:~$ cat /etc/bandit_pass/bandit14
MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS









# Bandit Level 9 → Level 10

## Level Goal

The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several ‘=’ characters.

Actions taken:

```bash
bandit9@bandit:~$ cat data.txt | grep "="
grep: (standard input): binary file matches

````
- The command above outputted that text file is binary
````
bandit9@bandit:~$ strings data.txt | grep "="
FB`=
c\5D=
========== the
?/=l
=Uc1
=vG*2P
========== password
k=ezG
E========== is
=%r_
.?=Dm
O&A=n
5========== FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
=*^Y
=L3jT
q<=,
'QHE=
+=NBf
bandit9@bandit:~$
````

- I used strings infront of the pipeline to filter out all
of the unreadable charaters leaving only human readable 
charatcters.
- Then grep "=" searches through that readable output and 
shows only the line that contains the = sign, which is 
where the password is stored.


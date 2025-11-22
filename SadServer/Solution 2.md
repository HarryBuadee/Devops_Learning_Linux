# Solution: "Saskatoon": counting IPs.

## Goals

- Find out what's the IP address that has the most requests in the file./home/admin/highestip.txt

- Test the soltuion by the SHA1 cheksum of the IP addrtess sha1sum /home/admin/highestip.txt is 6ef426c40652babc0d081d438b9f353709008e93 

- Write soluition into a file /home/admin/highestip.txt

## Actions taken:

- Checked the log file.
```
admin@ip-172-31-27-155:~$ cat /home/admin/access.log

````
- Used the command to identify the most active IP address in the access log and to show how many requests it made.
````
admin@ip-172-31-27-155:/$ awk '{print $1}' /home/admin/access.log | sort | uniq -c | sort -nr | head -n 1
    482 66.249.73.135
````
This printed only the IP address not the amount of times it appeared aswell
````
admin@ip-172-31-27-155:/$  awk '{print $1}' /home/admin/access.log | sort | uniq -c | sort -nr | head -1 | awk '{print $2}'
66.249.73.135
````
Wrote the soluition into the /home/admin/highestip.txt
````
admin@ip-172-31-27-155:/$  awk '{print $1}' /home/admin/access.log | sort | uniq -c | sort -nr | head -1 | awk '{print $2}' > /home/admin/highestip.txt
````
- Checked the file’s SHA-1 hash value

````
admin@ip-172-31-27-155:/$ sha1sum /home/admin/highestip.txt
6ef426c40652babc0d081d438b9f353709008e93  /home/admin/highestip.txt
admin@ip-172-31-27-155:/$

````

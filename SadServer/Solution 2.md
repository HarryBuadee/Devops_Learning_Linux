

Goals

- Find out what's the IP address that has the most requests in thif ile./home/admin/highestip.txt




- Test the soltuion by the SHA1 cheksum of the IP addrtess sha1sum /home/admin/highestip.txt is 6ef426c40652babc0d081d438b9f353709008e93 

Write sol;tion to a 

admin@ip-172-31-27-155:/$ awk '{print $1}' /home/admin/access.log | sort | uniq -c | sort -nr | head -n 1
    482 66.249.73.135
admin@ip-172-31-27-155:/$    awk '{print $1}' /home/admin/access.log | sort | uniq -c | sort -nr | head -1
    482 66.249.73.135
admin@ip-172-31-27-155:/$  awk '{print $1}' /home/admin/access.log | sort | uniq -c | sort -nr | head -1 | awk '{print $2}'
66.249.73.135
admin@ip-172-31-27-155:/$  awk '{print $1}' /home/admin/access.log | sort | uniq -c | sort -nr | head -1 | awk '{print $2}' > /home/admin/highestip.txt
admin@ip-172-31-27-155:/$ sha1sum /home/admin/highestip.txt
6ef426c40652babc0d081d438b9f353709008e93  /home/admin/highestip.txt
admin@ip-172-31-27-155:/$



# Solution: Killing the process writing to /var/log/bad.log

## Goals:

- Locate the responsible process filling up the disk

- Stop it

- Address the problem without removing the log file

Actions taken:

- Used ps auxf to display what processes are running. There wasn't an obivous process that stuck out for me. As you can see below:
```
admin@ip-10-1-12-200:~$ ps auxf
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           2  0.0  0.0      0     0 ?        S    20:07   0:00 [kthreadd]
root           3  0.0  0.0      0     0 ?        I<   20:07   0:00  \_ [rcu_gp]
root           4  0.0  0.0      0     0 ?        I<   20:07   0:00  \_ [rcu_par
root           5  0.0  0.0      0     0 ?        I    20:07   0:00  \_ [kworker
root           6  0.0  0.0      0     0 ?        I<   20:07   0:00  \_ [kworker
root           7  0.0  0.0      0     0 ?        I    20:07   0:00  \_ [kworker
root           8  0.0  0.0      0     0 ?        I<   20:07   0:00  \_ [mm_perc
root           9  0.0  0.0      0     0 ?        S    20:07   0:00  \_ [rcu_tas
root          10  0.0  0.0      0     0 ?        S    20:07   0:00  \_ [rcu_tas
root          11  0.0  0.0      0     0 ?        S    20:07   0:00  \_ [ksoftir
root          12  0.0  0.0      0     0 ?        I    20:07   0:00  \_ [rcu_sch
root          13  0.0  0.0      0     0 ?        S    20:07   0:00  \_ [migrati
root          14  0.0  0.0      0     0 ?        I    20:07   0:00  \_ [kworker
root          15  0.0  0.0      0     0 ?        S    20:07   0:00  \_ [cpuhp/0
root          16  0.0  0.0      0     0 ?        S    20:07   0:00  \_ [cpuhp/1
root          17  0.2  0.0      0     0 ?        S    20:07   0:00  \_ [migrati
root          18  0.0  0.0      0     0 ?        S    20:07   0:00  \_ [ksoftir
root          19  0.0  0.0      0     0 ?        I    20:07   0:00  \_ [kworker
root          20  0.0  0.0      0     0 ?        I<   20:07   0:00  \_ [kworker
root          22  0.0  0.0      0     0 ?        I    20:07   0:00  \_ [kworker
root          23  0.0  0.0      0     0 ?        S    20:07   0:00  \_ [kdevtmp
root          24  0.0  0.0      0     0 ?        I<   20:07   0:00  \_ [netns]
root          25  0.0  0.0      0     0 ?        S    20:07   0:00  \_ [kauditd
root          26  0.0  0.0      0     0 ?        S    20:07   0:00  \_ [khungta
root          27  0.0  0.0      0     0 ?        S    20:07   0:00  \_ [oom_rea
root          28  0.0  0.0      0     0 ?        I<   20:07   0:00  \_ [writeba
root          29  0.0  0.0      0     0 ?        S    20:07   0:00  \_ [kcompac
root          30  0.0  0.0      0     0 ?        SN   20:07   0:00  \_ [ksmd]
root          49  0.0  0.0      0     0 ?        I<   20:07   0:00  \_ [kintegr
root          50  0.0  0.0      0     0 ?        I<   20:07   0:00  \_ [kblockd
root          51  0.0  0.0      0     0 ?        I<   20:07   0:00  \_ [blkcg_p
root          52  0.0  0.0      0     0 ?        I    20:07   0:00  \_ [kworker
root          53  0.0  0.0      0     0 ?        I<   20:07   0:00  \_ [kworker
root          54  0.0  0.0      0     0 ?        S    20:07   0:00  \_ [kswapd0
root          55  0.0  0.0      0     0 ?        I<   20:07   0:00  \_ [kthrotl
root          56  0.0  0.0      0     0 ?        I<   20:07   0:00  \_ [acpi_th
root          57  0.0  0.0      0     0 ?        I<   20:07   0:00  \_ [nvme-wq
root          58  0.0  0.0      0     0 ?        I<   20:07   0:00  \_ [nvme-re
root          59  0.0  0.0      0     0 ?        I<   20:07   0:00  \_ [nvme-de
root          60  0.0  0.0      0     0 ?        I    20:07   0:00  \_ [kworker
root          61  0.0  0.0      0     0 ?        I    20:07   0:00  \_ [kworker
root          62  0.0  0.0      0     0 ?        I<   20:07   0:00  \_ [kworker
root          63  0.0  0.0      0     0 ?        I<   20:07   0:00  \_ [ipv6_ad
root          70  0.0  0.0      0     0 ?        I    20:07   0:00  \_ [kworker
root          73  0.0  0.0      0     0 ?        I<   20:07   0:00  \_ [kstrp]
root          78  0.0  0.0      0     0 ?        I<   20:07   0:00  \_ [kworker
root         113  0.0  0.0      0     0 ?        I<   20:07   0:00  \_ [ena]
root         132  0.0  0.0      0     0 ?        S    20:07   0:00  \_ [jbd2/nv
root         133  0.0  0.0      0     0 ?        I<   20:07   0:00  \_ [ext4-rs
root         193  0.0  0.0      0     0 ?        I    20:07   0:00  \_ [kworker
root         236  0.0  0.0      0     0 ?        I<   20:07   0:00  \_ [cryptd]
root         314  0.0  0.0      0     0 ?        I    20:07   0:00  \_ [kworker
root         665  0.0  0.0      0     0 ?        I    20:08   0:00  \_ [kworker
root           1  1.6  2.1  98152  9968 ?        Ss   20:07   0:03 /sbin/init
root         195  0.1  2.7  56592 12760 ?        Ss   20:07   0:00 /lib/systemd
root         212  0.0  1.1  19496  5144 ?        Ss   20:07   0:00 /lib/systemd
root         395  0.0  1.2  99884  5616 ?        Ssl  20:08   0:00 /sbin/dhclie
root         470  0.0  1.1  99884  5584 ?        Ssl  20:08   0:00 /sbin/dhclie
admin        565  0.0  2.7 1304140 12656 ?       S<sl 20:08   0:00 /usr/local/g
admin        670  0.0  0.9   6740  4528 pts/0    S<s+ 20:08   0:00  \_ bash -l
admin        674  0.1  4.1  98188 19268 pts/0    S<l+ 20:08   0:00      \_ /usr
admin        677  0.0  3.0  24456 14364 pts/0    S<+  20:08   0:00          \_ 
admin        678  0.0  0.1   2480   508 pts/1    S<s  20:08   0:00          \_ 
admin        679  0.0  0.9   6820  4428 pts/1    S<   20:08   0:00             
admin        705  0.0  0.6   8804  3168 pts/1    R<+  20:10   0:00             
admin        566  0.0  2.3 1080936 10824 ?       S<sl 20:08   0:00 /home/admin/
root         569  0.0  0.5   5636  2736 ?        Ss   20:08   0:00 /usr/sbin/cr
message+     570  0.0  0.8   7864  3800 ?        Ss   20:08   0:00 /usr/bin/dbu
root         572  0.0  0.9 220796  4232 ?        Ssl  20:08   0:00 /usr/sbin/rs
root         585  0.0  1.4  13504  6784 ?        Ss   20:08   0:00 /lib/systemd
root         591  0.1  0.3   2872  1724 tty1     Ss+  20:08   0:00 /sbin/agetty
root         592  0.0  0.4   4396  2064 ttyS0    Ss+  20:08   0:00 /sbin/agetty
admin        594  0.0  1.7  12508  8268 ?        S    20:08   0:00 /usr/bin/pyt
root         595  0.0  1.5  13348  7016 ?        Ss   20:08   0:00 sshd: /usr/s
root         604  0.0  3.7  26612 17472 ?        Ss   20:08   0:00 /usr/bin/pyt
_chrony      607  0.0  0.8  10852  3740 ?        S    20:08   0:00 /usr/sbin/ch
_chrony      610  0.0  0.1  10724   556 ?        S    20:08   0:00  \_ /usr/sbi
root         694  0.0  0.7   5788  3396 ?        Ss   20:10   0:00 /bin/bash /r
root         703  0.0  2.1  93604 10092 ?        S    20:10   0:00  \_ curl --o

```
- Used the lsof command to view open files, and by targeting /var/log/bad.log, it displayed only the processes actively using that log file.
```
admin@ip-10-1-12-200:~$ lsof /var/log/bad.log
COMMAND   PID  USER   FD   TYPE DEVICE SIZE/OFF   NODE NAME
badlog.py 594 admin    3w   REG  259,1    24380 265802 /var/log/bad.log
```
- As you can see above it shows the process ID 594 which is the active process running in the background that is filling up the server. I killed the server below:
```
admin@ip-10-1-12-200:~$ kill -9 594

```
- Tested to see if the process is still running:
```
admin@ip-10-1-12-200:~$ /home/admin/agent/check.sh
OKadmin@ip-10-1-12-200:~$ ^C
admin@ip-10-1-12-200:~$
````

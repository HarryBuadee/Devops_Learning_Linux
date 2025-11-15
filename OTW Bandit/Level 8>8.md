# Bandit Level 8 → Level 9
## Level Goal

The password for the next level is stored in the file data.txt and is the only line of text that occurs only once

Actions taken:

```bash
bandit8@bandit:~$ cat data.txt
eEAA4ytk957MspwYKLeOgooPzJKOg8jY
VVamYLR8vQaPhZV8sFPh7NVrqt3cwx5E
q9C0UQZ52GznEieTtXOgPrVvIvB60jxL
1kopVbuefPoyJ5GDXH0q46SXQVQQZmge
HeSAR9opVOfF0r39s92ig6Pu9EOeVwhF
6WLU0f8RPUW6O9z6rdXb2wHufXmbYn8f
9bFDdDjS8i613oA6Gv5Gv9tyIm6giwie

bandit8@bandit:~$ sort data.txt | uniq -u
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM


```

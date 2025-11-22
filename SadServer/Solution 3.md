
# Solution: "The Command Line Murders"

Goals:
- Going through hints find clue into who the murderer is.
- Validating and verifying that it's the actual murderer.

Actions taken:

- Checked out the mystery directoy.
````
admin@ip-10-1-12-119:~/clmystery$ cd mystery/
admin@ip-10-1-12-119:~/clmystery/mystery$ ls
crimescene  interviews  memberships  people  streets  vehicles
````

- Investigating to identify the perpetrator. I’ve uncovered some clues.
````
admin@ip-10-1-12-119:~/clmystery/mystery$ cat crimescene | grep "CLUE"
CLUE: Footage from an ATM security camera is blurry but shows that the perpetrator is a tall male, at least 6'.
CLUE: Found a wallet believed to belong to the killer: no ID, just loose change, and membership cards for Rotary_Club, Delta SkyMiles, the local library, and the Museum of Bash History. The cards are totally untraceable and have no name, for some reason.
CLUE: Questioned the barista at the local coffee shop. He said a woman left right before they heard the shots. The name on her latte was Annabel, she had blond spiky hair and a New Zealand accent.
````
- Reviewed all the hints from 1 to 8. This will help me identify the murderer.
````
admin@ip-10-1-12-119:~/clmystery$ cat hint1
Try poking around what's in a file by using the 'head' command:

  head -n 20 people

This will show you the first 20 lines of the 'people' file.
admin@ip-10-1-12-119:~/clmystery$ cd mystery/
admin@ip-10-1-12-119:~/clmystery/mystery$ cat ../hint2
Try using grep to search for the clues in the crimescene file:

        grep "CLUE" crimescene
admin@ip-10-1-12-119:~/clmystery/mystery$ cat ../hint3
In order to track down our potential witness, we need to figure out where she lives.

Try using 'head' on some of the files like 'people' and 'vehicles' and see where we might find that.
admin@ip-10-1-12-119:~/clmystery/mystery$ cat ../hint4
To find all the Annabels' addresses, use the 'people' file:

        grep "Annabel" people

Notice that not all of the results are worth investigating.  Remember what we know about Annabel.
admin@ip-10-1-12-119:~/clmystery/mystery$ cat ../hint5
"Interview" the two possible witnesses by reading the correct line from the streets they live on:

        head -n 173 streets/Mattapan_Street | tail -n 1

This will give you just line 173 of Mattapan street, because it will take first 173 lines, and then take
the last line from those.
admin@ip-10-1-12-119:~/clmystery/mystery$ cat ../hint6
To find a matching license plate, or a matching car, you can use grep on the 'vehicles' file:

        grep "Honda" vehicles

        grep "Blue" vehicles

        grep "L337" vehicles

This doesn't give us anything useful - why not? Try using 'head' on the file to investigate its structure.
admin@ip-10-1-12-119:~/clmystery/mystery$ cat ../hint7
In order to actually get information about vehicles that might match our description,
we need to get multiple lines AROUND each match.  We can use the -A, -B, or -C option with grep:

        grep -A 5 "L337" mystery/vehicles

This will match the license plates that contain "L337" and, for each match, show us the five lines AFTER it.
admin@ip-10-1-12-119:~/clmystery/mystery$ cat ../hint8
To see who was a member of several different groups, you can combine their membership lists into one and search against that.

        cat Fitness_Galaxy AAA United_MileagePlus | grep "John Smith"

If you only want to see the number of matches, you can use grep's -c option (the c must be lowercase):

        cat Fitness_Galaxy AAA United_MileagePlus | grep -c "John Smith"

Or you can pipe the result to 'wc -l':

        cat Fitness_Galaxy AAA United_MileagePlus | grep "John Smith" | wc -l
admin@ip-10-1-12-119:~/clmystery/mystery$
````

- From the clue at the crime scene, I'm trying to find out who Annabel is because she is a witness.
````
admin@ip-10-1-12-119:~/clmystery/mystery$ cat people | grep "Annabel"
Annabel Sun     F       26      Hart Place, line 40
Oluwasegun Annabel      M       37      Mattapan Street, line 173
Annabel Church  F       38      Buckingham Place, line 179
Annabel Fuglsang        M       40      Haley Street, line 176
`````
- Checked the address for the two females named Annabel. I only checked for the females because from clue from the crimescene stated that the witness was a female.
`````
admin@ip-10-1-12-119:~/clmystery/mystery$ cat streets/Hart_Place | head -n 40 | tail -n 1
SEE INTERVIEW #47246024
admin@ip-10-1-12-119:~/clmystery/mystery$ cat streets/Buckingham_Place | head -n 179 | tail -n 1
SEE INTERVIEW #699607
`````
- Checked the interviews and discovered Annabel Church was the witness from the statement.
`````
admin@ip-10-1-12-119:~/clmystery/mystery$ cat interviews/interview-47246024
Ms. Sun has brown hair and is not from New Zealand.  Not the witness from the cafe.
admin@ip-10-1-12-119:~/clmystery/mystery$ cat interviews/interview-699607
Interviewed Ms. Church at 2:04 pm.  Witness stated that she did not see anyone she could identify as the shooter, that she ran away as soon as the shots were fired.

However, she reports seeing the car that fled the scene.  Describes it as a blue Honda, with a license plate that starts with "L337" and ends with "9"

`````
- From the witness statement I read, I searched for blue Hondas. With the start of the registration "L337" which I got from hint 7.
`````
admin@ip-10-1-13-85:~/clmystery/mystery$ grep -C4 "Honda" vehicles | grep -C4 "Blue" | grep -C4 "L337"
--
--
Weight: 214 lbs

License Plate L337QE9
Make: Honda
Color: Blue
Owner: Erika Owens
Height: 6'5"
--
--
--
Weight: 181 lbs

License Plate L337539
Make: Honda
Color: Blue
Owner: Aron Pilhofer
Height: 5'3"
--
--
--
Weight: 239 lbs

License Plate L337369
Make: Honda
Color: Blue
Owner: Heather Billings
Height: 5'2"
--
--
--
Weight: 137 lbs

License Plate L337DV9
Make: Honda
Color: Blue
Owner: Joe Germuska
Height: 6'2"
--
--
--
Weight: 176 lbs

License Plate L3375A9
Make: Honda
Color: Blue
Owner: Jeremy Bowers
Height: 6'1"
--
--
--
Weight: 224 lbs

License Plate L337WR9
Make: Honda
Color: Blue
Owner: Jacqui Maher
Height: 6'2"


`````
- Verifying whether Joe Germuska belongs to the AAA, Delta SkyMiles, Museum of Bash History, Rotary Club, and Terminal City. It turns out he is affiliated with all of them.
``````
admin@ip-10-1-13-85:~/clmystery/mystery$ grep "Joe Germuska" memberships/*
memberships/AAA:Joe Germuska
memberships/Delta_SkyMiles:Joe Germuska
memberships/Museum_of_Bash_History:Joe Germuska
memberships/Rotary_Club:Joe Germuska
memberships/Terminal_City_Library:Joe Germuska
admin@ip-10-1-13-85:~/clmystery/mystery$

``````
- Verifying the Joe Germuska is the muderer.
``````
admin@ip-10-1-13-85:~/clmystery/mystery$ cd
admin@ip-10-1-13-85:~$ ls
agent  clmystery  mysolution
admin@ip-10-1-13-85:~$ echo "Joe Germuska" > mysolution 
admin@ip-10-1-13-85:~$ md5sum ~/mysolution 
9bba101c7369f49ca890ea96aa242dd5  /home/admin/mysolution
admin@ip-10-1-13-85:~$
``````


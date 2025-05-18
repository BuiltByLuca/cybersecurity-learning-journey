# Useful Resources

To-To: intro for this file xD

## OverTheWire Bandit

Here I will Save notes for the [OverTheWire Bandit](https://overthewire.org/wargames/bandit/) Game. The time indication behind each level is how long it took me to complete each level (not precise)

### Level 0 🕑10min

``` Python
#OTW SSH Login:
ssh bandit0@bandit.labs.overthewire.org -p 2220

#Password:
bandit0
```

### Level 0 → Level 1 🕑15min

``` Python
#Make sure you're in bandit0 dir
ls

#A file named "readme" should appear
cat readme

#File should open and reveal password
ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If
```

Now log out of ssh with "exit", and log back in with ssh, but change the account name to bandit1.

### Level 1 → Level 2 🕑15min

```Python
#login with bandit1
#ls to find "-" file
ls

# open file with cat
cat ./-

#File should open and reveal password
263JGJPfgU6LtdEvgfWU1XP5yac29mFx
```

**Explanation:**

- ```cat``` for opening files.
- the "." is there to indicate the current directory.
- the "/" is there to search within the current directory.
- the "-" is the filename.

### Level 2 → Level 3 🕑2min

```Python
#Login with bandit2
#Same procedure as before, just use "" around filenamme
cat ./"spaces in this filename"

#File should open and reveal password
MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
```

(I didn't do any research, i just guessed "" and it worked. might not always work in the future)

### Level 3 → Level 4 🕑2min

```Python
#Login with Bandit3
cd inhere

#Use ls -a to list all files
ls -a
#.  ..  ...Hiding-From-You

cat ./...Hiding-From-You

#File should open and reveal password
2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ
```

I am a little confused about the ```".  ..  "``` before the actual file name, but in Ubuntu those dots we colored blue and so I just left them out of the file name while opening it, and it worked just fine.

### Level 4 → Level 5 🕑15m

```Python
#Bandit 4
cd Inhere

#ls gives a bunch of files "-file00, -file01.. -file09"

bandit4@bandit:~/inhere$ file ./-file*
>./-file00: PGP Secret Sub-key -
>./-file01: data
>./-file02: data
>./-file03: data
>./-file04: data
>./-file05: data
>./-file06: data
>./-file07: ASCII text
>./-file08: data
>./-file09: data

#Took me a bit, but file 7 only has ASCII text, thats why is says that.

Cat ./-file07

#File should open and reveal password
4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
```

### Level 5 → Level 6 🕑35min

``` Python
#Bandit5
find -size 1033c
> ./maybehere07/.file2

cat ./maybehere07/.file2

#File should open and reveal password
HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
```

The Search parameters for the "find" command threw me on a whirl. I still don't really understand them tbh. (I mean i do get -size 1033c)

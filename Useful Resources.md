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

### Level 6 → Level 7 🕑35min (Day 2)

This one took a bit of thinking. The password is stored *somewhere on the system* but I didn't at first think to just.. search the entire system with:

```Python
find -user bandit7 -group bandit6 -size 33c
```

For some reason I had thought it would be smarted to look in the folder that contains all the games.. because why would it not be in the folder where all the games are in?.. Limited thinking i guess xD

In any way, I found the file by going into the main directory of the server.. so "cd .." as much as it let me, and then run the command again. This time it gave me a big big list of files that match the criteria. But, every single file but 1 was "Permission Denied". that file was ```./var/lib/dpkg/info/bandit7.password``` which that file name seems fitting :)

```Python
#Bandit6
#File should open and reveal password
morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj
```

finding the file outside of the "game environment" was something that I really didn't expect.

### Level 7 → Level 8 🕑3min

This one was quicker than I thought. relatively straight forwards.

```Python
#Bandit7

grep -G millionth data.txt

#File should open and reveal password
dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
```

### Level 8 → Level 9 🕑40min

This one also took me quite some time.

sort makes sure to sort the entire file aplhabetically, meaning duplicate passwords will be next to another.
uniq is only able find unique things with -u if the duplicates are next to another.
meaning uniq -u **will** find 0 to be unique in:
"0 1 1 1 3 3" but it **will not** find 0 in: "0 1 3 1 3 1" here it will output everything, since no adjacent results are duplicates

```Python
#Bandit8
sort data.txt | uniq -u
#File should open and reveal password
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
```

(cat data.txt | sort | uniq -u) would also do the same ting btw

### Level 9 → Level 10 🕑 30min

I used something that I am not sure if it was correct... but it worked?
While it did work, I do have to mention that this would not work in large scale, huge files because it has a manual aspect to it.

```Python
#Bandit9
xxd data.txt
#I looked through the result, and there was one that was very clearly maked by the mentioned "=" symbol:
![Bandit9Password](image.png)

#Copied password:
FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
```

I feel a bit cheesy about doing it this way, so I am going to spend some extra time to figure out if i can get a more clean result. This took 10 minutes so far.

```Python
strings data.txt
#Outputs all human readable character strings longer than 3 characters.

strings data.txt | grep ==
#Searches for "==" within the output strings.

>========== the
>========== password{k
>=========== is
>========== FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
#This is the new output, which is far more desirable.
```

### Level 10 → Level 11 🕑 45 seconds

```Python
#Bandit10 🎉
base64 -d data.txt

>The password is dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
```

that was.. easy lol

### Level 11 → Level 12 🕑 15min

I really had no clue how to go about this one, so I looked it up. not proud of it but honestly I dont quite know how i woul've figured that out by myself.

```Python
#Bandit11
#ROT13 Translation
cat data.txt | tr A-Za-z N-ZA-Mn-za-m
The password is 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
```

After a few more minutes of reading up on it and asking chatgpt to explain it to me in more detail, I understand it now. Will i be able to repeat it flawlessly next time without needing to look back at my notes 🤔 no. xD

### Level 12 → Level 13 🕑35min

Wow. I feel like I just got thrown under the bus. This one is WAY harder than the other ones. I looked up a [Tutorial](https://github.com/leegengyu/OverTheWire-Bandit) on how to do it. NO WAY I could have figured all of that out on my own. Not even close. This is a crazy jump imo.

```Python
#Bandit12
mktemp -d #make a temp dir to work in
cp data.txt /tmp/tmp."FOLDER THAT WAS MADE"
cd "Folder" 
file data.txt #Shows it gets seen as ASCII but is a hexdump
ccd -r data.txt > hexdata.txt #make new file that doesn't get seen as ascii like the one before
file hexdata.txt #now show's gzip compressed
mv hexdata.txt hexdata.tar.gz #convert into actually gzip compressed because for some reason it wasnt before.. so the gunzip couldnt read it
gunzip hexdata.tar.gz
file hexdata.tar #Now show's the file is bzip2 compressed.

#From here on out, its just back and forth compression.

Mv hexdata.tar hexdata.bz2
bunzip2 hexdata.bz2
file hexdata #Now gzip compressed
mv hexdata hexdata.tar.gz
gunzip hexdata.tar.gz
file hexdata #Now POSIX compressed
tar -xf hexdata.tar #Makes data5.bin file (POSIX)
tar -xf data5.bin #Makes data6
tar -xf data6.bin #Makes data8
file data8.bin #Now gzip compressed
mv data8.bin data8.tar.gz
gunzip data8.tar.gz
file data8.tar #FINALLY ASCII

cat data8.tar

#File should open and reveal password
The password is FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn
```

HOLY SHIT THAT WASNT EVEN CLOSE TO AS EASY AS THE LAST ONE! EVEN WITH A TUTORIAL.. at least i know what was going on and what I was donig.. just figuring the commands out by myself would have taken days i feel like.

### Level 13 → Level 14 🕑15min

```Python
#Bandit13

ssh -i sshkey.private bandit14@localhost -p 2220 # -I is to read key from file.
# Now we are logged into Bandit14's acc.

cd /etc/bandit_pass/ | cat bandit14

#File should open and reveal password
MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS
```

### Level 14 → Level 15 🕑25min

```Python
#Bandit14
Telnet localhost 30000
MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS

#Should open and reveal password
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
```

at this point i find that it is incredibly difficult to actually just do these tasks without looking at an external resource to figure it out.. most of this just doesn't make sense to me at first.

### Level 15 → Level 16 🕑15min

```Python
#Bandit15

openssl s_client localhost:30001
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo

#Should open and reveal password
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
```

### Level 16 → Level 17 🕑35min

```Python
#Bandit16
nmap localhost -p31000-32000;
=============================
PORT      STATE SERVICE
31046/tcp open  unknown
31518/tcp open  unknown
31691/tcp open  unknown
31790/tcp open  unknown
31960/tcp open  unknown
=============================

nmap --script ssl-enum-ciphers -p 31000-32000 localhost

#Port 31518
#Port 31790
#Have TLS

# Here is where I just completly lost the plot. I didn't really know where to go from here. So I got the code from the website below.


cat /etc/bandit_pass/bandit16 | openssl s_client -ign_eof -connect localhost:31790 -quiet

#copy rsa key

cd /tmp/
cat > key.private
#Past Rsa Key
#Ctrl+C I think? im kida confused what happened here.. did it take it from my clipboard or did I paste it into the file?
chmod 600 key.private
ssh -i key.private bandit17@localhost -p 2220

cat /etc/bandit_pass/bandit17

#File should open and reveal password
EReVavePLFHtFlFsjn3hyzMlvSuSAcRD
```

[Website](https://wceastwood01.medium.com/overthewire-bandit-3e182800360c).. That was enough for today.

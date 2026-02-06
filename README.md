OVERTHEWIRE 
------
Level 1

The only file in this level was found using ls
cat readme gave me the password.

-----
Level 2 

This had to do with a file named -
This was the first time i encountered this kind of file so i had to look it up, i ended up using the command ./-    This allowed me to open the file and give me the password.
I had also tried usng cat - which didnt work.

-----
Level 3

used ls to see all files and what appeared was --spaces in this file--
The chalange was opening this files with the strange spaces in the name
cat didnt work, ./--spaces in this filename-- didnt work because kali thought i was trying to enter a command becxause of the --
I learned about putting this kind of file name in "", so the solution was cat ./"--spaces in this filename--".

-----
level 4

'ls' showed 'inhere' so i tried to open it and it came up as a directory, so i used 'cd inhere' and used 'ls' again to show the files, there were -files 00 through 09
Im sure was a better was but i resorted to using "cat ./"-file00" " on every file until i found the password.

-----
level 5

Again the directory inhere was present.
'cd inhere' -> 'ls' this resulted in 15 over directories "maybehere"
i opened a few of the directories to see what was inside, there was 5 files in each one.
i knew that going through every file one by one was taking too long and there should be a way for me to find excatly what i was looking for.
The site for overthewire gave me the size of the file, 1033 bytes so i needed to use the correct 'find' command
I found that using '-size 1033c' could search for the file i needed, bu i still needed it to search the entire inhere directory.
'find ~/inhere/ -size 1033c' gave me the file .file2 in maybehere07 which gave me the password.

-----
level 6

logged in and 'ls' 'cd' didnt come up with anything, so i used 'ls -la' that i learned from a peer.
This showed a table of files along with the permissions, ".bash_logout" ".basgrc" ".profile" all has a lot of information but not sure if its relevant yet.
There were 2 files that were named "." and ".."
i used 'file . / ..' and they are directories
i used 'cd ..' and got into the home directory, this has many other directories so i have to find a saw to comb through them all.
The information the site gives me is 33 bytes, owned by user bandit7, and owned by group bandit6.
I need to an 'find' command that can use all this information.
I used 'find -user bandit7 -group bandit6 -size 33c' which led me to the file "./bandit5/inhere".
'cd bandit5' found the directory "inhere" but cant get in, permission denied.
I learned about how to use the 'find' command when having more perameters, in this case i needed to find, user, group, file size, and text so 'find \ -user bandit7 -group bandit6 -size 33c -exec grep -a . {} \;' worked to find the password.
-exec is used to find anfile i can access

-----
level 7

the only file is data.txt and it is a lot of words or names and codes next to them, i think i have to find a certain word and get the password that way. 

-----
level 9

The only file in here is data.txt again, The site tells me there is only a few readable lines in here, i have to filter out the rest. The 'string' command has a '-a' parameter that would search the whole find for readable text, this gave me the password.
<img width="1652" height="1092" alt="image" src="https://github.com/user-attachments/assets/d14c0c85-ceb3-4bc5-83a0-06fe4798dc52" />

-----
level 10

The sites tells me that the information in data.txt and is encoded with base64. Ive used base64 in PicoCTF befire so i know the command is 'base64 -d data.txt' this gave me the password.
<img width="844" height="434" alt="Screenshot 2026-02-06 at 8 17 22 AM" src="https://github.com/user-attachments/assets/87562272-8330-4232-bf09-842bc528515f" />

-----
level 11

Another base64 encoded, this time the text has been rotated 13 positions, maybe this time its a combination of base64 and another command.

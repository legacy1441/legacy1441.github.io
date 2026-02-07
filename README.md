OVERTHEWIRE 
------
Level 1 

The only file in this level was found using 'ls'. 'cat readme' gave me the password, this one was easy due to prior knowledge.

<img width="816" height="223" alt="Screenshot 2026-02-06 at 6 27 36 PM" src="https://github.com/user-attachments/assets/0392c6bc-e672-4c34-8de5-91e4980acfae" />

-----
Level 2 

This had to do with a file named "-". This was the first time i encountered this kind of file so i had to look it up, i ended up using the command "./-"    This allowed me to open the file and give me the password. I had also tried usng 'cat -' which didnt work.

<img width="830" height="144" alt="Screenshot 2026-02-06 at 6 30 10 PM" src="https://github.com/user-attachments/assets/120179fe-ddf5-4f35-9224-5bdc9070f4dc" />

-----
Level 3

used 'ls' to see all files and what appeared was "--spaces in this file--". The chalange was opening this files with the strange spaces in the name. 'cat' didnt work, './--spaces in this filename--' didnt work because kali thought i was trying to enter a command becxause of the --. I learned about putting this kind of file name in "", so the solution was cat ./"--spaces in this filename--".

<img width="827" height="152" alt="Screenshot 2026-02-06 at 6 34 09 PM" src="https://github.com/user-attachments/assets/023c1510-ae6e-48cd-b712-317a0deee2cf" />

-----
level 4

'ls' showed 'inhere' so i tried to open it and it came up as a directory, so i used 'cd inhere' and used 'ls' again to show the files, there were -files 00 through 09
Im sure was a better was but i resorted to using "cat ./"-file00" " on every file until i found the password.

<img width="843" height="202" alt="Screenshot 2026-02-06 at 6 47 17 PM" src="https://github.com/user-attachments/assets/96d3f2da-0c52-4814-b613-76208acfbe4b" />

-----
level 5

Again the directory inhere was present. 'cd inhere' -> 'ls' this resulted in 15 over directories "maybehere". i opened a few of the directories to see what was inside, there was 5 files in each one. i knew that going through every file one by one was taking too long and there should be a way for me to find excatly what i was looking for. The site for overthewire gave me the size of the file, 1033 bytes so i needed to use the correct 'find' command. I found that using '-size 1033c' could search for the file i needed, bu i still needed it to search the entire inhere directory. 'find ~/inhere/ -size 1033c' gave me the file .file2 in maybehere07 which gave me the password. The solution was 'cat ./maybehere07/.fil2'. (when i went back to get a ss i could not for the life of me remember the solution)

<img width="827" height="561" alt="Screenshot 2026-02-06 at 6 57 12 PM" src="https://github.com/user-attachments/assets/d4148655-f743-47a7-8879-3a3a5a2fd23f" />

-----
level 6

logged in and 'ls' 'cd' didnt come up with anything, so i used 'ls -la' that i learned from a peer. This showed a table of files along with the permissions, ".bash_logout" ".basgrc" ".profile" all has a lot of information but not sure if its relevant yet. There were 2 files that were named "." and "..". i used 'file . / ..' and they are directories. i used 'cd ..' and got into the home directory, this has many other directories so i have to find a way to comb through them all. The information the site gives me is 33 bytes, owned by user bandit7, and owned by group bandit6. I need to an 'find' command that can use all this information. I used 'find -user bandit7 -group bandit6 -size 33c' which led me to the file "./bandit5/inhere". 'cd bandit5' found the directory "inhere" but cant get in, permission denied. I learned about how to use the 'find' command when having more perameters, in this case i needed to find, user, group, file size, and text so 'find / -user bandit7 -group bandit6 -size 33c -exec grep -a . {} \;' worked to find the password. -exec is used to find a file i can access

<img width="1648" height="1825" alt="image" src="https://github.com/user-attachments/assets/fe680015-a404-4077-bf14-827dcb8a9cf6" />

<img width="821" height="918" alt="Screenshot 2026-02-06 at 7 09 03 PM" src="https://github.com/user-attachments/assets/2a052f01-16c7-4ff3-bc3b-248091873773" />

-----
level 7

the only file is data.txt and it is a lot of words or names and codes next to them, i think i have to find a certain word and get the password that way. In this one i had to use 'grep millionth data.txt" to search the file for that word.

<img width="834" height="248" alt="Screenshot 2026-02-06 at 7 13 32 PM" src="https://github.com/user-attachments/assets/81775f70-4c12-42ae-b8d7-0f7ff0c1b0f3" />

-----
level 8

This level only had one file, seems i have to search for the only unique line in this file. 'uniq -u data.txt' didnt work, 'sort -u data.txt' didnt work, i thought they would show me unique lines and they did, just one instance of repeating lines. 'sort data.txt | uniq -u' turns out i needed a bit of both to get the password, 'sort data.txt' to sort the file, 'uniq' to sort the file in uniq lines only.

<img width="850" height="457" alt="Screenshot 2026-02-06 at 7 39 28 PM" src="https://github.com/user-attachments/assets/c6cfb8c0-120d-4f51-a8ee-4d561996747f" />

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

Another base64 encoded, this time the text has been rotated 13 positions, maybe this time its a combination of base64 and another command. I learned that when the letters are shifted in a constant manner, stated by the site, then this means its using rot13. I have to use 'tr' to get the password. 'cat filename | tr 'A-Za-z' 'N-ZA-Mn-za-m' ' worked to get the password, 'cat' to open the file, then 'tr' and the letters mean that all the upper and lowercase has to be used, the second part is low much to shift the letter back.

<img width="1685" height="772" alt="image" src="https://github.com/user-attachments/assets/00ac8046-4a1c-4198-aabc-531fefa9786d" />

-----
Level 12

The next data.txt is a hexdump so must have to use xxd or some other new command. When i open the file there is plain text that says "data.2bin" bin files has to do with archives, i have to find out what kind of file this is exactly. Im looking though the 'file --help' to see if it has anything useful. Used 'file -v data.txt' to see what kind of file this is and came back as a magic file. Magic files can be used to hide other files in them, i have to find out how to see the "magic number". Also "file-5.45" came up but it seems that it has nothing to do with this puzzle, ignore.

<img width="1124" height="197" alt="image" src="https://github.com/user-attachments/assets/f27311ca-b115-406a-b616-51735591bf03" />

The site tells me that this file is compressed, not sure how i would figure that out on my own, tried using 'tar' on this file but when looking through the '--help' it seems this is used more to create archives, ill try 'gzip'. 'gzip -l dat.txt' to list compressed files, nada. 'gzip -N data.txt' to get og name of file, nada. After some google, seems i have to convert this file from hexdumb, to binary, then extract the info using tar, gzip, or another like that. Everything i try doesnt work, the site does say to copy this file into a new directory made by me, ima try that. I dont have permission to make my own directory so ive found out about '/tmp' being a temporary directory i cab work with. 'cd /tmp' 'mkdir 12_work' 'cd 12_work' this is how i made my own temp directory. Now to copy that file into my own.

<img width="819" height="511" alt="Screenshot 2026-02-06 at 7 53 53 PM" src="https://github.com/user-attachments/assets/a7fe3314-5a1d-4c43-96db-6551cc69d1a7" />

Learned about 'cp' this command can copy files into other directories. After a lot of trial and error 'cp ~/data.txt /tmp/12_work' this is run from the main directory where the file is located, and moved to my own, then i 'cd' back to my dir.

<img width="785" height="122" alt="Screenshot 2026-02-06 at 7 57 35 PM" src="https://github.com/user-attachments/assets/ad2aded2-f68d-4ac1-833f-89cc4e5d1182" />

The file is a hexdump, ive learned (through google) that i have to reverse this back into readable data. 'xxd -r data.txt' turned it into raw bytes, 'file data.txt' says "gzip compressed data'. After a lot of trial and error i used 'mv data.txt data.gz' bc it has to be a .gz file for it to work. 'gzip -d data.gz' tuened it into a tar file. there is a .bin file inside. 

<img width="840" height="958" alt="Screenshot 2026-02-06 at 8 21 24 PM" src="https://github.com/user-attachments/assets/7ddca6f2-90b1-471c-9b5b-0816045254d4" />

The hex file had a tar file inside, that file had another inside of it, each was compressed with either bzip2 or gzip found by 'file' command. gzip needed the file to be .gz, to see and extract tar 'tar -tf <file>' 'tar -xf <file>' and in the end its a ASCII file and readble.

<img width="846" height="1050" alt="Screenshot 2026-02-06 at 8 35 34 PM" src="https://github.com/user-attachments/assets/b937a441-45a8-4bc0-9ffb-2ab8c668bd80" />

-----
level 13 (Hell on linux)

For this level i wont get a password, ill get a private SSH key to login to next level. I have to use the ssh command from previous levels to get me into this one. 

<img width="839" height="1050" alt="Screenshot 2026-02-06 at 8 42 23 PM" src="https://github.com/user-attachments/assets/d18311c1-a359-477f-8721-91979cf7ed47" />

While researching the 'ssh' command, i learned that you can make it read a file as authentication, that is where the file "sshkey.private" comes in. I also have to connect like i do the other levels only using this file. "ssh -i ssjkey.private -p 2220 bandit14@bandit.labs.overthewire.org" is the command that make shh read the file and the site where im trying to connect. 

<img width="823" height="926" alt="Screenshot 2026-02-06 at 9 40 04 PM" src="https://github.com/user-attachments/assets/98a49a89-ebea-45cc-9e2d-2d21af655e1c" />

I tried everything, every permiation of this darn command, nothing worked, it would keep me in bandit13. The site talks about 'chmod' command, this is to change the read-write permissions on a file. I did 'chmod 600 sshkey.private' and it wouldnt let me change it bc bandit13 isnt the owner of the file. then i noticed when i tried to connect to bandit14 it would say that the localhost was blocked, then it dawned on me, i dont connect to bandit from within bandit, i do it from the kali host.

<img width="820" height="952" alt="Screenshot 2026-02-06 at 9 40 38 PM" src="https://github.com/user-attachments/assets/e8631747-43c9-4373-8012-ce7bd5ef8817" />

But i needed to download the file onto my host (kali), i used the command 'scp -P 2220 bandit13@bandit.labs.overthewire.org:~/sshkey.private .' to get the ssh file onto my kali. I then used the ssh command again to connect, bandit told me that the file needs to be unaccessable to others, this is where i used the 'chmod' to change permissions then "ssh -i ssjkey.private -p 2220 bandit14@bandit.labs.overthewire.org" worked and i got in.

<img width="829" height="947" alt="Screenshot 2026-02-06 at 9 39 33 PM" src="https://github.com/user-attachments/assets/e96533e5-cf5b-4042-b1b0-a1b710b666ce" />

<img width="828" height="949" alt="Screenshot 2026-02-06 at 9 40 45 PM" src="https://github.com/user-attachments/assets/4290ab8f-4ae9-4fa9-b19b-db504b4312c3" />
















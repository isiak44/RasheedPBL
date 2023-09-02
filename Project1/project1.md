# Project 1 Linux Practice Project

In this page we will explore some basic Linux commands with a preview of how I run each commands step by steps.
---

### 1. Sudo Command:

Sudo which also means superuser allows me to perform task that requires administrative or root permission. 

`sudo apt upgrade`

This command simply upgrades packages that need to be upgraded. 

<img width="965" alt="sudo apt upgrade" src="https://github.com/isiak44/Rasheed_Devops/assets/27869977/e3db044b-efc7-425f-ae2f-bc0fd7672886">

---

### 2. Pwd Command:

`pwd`

The pwd tells shows that I am in the /home/ray directory 

<img width="905" alt="pwd" src="https://github.com/isiak44/Rasheed_Devops/assets/27869977/d7ace3d6-9f23-41b7-a0d0-6b59c41b3aa8">

---

### 3. cd Command:

`cd | cd.. | cd ~ | cd -`

The cd command helps to navigate through folders and files. 
`cd` naturally takes you to home, `cd ..` take you one step backward through folders, `cd ~username` goes to another user home while `cd -` moves to the previous folder. 

<img width="905" alt="ls" src="https://github.com/isiak44/Rasheed_Devops/assets/27869977/ec3b649b-c321-4121-889e-82780adb1c0e">

---

### 4. Ls Command:

`ls`

ls command shows the current working directory content like files and folders.  `ls -a` shows hidden files, 

<img width="958" alt="ls-a" src="https://github.com/isiak44/Rasheed_Devops/assets/27869977/30a82ce2-0120-4119-a5e6-13b51407926f">

`ls -lh` shows file sizes in easily readable format such as MB, GB, TB. 

<img width="958" alt="ls-lh" src="https://github.com/isiak44/Rasheed_Devops/assets/27869977/1b5b4dfe-8a5e-41a0-ab15-a4a083a6c7d5">

`ls -R` list all the files in the subdirectories.

<img width="958" alt="ls-R" src="https://github.com/isiak44/Rasheed_Devops/assets/27869977/9b5ad674-75d8-494c-bb5b-78f5a7cc85a6">

---

### 5. cat Command:

`cat /home/ray/Devops`

The cat command which is also known as concatenate is used to read a file, multiple files together and even files between folders, here I am reading a file named Devops as shown below. 

<img width="868" alt="cat" src="https://github.com/isiak44/Rasheed_Devops/assets/27869977/c143dc0c-dc10-48b5-be00-f39c6f47033f">

---

### 6. cp Command:

`cp Devops /home/ray/Devops_Folder` 

This command basically means copying Devops file to Devops_Folder

<img width="950" alt="cp" src="https://github.com/isiak44/Rasheed_Devops/assets/27869977/4344d09d-f6ee-4ebe-b9c5-6e99c077e0bd">
---

`cp Devops Devops_New2` 

Here we make a duplicate of Devops as Devops_New2

<img width="960" alt="cp2" src="https://github.com/isiak44/Rasheed_Devops/assets/27869977/6e63ab85-6288-4e48-b8e8-e913dda62e41">
---

`cp -R /home/ray/Downloads/Devops_Folder/ /home/ray/Documents/`

With the -R we are able to copy Devops_Folder which is inside the Downloads directory to a new Directory `Documents` 

<img width="960" alt="cp-r" src="https://github.com/isiak44/Rasheed_Devops/assets/27869977/0ec8c8ef-a0a1-4720-bab0-a4d2371f158e">

### 7. mv Command:

`mv Devops /home/ray/Documents`

Here we use the mv command to move Devops file to Documents 

<img width="963" alt="mv" src="https://github.com/isiak44/Rasheed_Devops/assets/27869977/9cb356a5-4c38-4db3-9f44-4fa6d7e8f454">

---

### 8. mkdir Command:

`mkdir Devops_Folder | mkdir /home/ray/Documents/Devops_Folder/Inside_Folder`

`mkdir` simply helps to create a new folder Devops_Folder or multiple folders at once. 

<img width="1159" alt="mkdir copy" src="https://github.com/isiak44/Rasheed_Devops/assets/27869977/a3f79f82-68f4-4bff-8b7e-77fa5a2fdcf3">

---

### 9. rmdir  Command:

`rmdir /home/ray/Documents/Project1/Devops_Folder`

The `rmdir` basically remove empty directories 

<img width="1159" alt="rmdir" src="https://github.com/isiak44/Rasheed_Devops/assets/27869977/254ccba4-f288-4048-baea-a7cb28903129">

---

### 10. rm Command:

`rm -i Devops | rm -r /home/ray/Documents/Devops`

The `rm` remove files from directories `rm -i` promt system confirmation before deleting while the `rm -r` delete files and directories recursively. 

<img width="1159" alt="rm" src="https://github.com/isiak44/Rasheed_Devops/assets/27869977/786e8dde-0a80-4a4d-a41d-caaed20f772c">
---

### 11. touch Command:

`touch index.html`

We use the `touch` command to create an empty file `index.html`

<img width="1159" alt="touch" src="https://github.com/isiak44/Rasheed_Devops/assets/27869977/62445a6c-0487-487a-8b79-c13e46359736">

---
### 12. locate Command:

`locate -i Devops`

The locate command finds files in the system database, the `-i` turns of search case sensitivity. 

<img width="1159" alt="locate" src="https://github.com/isiak44/Rasheed_Devops/assets/27869977/398d8865-f3a5-4051-abc6-414dd2d880f5">

---
### 13. find Command:

`find /home -name Devops`

here we use find command to search files withing a specific directory.

<img width="1159" alt="find" src="https://github.com/isiak44/Rasheed_Devops/assets/27869977/1cacc9d7-55a4-4274-8077-d5d206bddb5c">

---
### 14. grep Command:

`grep pwd /home/ray/Documents/Devops_Folder/Devops`

The `grep` commands help to search for words in a file and here we search for the word `pwd` in Devops file 

<img width="1159" alt="grep" src="https://github.com/isiak44/Rasheed_Devops/assets/27869977/0073de5d-2137-4d0a-870f-91e8df74193a">

---
### 15. df Command:

`df -h`

df command simply reports the system or current directory disk usage `-h` flag prints this information in human readable format as shown below. 

<img width="1159" alt="df-h" src="https://github.com/isiak44/Rasheed_Devops/assets/27869977/67869384-b5d6-4aa3-a6a8-67a19695c28f">

---
### 16. du Command:

`du Documents`

This command checks how much space a file or directory takes up and it is important to specify the directory path when using du command.

<img width="1159" alt="du1" src="https://github.com/isiak44/Rasheed_Devops/assets/27869977/0da35a4a-00ac-478c-abab-b4ad65482063">

---
### 17. head Command:

`head -n 5 Devops`

The head command view the first 10 lines of a text, adding -n 5 view the first 5 lines of Devops file. 

<img width="1493" alt="head-n " src="https://github.com/isiak44/Rasheed_Devops/assets/27869977/1f50b083-73d8-4695-8a61-2338b329b5c2">

---
### 18. tail Command:

`tail -n 5 Devops`

Meanwhile, the tail command views the last 10 lines of a text, -n 5 also views the last 5 lines of Devops file as shown below. 

<img width="1149" alt="tail-n" src="https://github.com/isiak44/Rasheed_Devops/assets/27869977/8c06e5bd-2434-4386-bdcd-9b7598f46731">

---
### 19. diff Command:

`diff Devops Devops_New`

This command analyzes and compares two different files line by line as we did with Devops and Devops_New.

<img width="1149" alt="Diff" src="https://github.com/isiak44/Rasheed_Devops/assets/27869977/9d43ac71-0a0f-4565-a2c2-7276df6d1baa">

`diff -c Devops Devops_New`

<img width="1149" alt="diff-c" src="https://github.com/isiak44/Rasheed_Devops/assets/27869977/2edcdd04-e28b-466d-aae5-8ea315accd29">

---
### 20. tar Command:

`tar -cvf newachive.tar /home/ray/`

`tar`  command simply archive multiple files into tar file. 

> tar header

<img width="1450" alt="tarhead" src="https://github.com/isiak44/Rasheed_Devops/assets/27869977/8e8c0a03-d241-4ca1-8ffb-a48595888f2c">

> tar tail

<img width="1450" alt="tartail" src="https://github.com/isiak44/Rasheed_Devops/assets/27869977/66e6b9cc-9471-4346-83c0-ac356ca2c7e7">

---
### 21. chmod Command:

`chmod 777 Devops`

This command change a directory or file read, write and execute permission, In this case we allow all user class "Owner, group member and others" to read, write and execute `Devops` file with the numeric number 777 as shown below. 

<img width="1513" alt="chmod" src="https://github.com/isiak44/Rasheed_Devops/assets/27869977/d840f19c-e552-4a49-b6cb-a34318d234a6">

---
### 22. chown Command:

`sudo chown Rasheed project1.md`

This command simply change ownership of a file, directory or symbolic link to a specified username, and here we change the project1.md file owner to Rasheed. 

<img width="1266" alt="chown" src="https://github.com/isiak44/Rasheed_Devops/assets/27869977/d9e34f55-fb07-43ef-9d86-f41c2bbe1f9b">

---
### 23. jobs Command:

`jobs`



---
### 24. kill Command:

`kill`



---
### 25. ping Command:

`ping`

<img width="1725" alt="ping" src="https://github.com/isiak44/RasheedPBL/assets/27869977/0ea4647e-8d36-4368-ba90-7ffc530ba814">

---
### 26. wget Command:

`wget`



---
### 27. uname Command:

`uname`

prints detailed information about my Linux system and hardware. `-a` flat prints all the system information, `-s` prints the kernel name, while `-n` prints the node hostname. 

<img width="1723" alt="uname" src="https://github.com/isiak44/RasheedPBL/assets/27869977/4bc574a9-43e8-4d4f-a478-dca83796c852">

---
### 28. top Command:

`top`

This command displays all running processes and a dynamic real-time vew of the current system. It also identify and terminate a process that may use too many system resources. 

<img width="1173" alt="top" src="https://github.com/isiak44/Rasheed_Devops/assets/27869977/8c8200b8-9c2a-4452-9dba-de9dff16598d">

---
### 29. history Command:

`history`

simply list up to 500 previously executed commands, also allowing us to reuse them with re-entering. 

<img width="781" alt="history" src="https://github.com/isiak44/RasheedPBL/assets/27869977/ed1a6986-6a97-412c-9852-4caaa2c1f268">

---
### 30. man Command:

`man`

prints a user manual of any command or utilities you can run in the terminal, including the Name, Description and options. 

<img width="1066" alt="man ls" src="https://github.com/isiak44/RasheedPBL/assets/27869977/395ed476-505b-4a9a-ab48-292459bb7834">

---
### 31. echo Command:

`echo`

A built-in utility that displays a line of text or string using the standard output. 

<img width="1066" alt="echo" src="https://github.com/isiak44/RasheedPBL/assets/27869977/7d6a105d-7755-4fbb-b365-dab3cd3363fe">

---
### 32. zip, unzip Command:

`zip archive.zip project1.md`

The zip command can compress a file to a Zip file, also can archive a file and directory to reduce disk usage. 

<img width="856" alt="zip" src="https://github.com/isiak44/Rasheed_Devops/assets/27869977/663c7bd0-cccc-4643-8de6-f35fe2c1bb98">

`unzip achive.zip`

The unzip command unzip the zipped files from archive. 

<img width="781" alt="unzip" src="https://github.com/isiak44/Rasheed_Devops/assets/27869977/2805295f-4606-4615-bb24-589515bbe751">

---
### 33. hostname Command:

`hostname`

provides the system hostname, `-a` flag shows the hostname alias, `-A or --all-fqdns` shows the machine fully qualified domain name, `-i` shows the IP address as shown below

<img width="1661" alt="hostname" src="https://github.com/isiak44/RasheedPBL/assets/27869977/dcda9a36-dd6a-447a-92de-0cd2f5ce50c4">

---
### 34. userdel, useradd Command:

`useradd -m Rasheed`

Adds user "Rasheed" to the system.

<img width="1180" alt="useradd" src="https://github.com/isiak44/Rasheed_Devops/assets/27869977/c793f1ed-2ee5-49ae-a188-682eb997f44a">

`passwd`

Sets the password for user Rasheed

<img width="1173" alt="passwd" src="https://github.com/isiak44/RasheedPBL/assets/27869977/50cd88b2-c33c-4a53-a63c-fcbfeef38df8">

`userdel`

This command deletes user "Rasheed" from the system.

---
### 35. apt-get Command:

`sudo apt install vim `

A command-line tool for handling "Advance Package tool" Libraries in Linux. It manages, updates, remove and installs software and its dependencies.

<img width="1266" alt="apt get" src="https://github.com/isiak44/Rasheed_Devops/assets/27869977/d38f7ede-2cb5-44d7-bd2a-0feab64b53f8">

---
### 36. nano, vi, jed Command:

`nano|vim|jed`

These three commands allow users to edit and manage files via text editor. 

<img width="781" alt="nano vi" src="https://github.com/isiak44/RasheedPBL/assets/27869977/50165704-c486-40d4-bb77-035d247bf0b2">

---
### 37. alias, unalias Command:

`alias`

With alias command we create a shortcut with the same functionality as a command, file name or text. here we created a shortcut for `less` and `cat` command as shown below. 

<img width="1661" alt="alias" src="https://github.com/isiak44/RasheedPBL/assets/27869977/6e3fe624-59c5-4c21-99e0-67a33400ba8f">

---
`unalias`

Unalias simply deletes an existing alias

<img width="1725" alt="unalias" src="https://github.com/isiak44/RasheedPBL/assets/27869977/30c99f68-3c54-4b9f-bcf0-db5b5b9596b5">

---
### 38. su Command:

`su`

Alias "switchuser"  allows us to run a program as a different user

<img width="1066" alt="su" src="https://github.com/isiak44/RasheedPBL/assets/27869977/51767440-7995-4fa5-869e-2fa042d12394">

---
### 39. htop Command:

`htop`

This command monitors system resources and server processes in real-time. 

<img width="1723" alt="htop" src="https://github.com/isiak44/RasheedPBL/assets/27869977/1ba22211-5a0e-46dd-89e8-f0a5d8134c94">

---
### 40. ps Command:

`ps -e`

produces a snapshot of all running processes in the system 

<img width="1723" alt="ps" src="https://github.com/isiak44/RasheedPBL/assets/27869977/b14020b2-f640-4f85-afa0-ce882087d48c">

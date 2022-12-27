![image](https://user-images.githubusercontent.com/84150540/207605060-d50926be-3efc-41d4-b33c-5287cdfde61c.png)

# The Story - Scanning through the Snow
During the investigation of the downloaded GitHub repo (OSINT task), elf Recon McRed identified a URL `qa.santagift.shop` that is probably used by all the elves with admin privileges to add or delete gifts on the Santa website. The website has been pulled down for maintenance, and now Recon McRed is scanning the server to see how it's been compromised. Can you help McRed scan the network and find the reason for the website compromise?

## Learning Objectives
- What is scanning
- Scanning types
- Scanning Techniques
- Scanning tools

## Tasks
We can connect to this machine using attackbox and we can use the documentation of smbclient for better understanding!!

### Task 1: What is the name of the HTTP server running on the remote host?
we can run a SYN scan using nmap 
```bash
sudo nmap -sS targetIP
```
On port 80 we can see the name of the HTTP server ```Apache```.

### Task 2: What is the name of the service running on port 22 on the QA server?
Using the same scan we can see the service running on port 22 ```ssh```

### Task 3:  What flag can you find after successfully accessing the Samba service?
We start of by enumerating the smb service we can find the sharenames using ```smbclient```
```bash
smbclient -L targetIP
```
We can leave the password blank and we see a few interesting shares


We see there is an Admins share lets try to look what is inside it, using the credentials given to us in the task.
```bash
smbclient //10.10.87.144/admins -U ubuntu
```
The password is: **S@nta2022**
Now we are inside the admin share. Let's list the content using ls.
We will see two files with the name flag.txt and userlist.txt.
So now let's get these files on our local computer. Type the following command
```bash
get flag.txt
```
and 
```bash
get userlist.txt
```
We can access the files without quitting the smbclient by using:
```bash
!cat flag.txt
!cat userlist.txt
```

### Task 4: What is the password for the username santahr?
In the userlist.txt we found, we can see the password for santahr

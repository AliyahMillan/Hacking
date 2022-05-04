# Tech_Supp0rt: 1
<p align="center"><img src="https://user-images.githubusercontent.com/60375020/164568509-7ebe3105-7af2-4301-94ae-e7cd6840d93d.png"></p>

## Enumeration
I begin by starting the machine and doing an nmap scan: ```nmap -sC -sV -Pn 10.10.17.98```

<p align="center"><img src="https://user-images.githubusercontent.com/60375020/164568833-b9293896-5045-4cdf-92d0-3a828c7c8efd.png"></p>

From the nmap scan, we can see that there are four open ports: 22, 80, 139, and 445.

Port 22 manages ssh (secure shell).  

Port 80 manages http requests on a web server and is running on Ubuntu. We can see on the nmap scan that accessing this will lead you to the Ubuntu Default Page. I'll start with this port first, because it's often easier to find vulnerabilities on websites. 

After a quick Google search, I found that SMB (Samba share) used to run on port 139 to communicate with NetBIOS (for file and print sharing over Windows. Originally created in the 1980s, it's actually still used on a number of networks today). Newer versions of SMB run on port 445.

Starting with the website, I navigate to it using the command: ```firefox http://10.10.17/98```

If you'd prefer, you could just enter http://10.10.17/98 in the browser of your choice. 

As it showed up in the nmap scan, we can see it opens on the Ubuntu Default Page: 

<p align="center"><img src="https://user-images.githubusercontent.com/60375020/166619250-ffe50728-232b-4c40-b3ac-690067359ce1.png"><img src="https://user-images.githubusercontent.com/60375020/166619311-39b37a6a-7ea6-4448-a03e-fb5e3ea599eb.png"></p>

This doesn't give us anything. This means I'll investigate the SMB shares that we saw mentioned in the nmap scan (ports 139 and 445).  

The tool I'll be using to investigate the SMB shares is called smbclient, and you don't have to worry about installing or getting the tool if you're using Kali Linux (because it comes installed by default). Using the tool is simple, all you do is follow this syntax: ```smbclient –L  \\\\IP_Address_Goes_Here\\```, without the underscores, and with your given IP Address where stated.
<p align="center"><img src="https://user-images.githubusercontent.com/60375020/166620233-ce1432c1-d2de-4664-bfec-64d818ffbdeb.png"></p>

When entering in your command, it will prompt you for a password. You can leave it blank and just hit your "Enter" key.  

Looking at the results of our command, we can see that the following sharenames are present: print$, websvr, and IPC$. print$ and IPC$ are common sharenames, so this is probably something you won't want to spent time on  looking into. You're going to be more interested in uncommon and unique sharenames. So I'll be looking more closely into websvr.  

The way I'm going to look into it is by continuing to use smbclient, with the command: ```smbclient  \\\\IP_Address_Goes_Here\\where_you_want_to_look```, where "where_you_want_to_look" is the name of the sharefile you want to inspect. 

<p align="center"><img src="https://user-images.githubusercontent.com/60375020/166620556-901b6e00-c5ad-4030-9965-739bf7264cf9.png"></p>
Because we were able to do this, it means we have access to websvr, and can proceed to download and view the file we found in websvr (enter.txt). 

To do this, we're going to use the "get" command. This will download the file and save it for us, in my case, in the /home/kali/ directory on my Kali Linux machine. 

I cat the file:  
<p align="center"><img src="https://github.com/AliyahMillan/Hacking/files/8617771/cat.enter.txt"></p>


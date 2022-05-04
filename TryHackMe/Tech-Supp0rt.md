# Tech_Supp0rt: 1
<p align="center">
  <img src="https://user-images.githubusercontent.com/60375020/164568509-7ebe3105-7af2-4301-94ae-e7cd6840d93d.png">
</p>

## Enumeration
I begin by starting the machine and doing an nmap scan: ```nmap -sC -sV -Pn 10.10.17.98```

<p align="center">
  <img src="https://user-images.githubusercontent.com/60375020/164568833-b9293896-5045-4cdf-92d0-3a828c7c8efd.png">
</p>

From the nmap scan, we can see that there are four open ports: 22, 80, 139, and 445.

Port 22 manages ssh (secure shell).  

Port 80 manages http requests on a web server and is running on Ubuntu. We can see on the nmap scan that accessing this will lead you to the Ubuntu Default Page. I'll start with this port first, because it's often easier to find vulnerabilities on websites. 

After a quick Google search, I found that SMB (Samba share) used to run on port 139 to communicate with NetBIOS (for file and print sharing over Windows. Originally created in the 1980s, it's actually still used on a number of networks today). Newer versions of SMB run on port 445.

Starting with the website, I navigate to it using the command: ```firefox http://10.10.17/98```

If you'd prefer, you could just enter http://10.10.17/98 in the browser of your choice. 

As it showed up in the nmap scan, we can see it opens on the Ubuntu Default Page: 
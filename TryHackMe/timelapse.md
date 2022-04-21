# Enumeration
I began the enumeration phase with a basic nmap scan: ```nmap 10.10.11.152```

![nmap1scan](https://user-images.githubusercontent.com/60375020/164550829-f64b6817-c598-4746-9554-57715f01d848.png)

The first attempt showed that the ping was blocking the nmap probes, so I added ```-Pn``` to the nmap command to get it to work. 
From there, I was able to see 11 open ports. I did a more in-depth nmap scan: ```sudo nmap -Pn -p- -sS --min-rate 5000 --open -vv -n 10.10.11.152 -oG allPorts```

![nmap2scan](https://user-images.githubusercontent.com/60375020/164550849-6f8bbc40-3a73-4452-81c5-865caccd5874.png)

This told me a little more about the ports that we found open, and.

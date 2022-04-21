# Enumeration
I began the enumeration phase with a basic nmap scan: ```nmap 10.10.11.152```
<p align = "center">
<img src="https://user-images.githubusercontent.com/60375020/164550829-f64b6817-c598-4746-9554-57715f01d848.png">
</p>

The first attempt showed that the ping was blocking the nmap probes, so I added ```-Pn``` to the nmap command to get it to work. 
From there, I was able to see 11 open ports. I did a more in-depth nmap scan: ```sudo nmap -Pn -p- -sS --min-rate 5000 --open -vv -n 10.10.11.152 -oG allPorts```
<p align = "center">
<img src="https://user-images.githubusercontent.com/60375020/164550849-6f8bbc40-3a73-4452-81c5-865caccd5874.png">
</p>

This told me a little more about the ports that we found open, and -----------------------------------------------------------------------------------.

I continued with one last nmap, ```nmap -Pn -p389 --script ldap-rootdse 10.10.11.152```
<p align = "center">
<img src="https://user-images.githubusercontent.com/60375020/164555303-1b0b6192-895c-44e3-9f06-57407b20890c.png" width=60%>
</p>

```
┌──(kali㉿ADHDExcalibur)-[~] 

└─$ nmap -Pn -p389 --script ldap-rootdse 10.10.11.152 

Starting Nmap 7.92 ( https://nmap.org ) at 2022-04-13 21:53 EDT 

Nmap scan report for 10.10.11.152 

Host is up (0.084s latency). 

  

PORT    STATE SERVICE 

389/tcp open  ldap 

| ldap-rootdse:  

| LDAP Results 

|   <ROOT> 

|       domainFunctionality: 7 

|       forestFunctionality: 7 

|       domainControllerFunctionality: 7 

|       rootDomainNamingContext: DC=timelapse,DC=htb 

|       ldapServiceName: timelapse.htb:dc01$@TIMELAPSE.HTB 

|       isGlobalCatalogReady: TRUE 

|       supportedSASLMechanisms: GSSAPI 

|       supportedSASLMechanisms: GSS-SPNEGO 

|       supportedSASLMechanisms: EXTERNAL 

|       supportedSASLMechanisms: DIGEST-MD5 

|       supportedLDAPVersion: 3 

|       supportedLDAPVersion: 2 

|       supportedLDAPPolicies: MaxPoolThreads 

|       supportedLDAPPolicies: MaxPercentDirSyncRequests 

|       supportedLDAPPolicies: MaxDatagramRecv 

|       supportedLDAPPolicies: MaxReceiveBuffer 

|       supportedLDAPPolicies: InitRecvTimeout 

|       supportedLDAPPolicies: MaxConnections 

|       supportedLDAPPolicies: MaxConnIdleTime 

|       supportedLDAPPolicies: MaxPageSize 

|       supportedLDAPPolicies: MaxBatchReturnMessages 

|       supportedLDAPPolicies: MaxQueryDuration 

|       supportedLDAPPolicies: MaxDirSyncDuration 

|       supportedLDAPPolicies: MaxTempTableSize 

|       supportedLDAPPolicies: MaxResultSetSize 

|       supportedLDAPPolicies: MinResultSets 

|       supportedLDAPPolicies: MaxResultSetsPerConn 

|       supportedLDAPPolicies: MaxNotificationPerConn 

|       supportedLDAPPolicies: MaxValRange 

|       supportedLDAPPolicies: MaxValRangeTransitive 

|       supportedLDAPPolicies: ThreadMemoryLimit 

|       supportedLDAPPolicies: SystemMemoryLimitPercent 

|       supportedControl: 1.2.840.113556.1.4.319 

|       supportedControl: 1.2.840.113556.1.4.801 

|       supportedControl: 1.2.840.113556.1.4.473 

|       supportedControl: 1.2.840.113556.1.4.528 

|       supportedControl: 1.2.840.113556.1.4.417 

|       supportedControl: 1.2.840.113556.1.4.619 

|       supportedControl: 1.2.840.113556.1.4.841 

|       supportedControl: 1.2.840.113556.1.4.529 

|       supportedControl: 1.2.840.113556.1.4.805 

|       supportedControl: 1.2.840.113556.1.4.521 

|       supportedControl: 1.2.840.113556.1.4.970 

|       supportedControl: 1.2.840.113556.1.4.1338 

|       supportedControl: 1.2.840.113556.1.4.474 

|       supportedControl: 1.2.840.113556.1.4.1339 

|       supportedControl: 1.2.840.113556.1.4.1340 

|       supportedControl: 1.2.840.113556.1.4.1413 

|       supportedControl: 2.16.840.1.113730.3.4.9 

|       supportedControl: 2.16.840.1.113730.3.4.10 

|       supportedControl: 1.2.840.113556.1.4.1504 

|       supportedControl: 1.2.840.113556.1.4.1852 

|       supportedControl: 1.2.840.113556.1.4.802 

|       supportedControl: 1.2.840.113556.1.4.1907 

|       supportedControl: 1.2.840.113556.1.4.1948 

|       supportedControl: 1.2.840.113556.1.4.1974 

|       supportedControl: 1.2.840.113556.1.4.1341 

|       supportedControl: 1.2.840.113556.1.4.2026 

|       supportedControl: 1.2.840.113556.1.4.2064 

|       supportedControl: 1.2.840.113556.1.4.2065 

|       supportedControl: 1.2.840.113556.1.4.2066 

|       supportedControl: 1.2.840.113556.1.4.2090 

|       supportedControl: 1.2.840.113556.1.4.2205 

|       supportedControl: 1.2.840.113556.1.4.2204 

|       supportedControl: 1.2.840.113556.1.4.2206 

|       supportedControl: 1.2.840.113556.1.4.2211 

|       supportedControl: 1.2.840.113556.1.4.2239 

|       supportedControl: 1.2.840.113556.1.4.2255 

|       supportedControl: 1.2.840.113556.1.4.2256 

|       supportedControl: 1.2.840.113556.1.4.2309 

|       supportedControl: 1.2.840.113556.1.4.2330 

|       supportedControl: 1.2.840.113556.1.4.2354 

|       supportedCapabilities: 1.2.840.113556.1.4.800 

|       supportedCapabilities: 1.2.840.113556.1.4.1670 

|       supportedCapabilities: 1.2.840.113556.1.4.1791 

|       supportedCapabilities: 1.2.840.113556.1.4.1935 

|       supportedCapabilities: 1.2.840.113556.1.4.2080 

|       supportedCapabilities: 1.2.840.113556.1.4.2237 

|       subschemaSubentry: CN=Aggregate,CN=Schema,CN=Configuration,DC=timelapse,DC=htb 

|       serverName: CN=DC01,CN=Servers,CN=Default-First-Site-Name,CN=Sites,CN=Configuration,DC=timelapse,DC=htb 

|       schemaNamingContext: CN=Schema,CN=Configuration,DC=timelapse,DC=htb 

|       namingContexts: DC=timelapse,DC=htb 

|       namingContexts: CN=Configuration,DC=timelapse,DC=htb 

|       namingContexts: CN=Schema,CN=Configuration,DC=timelapse,DC=htb 

|       namingContexts: DC=DomainDnsZones,DC=timelapse,DC=htb 

|       namingContexts: DC=ForestDnsZones,DC=timelapse,DC=htb 

|       isSynchronized: TRUE 

|       highestCommittedUSN: 131177 

|       dsServiceName: CN=NTDS Settings,CN=DC01,CN=Servers,CN=Default-First-Site-Name,CN=Sites,CN=Configuration,DC=timelapse,DC=htb 

|       dnsHostName: dc01.timelapse.htb 

|       defaultNamingContext: DC=timelapse,DC=htb 

|       currentTime: 20220414095545.0Z 

|_      configurationNamingContext: CN=Configuration,DC=timelapse,DC=htb 

Service Info: Host: DC01; OS: Windows 

  

Nmap done: 1 IP address (1 host up) scanned in 0.84 seconds 
```
--------------------------------------------------------------------

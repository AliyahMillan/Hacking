# Root Me
______________________________________________________________________________

**DISCLAIMER**: Challenges will be in either French or English. I'd like to be able to practice French, especially in the infosec/cybersec field.

There's always Google Translate, but I might translate portions anyway.

## 🔒 Cryptanalysis/Cryptanalyse 🔒
### Encodage - ASCII:
https://www.root-me.org/fr/Challenges/Cryptanalyse/Encodage-ASCII

We're provided an associated resource to complete the challenge: ![image](https://user-images.githubusercontent.com/60375020/144296644-fdb7ac8c-6eea-481b-b202-cea9ce7c03f2.png)

Beginning the challenge, we're redirected to http://challenge01.root-me.org/cryptanalyse/ch8/ch8.txt and are provided the following string: 
> 4C6520666C6167206465206365206368616C6C656E6765206573743A203261633337363438316165353436636436383964356239313237356433323465

Now we  just have to use the table provided to decode the string.

<details>
  <summary> 📣 FLAG SPOILER WARNING 📣 </summary> 
  
  This is the solution to the challenge, valued at 5 points. You might have to finish the rest.... 😉
  Can't go giving the true flag, now can I?
 
Le flag de ce challenge est: [Really long string]
</details>

### Encodage - UU:
-------------------------------------------------------------------------------------------------------------
https://www.root-me.org/fr/Challenges/Cryptanalyse/Encodage-UU

We're provided a PDF titled 'EN - Encodings format.pdf': https://repository.root-me.org/Cryptographie/EN%20-%20Encodings%20format.pdf?_gl=1*bhowco*_ga*Mzg3ODQ3ODc2LjE2MzgyNDAxMDg.*_ga_SRYSKX09J7*MTYzODM3ODQyOC45LjEuMTYzODM4NDM4Ny4w. 

Beginning the challenge, we're redirected to http://challenge01.root-me.org/cryptanalyse/ch1/ch1.txt. On this website, it gives us the following:
```
_=_ 
_=_ Part 001 of 001 of file root-me_challenge_uudeview
_=_ 

begin 644 root-me_challenge_uudeview
B5F5R>2!S:6UP;&4@.RD*4$%34R`](%5,5%)!4TE-4$Q%"@``
`
end
```
This is where the PDF resource really comes in handy. Flipping through, we can see it really breaks down UU Encoding and provides useful tables.
<details>
  <summary> 📣 FLAG SPOILER WARNING 📣 </summary> 
  
  This is the solution to the challenge, valued at 5 points. You might have to tweak the final result just a little.... 😉
  Can't go giving the true flag, now can I?
  
```
Very simple ;)
PASS = [This should be the password] 
```

</details> 


# 1337 CTF

Below is my solutions for some of the challenges i've done.

## Crypto : get_next_line

You are given 2 files, main.c and file,
inspecting main.c we can see that there are a lot of "empty" lines and then a typical main for a get_next_line function
returning to the "empty area" of the main.c, selecting it shows that there ares some tabs in a very interesting sequence, we can from here expect that it is whitespace language, so let's try to translate it in dcode, indeed it give us the following

```python
from cryptography.fernet import Fernet 

flag = b'gAAAAABholOrj0h6mj3SDVrwGYCJSv9kpqPaiofosX7Z-50ydhS5XXXymn2xBowgVnQxbP67zegqSFG9kB72eWbjnme6nTH5Zn3plnB7OwpkSBPUdf_r9ZKHKSfJakM1Gc4hP5nW-Jqr'
```

we have the flag but as we can see it is encrypted, but looking at the import statement *from cryptography.fernet import Fernet*, the flag is encrypted in fernet, in order to decrypt a fernet message we need a key, luckily the second file attached to challege is likely the key in this instance so let's write a script to decrypt our flag:

```python
def decrypt(msg):
   
    key = "5QEqi9e-guHYP_VclQ-8Jz0_CQPqXjDE8PynuU3qCpI="
    f = Fernet(key)
    decrypted_message = f.decrypt(msg) #decrypt msg

    print(decrypted_message.decode())

if __name__ == "__main__":
    decrypt(b'gAAAAABholOrj0h6mj3SDVrwGYCJSv9kpqPaiofosX7Z-50ydhS5XXXymn2xBowgVnQxbP67zegqSFG9kB72eWbjnme6nTH5Zn3plnB7OwpkSBPUdf_r9ZKHKSfJakM1Gc4hP5nW-Jqr')
```
output => LORD_LAARBI{N0rm1nette_stRuggle_15_ReAL}


## Crypto : dekalog

You are given a txt file where you are somehow supposed to get the flag from it, initial look at the text we can see that it does not mean much. 


```
Laughter is on thee other side. These demons shall be gone by sabbath, soon.
Apostasy is religion's abandonment. I, the messenger of god brought Lord's
divine laws, believe in all these rules and the messiah shall save you all.
Yesterday's oath is all but broken.
```

Looking at the challenge description (ctf website is down so i can't screenshot), we can see that lord laarbi is somehow sending us cryptic messages through his "religious text".
A quick google search about bible code and we got this : "The Bible code, also known as the Torah code, is a purported set of encoded words within the Hebrew text of the Torah that, according to proponents, has predicted significant historical events."

Apparently some believe that encoded messages have been sent through the bible using Equidistant letter sequence, so let's try it on our challenge...
To obtain an ELS from a text, choose a starting point (in principle, any letter) and a skip number(the skip number remains constant), we already know that the flag format is LORDLAARBI{} so we have to search for that sequence in the text to obtain the ELS number, we start with the "L" and look where is the next "O", the number of letters between L and O is the constant number we gonna skip to obtain the flag so let's do it, we can obviously see that O is 9 letters away from L so let's skip every 9th letter and see what we will get...

```
"L"aughter is "o"n thee othe"r" side. These "d"emons shal"l" be gone by s"a"bbath, soon.
"A"postasy is "r"eligion's a"b"andonment. "I", the messen"g"er of god br"o"ught Lord's
"d"ivine laws, "b"elieve in a"l"l these rul"e"s and the me"s"siah shall "s"ave you all.
"Y"esterday's "o"ath is all b"u"t broken.
```

Combining the letters quoted we get ***LORDLAARBI god bless You***, knowing the flag format, we add underscores and brackets and hooray the flag is:
```
LORDLAARBI{god_bless_You}
```



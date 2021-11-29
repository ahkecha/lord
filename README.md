
# 1337 CTF

Below is my solutions for some of the challenges i've done.




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



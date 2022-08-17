# Quiz

Diese challenge war mehr oder weniger einfach "schreibe code welche keywoerter annimmt und fuehre die Operation aus".

Am Ende sah mein script wie folgt aus:

```python
from pwn import *
import sys
import codecs
import re

def do_calc(s):
    a = s.split("+")
    b =  int(a[0]) + int(a[1])
    return b
            
def normalize(s):
    return s.replace("-", "")
    
def rot13(s):
    return codecs.decode(s, 'rot_13')
    
def bin_dec(s):
    bin = int(s, 2)
    log.info(str(bin))
    return str(bin)
            
def xor_it(s,t):
    """xor two strings together"""
    return "".join(chr(ord(a)^ord(b)) for a,b in zip(s,t))
        
def main():
    c = remote('20.126.227.19', 45377)
    while True:
        challenge = c.recvline().decode('utf-8')
        log.info(challenge)
        if("Wieviel ist" in challenge):
            bla = re.search("\"(.*?)\"", challenge).group(1)
            log.info(bla)
            c.sendline(str(do_calc(bla)))
            
        
        elif("Normalisieren" in challenge):
            bla = re.search("(\w-)+.", challenge).group()
            log.info(str(bla))
            c.sendline(normalize(bla))

        elif("ROT13" in challenge):
            bla = re.findall("(\w+)\:", challenge)[1]
            log.info(str(bla))
            c.sendline(rot13(bla))

        elif("Base64" in challenge):
            bla = re.findall("([0-9a-zA-Z_=]+)\:", challenge)[1]
            log.info(str(bla))
            c.sendline(b64d(bla))

        elif("hexadezimal" in challenge):
            bla = re.findall("(\w+)\:", challenge)[1]
            log.info(str(bla))
            c.sendline(unhex(bla[2:]))

        elif("(dezimal)"in challenge):
            bla = re.findall("(\w+)\:", challenge)[0]
            log.info(str(bla))
            c.sendline(bin_dec(bla))

        elif("XOR" in challenge):
            bla = re.search("(\w+)\:", challenge).group(1)
            blax = re.findall("[A-Z]{4,}", challenge)[0]
            log.info("bla = " +str(bla))
            log.info("blax = " +str(blax))
            x = (xor_it(bla, blax))
            log.info(x)
            c.sendline(x)

        elif("Schirmherrin" in challenge):
            c.sendline("Judith Gerlach")

main()
```

welches in die folgende Flagge resultierte:
`DBH{h4b_5p455_b31_dbh}`

Was hierbei vielleicht noch interessant zu beachten ist ist, dass ich fuer den Namen der Schirmherrin ("Judith Gerlach") die DBH Seite durchforsten musste :)

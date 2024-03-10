# Credits
@ren completed the cryptography challenge, so credits for him on the cryptography category writeup.

## Task 1: round and round
Question: i love to eat pizza

Flag: `RWSC{PIZZINI_CIPHER_WAS_EAZY}`

We are given a ciphertext of `2126226{19122929121712_6121911821_26422_842928}`. Since we know the flag format, can assume that `RWSC = 2126226`. Looking at this logic for awhile, he noticed that the numbers could act as hex values instead where an extra 0 is appended to 6. Example: `21 26 22 06` So he made a script to build the flag.

```
test = "21 26 22 06".split()
a = "19 12 29 29 12 17 12".split()
b = "06 12 19 11 08 21".split()
c = "26 04 22".split()
d = "08 04 29 28".split()

for i in test:
    print(chr(int(i)+61),end="")
print("_",end="")

for i in a:
    print(chr(int(i)+61),end="")
print("_",end="")

for i in b:
    print(chr(int(i)+61),end="")
print("_",end="")

for i in c:
    print(chr(int(i)+61),end="")
print("_",end="")

for i in d:
    print(chr(int(i)+61),end="")
print("_",end="")

print()
```

```
└─$ python pizza.py 
RWSC_PIZZINI_CIPHER_WAS_EAZY_
```

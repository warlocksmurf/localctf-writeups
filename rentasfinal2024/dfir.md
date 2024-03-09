# Task 1: Hidden zombie
Question:

Flag: ``

We are given a png image file of a zombie. Unfortunately, I could not solve this during the CTF. But looking back at the challenge, it was actually pretty simple (and it's definitely not DFIR ffs). The first thing I always do is to use `pngcheck` to check for any errors in the png image. It mentions that there are errors on the `IHDR` chunk so I went to fix it.

```
└─$ pngcheck -v zomba.png
zlib warning:  different version (expected 1.2.13, using 1.3)

File: zomba.png (1536669 bytes)
  chunk IHDR at offset 0x0000c, length 13
    1024 x 921 image, 32-bit RGB+alpha, non-interlaced
  CRC error in chunk IHDR (computed 80d35286, expected 7f1d2b83)
ERRORS DETECTED in zomba.png
```

After fixing the IHDR chunk.
```
00000000   89 50 4E 47  0D 0A 1A 0A  00 00 00 0D  49 48 44 52  00 00 04 00  00 00 03 99  08 06 00 00  .PNG........IHDR............
0000001C   00 80 D3 52  86 00 00 00  01 73 52 47  42 00 AE CE  1C E9 00 00  00 04 67 41  4D 41 00 00  ...R.....sRGB.........gAMA..
00000038   B1 8F 0B FC  61 05 00 00  00 09 70 48  59 73 00 00  0E C4 00 00  0E C4 01 95  2B 0E 1B 00  ....a.....pHYs..........+...
```

Checking the png image again with `PCRT` this time, it seems that there are several IDAT chunks having incorrect lengths. So I tried adjusting the height and width of the image to find hidden secrets below or above the picture.

```
└─$ python2 PCRT.py -i ~/Desktop/sharedfolder/zomba-modified.png -o ../output.png 

         ____   ____ ____ _____ 
        |  _ \ / ___|  _ \_   _|
        | |_) | |   | |_) || |  
        |  __/| |___|  _ < | |  
        |_|    \____|_| \_\|_|  

        PNG Check & Repair Tool 

Project address: https://github.com/sherlly/PCRT
Author: sherlly
Version: 1.1

[Finished] Correct PNG header
[Finished] Correct IHDR CRC (offset: 0x1D): 80D35286
[Finished] IHDR chunk check complete (offset: 0x8)
[Finished] Correct IDAT chunk data length (offset: 0x53 length: FFA5)
[Finished] Correct IDAT CRC (offset: 0x10000): E413EAD2
[Detected] Error IDAT chunk data length! (offset: 0x10004)
chunk length:FFF4
actual length:FFA5
[Notice] Try fixing it? (y or n) [default:y] n
[Detected] Error IDAT chunk data length! (offset: 0x1FFB5)
chunk length:41FD3640
actual length:FFA5
[Notice] Try fixing it? (y or n) [default:y] n
[Detected] Error IDAT chunk data length! (offset: 0x2FF66)
...
```

After awhile, it seems that the height was the culprit.
```
00000000   89 50 4E 47  0D 0A 1A 0A  00 00 00 0D  49 48 44 52  00 00 04 00  00 00 03 99  08 06 00 00  00 80 D3 52  .PNG........IHDR...............R
to
00000000   89 50 4E 47  0D 0A 1A 0A  00 00 00 0D  49 48 44 52  00 00 04 00  00 00 04 00  08 06 00 00  00 80 D3 52  .PNG........IHDR...............R
```

![zomba-modified](https://github.com/warlocksmurf/localctf-writeups/assets/121353711/4b353819-5f7c-41d5-8fd9-caef2baa136c)

Additionally, a great tool recommended by another rENTAS member told me about [FotoForensics](https://fotoforensics.com/), that explains how they got first blood so quickly.

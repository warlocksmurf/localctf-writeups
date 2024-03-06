# Task 1: Mobile
Question: Below are the phone that has been physicaly extracted (full memory extraction). Somehow the data has been tampered, however the question is super easy. The flag is RWSC{passwordphone} (< dont submit this flag, its a clue).

Hint: [Hacking a Samsung Galaxy for $6,000,000 in Bitcoin!?](https://youtu.be/icBD5PiyoyI?si=LUV16WHkvm0hTdVk)

Flag: `RWSC{875463120}`

We are given a report on a forensics case on Android, specifically Lenovo P70. Before the hints were given, I actually read the reports slowly TWICE and found nothing of interest. 


![image](https://github.com/warlocksmurf/localctf-writeups/assets/121353711/daebd484-8c47-495d-bcf0-3a832777f936)

I noticed several artifacts like photos of a car, photos of Malaysian guys, bootup screenshots, and several Android icon caches. Using almost all my attempts, I was blessed with the hint from the authors and watched the video carefully. The video talked about a guy cracking the password pattern for an Android phone by analyzing its system files. So the hint was pretty obvious already, the password we are looking for is actually a password pattern, not a PIN or a password string.

![image](https://github.com/warlocksmurf/localctf-writeups/assets/121353711/787778e0-fb1f-446f-88d3-76fd4412c791)

From the video, it seems that the `gesture.key` file is where password patterns are stored, however, Lenovo P70 does not have this file since it was not written anywhere on the report. So I did some research on Android forensics and found this interesting [blog](https://resources.infosecinstitute.com/topics/digital-forensics/practical-android-phone-forensics/) and found out that it is sometimes stored in `/data/system/password.key`. So I filtered `/data/system` in the report and found the hex values of the password patterns.

![image](https://github.com/warlocksmurf/localctf-writeups/assets/121353711/34985f43-f628-431a-b69c-82981f153633)

Reading on how I can crack the hex values just like the guy in the video, I went online and found the perfect [tool](https://github.com/Webblitchy/AndroidGestureCrack) to crack the exact hash value `8e7e00c0bd5ce227f7be204c8b7c159669c776d4`. After running the script, the flag can be obtained.

```
└─$ python gesturecrack.py -r 8e7e00c0bd5ce227f7be204c8b7c159669c776d4
   

        The Lock Pattern code is [8, 7, 5, 4, 6, 3, 1, 2, 0]

        For reference here is the grid (starting at 0 in the top left corner):

        |0|1|2|
        |3|4|5|
        |6|7|8|

```

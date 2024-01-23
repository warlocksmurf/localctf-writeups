# Solution
## Challenge 1
The challenge asked us to find the registration number of a specific flute. Google it.

![flute](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/385ed7f3-db39-445a-b3a5-f73691542759)

## Challenge 2
The challenge asked us to find a specific card with its card name, error type and grade. 

A CGC cert number `4302093025` was provided to start our search, so I used the official CGC card verifier to identify the card.

![image](https://github.com/warlocksmurf/localctf-writeups/assets/121353711/063efe90-8dd4-483f-a60a-aa835d05cd71)

After verifying the card cert, we can identify the name and number of the card, but it seems that the error type and grade is not present for some reason. So I tried to just Google the cert number and found a video on a Charizard VSTAR card error.

![image](https://github.com/warlocksmurf/localctf-writeups/assets/121353711/54676bef-7e63-40a5-9d2f-78bfb170c47e)

Zooming into the card, the cert number proves that this is the card we are looking for, and hence the flag too.

<p float="left">
  <img src="https://github.com/warlocksmurf/localctf-writeups/assets/121353711/b555550b-764f-47b3-b9ed-e8d5999e07ba" alt="pokemon2" />
  <img src="https://github.com/warlocksmurf/ctf-writeups/assets/121353711/531cb360-f9bb-40ee-a839-1744c6d9b838" alt="spy-kids-lemme-zoom-in-on-that" />
</p>

## Challenge 3
The challenge asked us to find a specific location shown in these two videos `Kpop MV` and `the LCK trailer`. Watching the videos carefully, it seems that the location shown in both videos is a container yard.

![kpop](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/bc836ad4-b024-4323-999e-61e18a60e602)

![LCK](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/3fab868b-fa87-47ed-af62-f0adbab5a5c0)

So I tried reverse searching the LCK image and got the exact location in the first result!

![Screenshot 2023-12-24 224713](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/a2fc8c53-627d-45e0-8f19-7727917972b6)

![korea](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/0aba5b91-fd48-4fc1-a9e6-282610c310d2)

## Challenge 4
The challenge asked us to find the two specific stations between the person in the picture. Sadly I could not solve this before the CTF ended, so I attempted it at home.

![Sky_Full_of_ _Cables](https://github.com/warlocksmurf/localctf-writeups/assets/121353711/bf5a954e-e658-4aeb-bc3b-8a9b2cfde0d1)

Reversing the full picture, it seems that this place could potentially be in Thailand, specifically Bangkok. Now it's time to narrow the search by going through different parts of the picture.

![image](https://github.com/warlocksmurf/localctf-writeups/assets/121353711/cdc37d46-5641-45b9-9768-43e8bce90024)

After several minutes of searching, I found this youtube video that could help in finding the specific location.

![image](https://github.com/warlocksmurf/localctf-writeups/assets/121353711/a503fab3-f62e-4400-80a6-6245d038cf2a)

It looks like the location could be near Golden Line, so I continued looking for clues in the picture and found a barber at the bottom of the picture.

![image](https://github.com/warlocksmurf/localctf-writeups/assets/121353711/df8b2238-126d-4f2a-b702-2a9caa73f1c6)

Googling the barber store's name (54 Barber), it is shown the location is actually Golden Line. So can even see the tall bulky building indicated at the right corner of the picture.

![image](https://github.com/warlocksmurf/localctf-writeups/assets/121353711/4e8edbd7-0a8b-4a80-a165-d5774938da27)

![osint2](https://github.com/warlocksmurf/localctf-writeups/assets/121353711/b0528da6-c059-4a62-b5bf-1f4e61b9c482)

Now we just have to find the two stations between this line. Looking at the train line, we can see it starts at Krung Thonburi (Golden Line) and stops at Charoen Nakhon. So the flag is these two stations.

![osint3](https://github.com/warlocksmurf/localctf-writeups/assets/121353711/33e62d01-e6bf-4ded-ae88-588852cb391e)

## Challenge 4
The challenge asked us to the last ping location of a shark that bit the author's report in her blog. Sadly I could not solve this before the CTF ended, so I attempted it at home.

Since its the author's blog, we can access it to find more clues. However, since the challenge said that the shark bit (past tense) her report, the report should not be present in her blog. One way to recover it is to use WayBackMachine to essentially "go back in time".

![image](https://github.com/warlocksmurf/localctf-writeups/assets/121353711/94242088-d125-4a0d-ade2-55bc764759b8)

Alright so there is a hidden post in her blog. Looking through it, it was filled with random text and irrelevent clues for finding the flag. However, there is a statement that could prove beneficial. They mentioned that the shark was a Male, so we could use that information to filter something else later on.

![image](https://github.com/warlocksmurf/localctf-writeups/assets/121353711/a891a6e5-02e3-4a71-9921-c9cb3f980d23)

We also found a supposedly barcode at the bottom of the page, but after several minutes on decoding it, it was completely irrelevent.

![image](https://github.com/warlocksmurf/localctf-writeups/assets/121353711/5b5994a0-551e-467f-8a93-0e9bb78b0cf0)

Since we have to find the last ping location of this shark, I tried this website to maybe get the location.

![image](https://github.com/warlocksmurf/localctf-writeups/assets/121353711/c14f899f-19f4-4008-942f-a298097d6dfd)

Since we know its a Male shark, we can filter it and narrow our search. However, the author updated the flag saying that we should change the filters to specify Tracking Activity to show the most recent only. Apparently the shark's ping suddenly went alive the moment the CTF started (what a coincidence). With this update, many people finally knew which shark to take and the answer can be found by looking at the most recent shark ping which is Bob.

![image](https://github.com/warlocksmurf/localctf-writeups/assets/121353711/2499f5ab-25c9-4cd6-83a1-7c812fd0bcdd)

![image](https://github.com/warlocksmurf/localctf-writeups/assets/121353711/898b785a-a415-41a8-bbab-0c5baf18bfc5)

# OSINT
## Challenge 2
The challenge gave us an image only. So of course I have to reverse search it for more information.

![Free! - Study Hard by GothicShoujo on DeviantArt](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/fba4714d-5047-4e63-8090-8b6278cb51be)

Google reverse search will lead us to a Pinterest website: `https://www.pinterest.com/pin/402016704213891878/`

Notice how there is a user (Liciela) that liked the image, we then go to their profile.

![image](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/a9588061-0163-4aa2-86f0-15161df07410)

![Screenshot 2023-12-24 214423](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/a476079f-30ff-4e63-9caa-9f7d4f306ccd)

Hmmm a UniKL user, bingo! Going to one of his created post, we can see that he has a Hoyolab account. I assume the name is the same in Hoyolab.

![Screenshot 2023-12-24 214508](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/2473d1c0-7277-4621-8e37-580e9b580ff3)

![Screenshot 2023-12-24 214629](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/a7737b52-b2f2-4804-a229-91e051bdcdc2)

After checking his hoyolab account, we can see that he has a Twitter account now lol. At this point, I was prepared to dive into an Inception OSINT game.

![image](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/50079f00-78a6-4ffc-8f4a-8a13b27b9520)

So stalking his Twitter page, I notice that he said he was top 50 on Malaysia. I guess its time to go Tryhackme.

![image](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/9621d396-f697-4010-b7c4-947209d4e03c)

When checking the monthly leaderboards (November), we can see that his account was top 1. Pressing into his Tryhackme account shows a Github account linked to it so we can proceed there now.

![image](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/2c63bc5a-5f2c-4964-a452-6dbb6115c621)

![image](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/8025a256-30ac-4fb4-b3de-314f9c4537f7)

The flag: ``gohunikl2023{Y0u_F0und_M3}``

![image](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/4fb84283-f0ae-4959-8258-0031ddbb4d7d)


# Forensics
## Challenge 2
We are given a ``eerie-area.pcapng`` file for this challenge. The first thing that I always do is to filter and analyze important protocols first like HTTP or DNS.

![image](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/9c740c00-88fa-47f6-b458-69544433f6bd)

Looking at HTTP packets, notice a strange GET request where the full URL seems to be ``http://www.example.com/4W3i2hyrJTVfRrM77fBXcpRjYJwb3NkzyzP3kAXWqy9N2sJKm6Y``. However, accessing it gives a random domain.

![image](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/676db477-3b0b-4780-b21c-99d75dc36d1f)

So I tried decoding the URL with base58 and we get another URL that redirects to dropmefiles.

![image](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/e3e01309-5e9f-461e-ac35-2994f7158e80)

Entering the website, we can download another file which gives us an executable file (``dropmefiles.net_boo.exe``). Using 7zip we can discover hidden stuff in this .exe file and after going through all of them, we come across a flag.

![image](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/165a20b6-99bb-439a-875c-d981625e00b4)

![image](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/7d4dcd9e-bc38-456d-ab0c-7e0ccc3b0f2b)

However, this was a bait!! So I just check the contents in this .exe file and found the real flag.

![eerie](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/8bc7005a-f0fb-4bfd-93a9-04b4f6173654)

The flag: ``gohunikl2023{p3eK_4_&0o}``

# Scoreboard
## Team Perseus
![image](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/db8e8995-ae82-49e5-833e-d0182268231a)

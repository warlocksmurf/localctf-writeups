# Solution
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

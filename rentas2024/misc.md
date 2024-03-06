# Task 1: Hidden Discord
Question: Starting point: (https://discord[.]gg/7aMtftbDY4)

Flag: `RWSC{r34d_d15c0rd_d3v3l0p3r_API_r3f3r3nc3}`

We are given a link to join a Discord server. Inside the server, the admin mentioned that there are 5 parts of the flag throughout the server.

![image](https://github.com/warlocksmurf/localctf-writeups/assets/121353711/0c2bed2b-4efa-499d-ba28-f5367f842537)

Part 1 of the flag was easily noticed, its in the chat room of the voice channel. Similarly, part 3 can be easily found in the events tab.

![image](https://github.com/warlocksmurf/localctf-writeups/assets/121353711/65a9b64e-08d3-4f40-bfe6-fdda54bc3cf3)

![image](https://github.com/warlocksmurf/localctf-writeups/assets/121353711/b8ca43c3-c82d-4d28-afd6-8e8bd2fc6234)

While getting the flag parts we actually got several hints from the admin. 

```
Find the CATegory? :black_cat: :cat2:
roles :question:
```

For part 2 and 4, my teammate @Shen helped find them with special plugins. After finding this [video](https://www.youtube.com/watch?v=3s7YFN-nT3Q) about a [plugin](https://github.com/JustOptimize/return-ShowHiddenChannels) with BetterDiscord to see hidden channels, he managed to get part 2 and 4 of the flag.

![hidden](https://github.com/warlocksmurf/localctf-writeups/assets/121353711/4cade388-e7c9-4802-9a8e-7c8402f1e01a)

For the last part of the flag, it is in the server icon. So just use Discord on browser and inspect the icon and change the size of it.

```
https://cdn.discordapp.com/icons/1202263455466541096/bfa6d5f2ed8067d3367791ed5b4d6941.webp?size=1024
```

![bfa6d5f2ed8067d3367791ed5b4d6941](https://github.com/warlocksmurf/localctf-writeups/assets/121353711/1f9f5e51-6e8f-448f-ad6a-1ae8b4986031)

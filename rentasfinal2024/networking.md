## Task 1: I Hope You Have The Software
Question: There is a flag in one of these servers. Can you Help me find them? Retrieve it and submit as RWSC{flag}.

Flag: `RWSC{!t5_a_t4c3r_f!l3_:D}`

We are given a packet tracer file to analyze a network. After looking at the connections, it seems that there were extra servers overlapping one another.

![Screenshot 2024-03-09 164657](https://github.com/warlocksmurf/localctf-writeups/assets/121353711/d5618e17-14ad-4ba7-91b5-695ebe006db0)

Looking at every server configurations, only server 6 had an `index.html` website in it. Checking its contents, the flag can be found.

![Screenshot 2024-03-09 164719](https://github.com/warlocksmurf/localctf-writeups/assets/121353711/c172a2d0-1d75-4e5a-8ebd-0af070ad183a)

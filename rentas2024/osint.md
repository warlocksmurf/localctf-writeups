## Task 1: Medellín Cartel
Question: Assume that you are working for Law Enforcement, do you really got some IQ to investigate high profile criminals?

Hint(s):
* The Sicarios…
* You might think the given picture, is useless. Guessy. But its not. If u are about to investigate a crime group. You have to criminal-profile every single member of the group. E.g what they do, eat, visit, etc. If u recon, Blacky AKA Nelson Hernandez is the only sicarios that has went to uniten IG. U should focus on that acc only. For real - If u went to other sicarios, u will get lost. Next step? Technical stuff. Dig the flag inside the IG, metadata is there. That is how u profile someone, dig deeper as u could on that acc.

Flag: `RWSC{Bl4cky_S1c4r1o}`

We are given an image of the Medellín Cartel tree. 

![organization](https://github.com/warlocksmurf/localctf-writeups/assets/121353711/8a13289c-b261-473b-8d2a-49e51cc5b1ac)

No offence but this OSINT challenge was guessy, without the hint I would have never know we are looking for `Nelson Hernandez` and especially on Instagram. However, since we got the hint already, it was actually super simple. First find his Instagram profile, thank god he was the only person with `blacky` if not it will take awhile.

![image](https://github.com/warlocksmurf/localctf-writeups/assets/121353711/b1b00061-44bd-40d6-b288-40a5446fab49)

![image](https://github.com/warlocksmurf/localctf-writeups/assets/121353711/117505c4-6b7a-4896-8e85-23c6fb1b0be0)

Then inspect the source code or "Instagram metadata" and just filter the flag. Overall, not a great OSINT challege compared to the next challenge.

![image](https://github.com/warlocksmurf/localctf-writeups/assets/121353711/b17be348-364b-44d1-9a73-c8e0a5ef372f)

## Task 2: Cali Cartel
Question: Unlike Medellin Cartel, the Cali Cartel rootcause of their falldown is clear. This is why knowledge is power!

Flag: `RWSC{C4L1_C4RT3L_PWN3D}`

We are given an image of a strange looking business operation (probably drugs). Reading the description, it seems that I must be looking for information on the `Cali Cartel`.

![Cali_chart2](https://github.com/warlocksmurf/localctf-writeups/assets/121353711/0e476133-4b40-4eee-be25-430bcf9f882c)

Doing some research on them, it seems that their downfall was caused by an insider betrayal, specifically from [Jorge Salcedo](https://www.seattletimes.com/nation-world/a-daring-betrayal-helped-wipe-out-cali-cocaine-cartel/). So I went ahead and lookup the betrayer's name and got lucky when using Google Dorking.

![image](https://github.com/warlocksmurf/localctf-writeups/assets/121353711/0250fd69-e05f-4926-a622-76c202f8ee68)

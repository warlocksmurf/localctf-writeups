# Task 1: Скорпион
Question: In one investigation, xxxxxxx actors created two folders in the C:\ drive labeled in and out, which served as a staging directory (central location) for hosting malicious executables. he in folder contained file names in accordance with host names on the victim’s network, likely imported through a scanning tool. The out folder contained various files listed in Table 2 below. For encryption process - After mapping the network, the ransomware encrypts data using a 4096-bit RSA encryption key with a ChaCha20 algorithm. The algorithm features a 256-bit key, a 32-bit counter, and a 96-bit nonce along with a four-by-four matrix of 32-bit words in plain text. Registry modification commands are not obfuscated, displayed as plain-text strings and executed via cmd.exe. The encryptor allows arguments -d (select a directory) and -sr (file deletion), defined by the authors of the code as parseOptions. After the lines of binary strings complete their tasks, they delete themselves through the control panel to evade detection.

Hint(s): Telegram -> Darkweb

Flag: `RWSC{rhysidafc6lm7qa2mkiukbezh7zuth3i4wof4mh2audkymscjm6yegad}`

Reading the description, it seems that they are referring to a pretty recent ransomware called `Rhysida`. Reading about it, I found a [blog](https://www.cisa.gov/news-events/cybersecurity-advisories/aa23-319a) that talks about it and also all the C2 IPs it connects to. I also found out that they operate in the Dark Web where they sell the information they stole from victims. 

![fig6a-rhysida-recent-victim](https://github.com/warlocksmurf/localctf-writeups/assets/121353711/85f9e610-5492-4e01-ac9e-7da1ce3be0c1)

This was kind of guessy cause no where in the question mentioned Telegram, but after receiving the hint, I went on Telegram and search `Rhysida` and found a chat room with a sameple flag.

![Screenshot_20240306_085725_Telegram](https://github.com/warlocksmurf/localctf-writeups/assets/121353711/79a9d200-5ea4-4b13-b393-b5fe16d77c9b)

Reading the chat, it seems that the flag is the mirror link of their onion page. This can be obtained in many sources like [this](https://github.com/fastfire/deepdarkCTI/blob/main/ransomware_gang.md)

PS: Random stuff I encountered:
* I found out the ransomware also attacked `Indah Water Konsortium` in Malaysia.
* I messaged a random Telegram bot when finding the chat room.

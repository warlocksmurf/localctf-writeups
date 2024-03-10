## Task 1: Скорпион
Question: In one investigation, xxxxxxx actors created two folders in the C:\ drive labeled in and out, which served as a staging directory (central location) for hosting malicious executables. he in folder contained file names in accordance with host names on the victim’s network, likely imported through a scanning tool. The out folder contained various files listed in Table 2 below. For encryption process - After mapping the network, the ransomware encrypts data using a 4096-bit RSA encryption key with a ChaCha20 algorithm. The algorithm features a 256-bit key, a 32-bit counter, and a 96-bit nonce along with a four-by-four matrix of 32-bit words in plain text. Registry modification commands are not obfuscated, displayed as plain-text strings and executed via cmd.exe. The encryptor allows arguments -d (select a directory) and -sr (file deletion), defined by the authors of the code as parseOptions. After the lines of binary strings complete their tasks, they delete themselves through the control panel to evade detection.

```
Table 2: Malicious Executables Affiliated with xxxxxxx Infections

conhost.exe
6633fa85bb234a75927b23417313e51a4c155e12f71da3959e168851a600b010
A ransomware binary.

psexec.exe
078163d5c16f64caa5a14784323fd51451b8c831c73396b967b4e35e6879937b
A file used to execute a process on a remote or local host.

S_0.bat
1c4978cd5d750a2985da9b58db137fc74d28422f1e087fd77642faa7efe7b597
A batch script likely used to place 1.ps1 on victim systems for ransomware staging purposes [T1059.003].

1.ps1
4e34b9442f825a16d7f6557193426ae7a18899ed46d3b896f6e4357367276183
Identifies an extension block list of files to encrypt and not encrypt.

S_1.bat
97766464d0f2f91b82b557ac656ab82e15cae7896b1d8c98632ca53c15cf06c4
A batch script that copies conhost.exe (the encryption binary) on an imported list of host names within the C:\Windows\Temp directory of each system.

S_2.bat
918784e25bd24192ce4e999538be96898558660659e3c624a5f27857784cd7e1
Executes conhost.exe on compromised victim systems, which encrypts and appends the extension of .groupname(sensored) across the environment.
```

Hint(s): Telegram -> Darkweb

Flag: `RWSC{rhysidafc6lm7qa2mkiukbezh7zuth3i4wof4mh2audkymscjm6yegad}`

Reading the description, it seems that they are referring to a pretty recent ransomware called `Rhysida`. Reading about it, I found a [blog](https://www.cisa.gov/news-events/cybersecurity-advisories/aa23-319a) that talks about it and also all the C2 IPs it connects to. I also found out that they operate in the Dark Web where they sell the information they stole from victims. 

<p align="center">
  <img src="https://github.com/warlocksmurf/localctf-writeups/assets/121353711/85f9e610-5492-4e01-ac9e-7da1ce3be0c1" width=50% height=50%>
</p>

  This was kind of guessy cause no where in the question mentioned Telegram, but after receiving the hint, I went on Telegram and search `Rhysida` and found a chat room with a sameple flag.

<p align="center">
  <img src="https://github.com/warlocksmurf/localctf-writeups/assets/121353711/79a9d200-5ea4-4b13-b393-b5fe16d77c9b" width=50% height=50%>
</p>

Reading the chat, it seems that the flag is the mirror link of their onion page. This can be obtained in many sources like [this](https://github.com/fastfire/deepdarkCTI/blob/main/ransomware_gang.md)

PS: Random stuff I encountered:
* I found out the ransomware also attacked `Indah Water Konsortium` in Malaysia.
* I messaged a random Telegram bot when finding the chat room.

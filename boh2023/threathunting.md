# Solution
## Challenge 1
The challenge wants us to analyze a compromised virtual machine that was recently attacked by a ransomware.

Challege 1 ask us to find the filename of the ransomware executable inside the compromised system. My method to solve it was basically just manually analyzing the directories and files within the machine and found suspicious programs in the System32 directory.

![image](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/e5aa0a7e-279a-44df-abab-1c1e978859cc)

However, after the CTF ended, I felt like the best way to find suspicious executables (accordng to SANS) is by using either Amcache, Shimcache or even Prefetch files. So by using AmcacheParser from EZTools, we can extract the Amcache located in `C:\Windows\appcompat\Programs\Amcache.hve` and parse it to be analyze further using Timeline Explorer.

```
.\AmcacheParser.exe -f 'C:\Users\ooiro\Documents\CTF\BOH2023\Threat Hunting\Amcache.hve' --csv 'C:\Users\ooiro\Documents\CTF\BOH2023\Threat Hunting\Chall1.csv'
```

Going through Timeline Explorer, we can find two suspicious executables in System32.

![image](https://github.com/warlocksmurf/localctf-writeups/assets/121353711/cdbaab33-0e6e-4fb1-bf07-fb1a92f46526)

Answer: `Mcqqic24UJyU40JKdja0A.exe`

## Challenge 2
The challenge wants us to identify the SHA256 hash value of the executable responsible for exfiltrating data. We know there is another suspcious program located in the same directory with the ransomware. So I analyzed the other executable using VirusTotal and found out it was the dropper for the ransomware. So I assume is the answer and surprisingly it is.

![image](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/9c0deddc-ccf5-4104-b1a0-90e6aa719d87)

Answer: `2e1594cea1d8e012c709f3d71a4e57dcbc9d017b89f623822fc56c9f734eb491`

## Challenge 3
The challenge wants us to identify the external connections done by this malicious executable (dropper). Using Virustotal again, we can see the HTTP request done to a malicious IP address.

![image](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/c97ac23c-daa1-4953-a054-200351cd976a)

Answer: `http://146.190.89.115:8080/YPAPJDoGD3aIQlFix11ZA.php`

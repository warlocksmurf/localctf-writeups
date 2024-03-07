# Solution
## Challenge 1
The challenge wants us to decipher the flag with AES decryption.

Encryption script:
```
from Crypto.Cipher import AES
from Crypto.Util.Padding import pad
from Crypto.Random import get_random_bytes
from Crypto.Protocol.KDF import PBKDF2

import textwrap

def encrypt_file(file_path, password):
    with open(file_path, 'rb') as file:
        plaintext = file.read()


    iv = get_random_bytes(AES.block_size)

    passwd = textwrap.dedent(password)[:-1]


    salt = b'salt123'  
    key = PBKDF2(passwd.encode(), salt, dkLen=16)


    cipher = AES.new(key, AES.MODE_CBC, iv)


    ciphertext = cipher.encrypt(pad(plaintext, AES.block_size))


    encrypted_file_path = file_path + '.enc'
    with open(encrypted_file_path, 'wb') as file:
        file.write(ciphertext + iv)

    print("Encryption successful. Encrypted file saved as:", encrypted_file_path)


password = "ni5h2h?Yrq8Do?n+|6a;pKbZkv%}O~tV" 
file_path = "./flag.txt"   
encrypt_file(file_path, password)
```

The output given:
```
N: 28161864534081810305839467239167774824180698442991360538137338315924601027539535041400325106523598882827263670671140966855944057889837783992080270143420119844958855679728614805589197733901663249220100214524859116110365815705699485099116276988534253521580223115836247118089590595980346272692504104976860138248959015932618979651746563030552421216691329694961700647328850519321776696007920491542096366696034760558758393690945535590284240994579352805664119144134863786797266463118165575746650538843159490903440899114347091988968775074879305009340592457617508211781199057573663246634610497629416920053419998682083393087987
C: 762355112596222421309825166446067448121886093544068458795156044255325081286699861240486430215279901835675723822721970949307265398924333599178805487220325668055743991293697494477706560130827449405781098938392283482757063955895656607033694619449376928780098570577226994800731087835230561205556094959240210387000
e: 3
```

So I created a decryption script with `ChatGPT` to obtain flag.

Decryption script:
```
from Crypto.Cipher import AES
from Crypto.Util.Padding import unpad
from Crypto.Protocol.KDF import PBKDF2
import textwrap

def decrypt_file(encrypted_file_path, password):
    with open(encrypted_file_path, 'rb') as file:
        ciphertext_iv = file.read()

    # Extract the IV (Initialization Vector) and ciphertext
    ciphertext = ciphertext_iv[:-AES.block_size]
    iv = ciphertext_iv[-AES.block_size:]

    passwd = textwrap.dedent(password)[:-1]
    salt = b'salt123'
    key = PBKDF2(passwd.encode(), salt, dkLen=16)

    cipher = AES.new(key, AES.MODE_CBC, iv)

    decrypted_data = unpad(cipher.decrypt(ciphertext), AES.block_size)

    decrypted_file_path = encrypted_file_path[:-4]  # Remove the '.enc' extension
    with open(decrypted_file_path, 'wb') as file:
        file.write(decrypted_data)

    print("Decryption successful. Decrypted file saved as:", decrypted_file_path)

password = "ni5h2h?Yrq8Do?n+|6a;pKbZkv%}O~tV"
encrypted_file_path = "./flag.txt.enc"
decrypt_file(encrypted_file_path, password)
```

![image](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/564de13f-a2f3-450b-9bf9-616acab7fb36)


## Challenge 2
This challenge wants us to decipher the flag with SageMath. This challenge was done by my teammate @Damien

Reading the code, we see that this is an RSA implementation with small `e = 3` and when the exponent of RSA is small, it is vulnerable to `Coppersmith Attack`.

The sage file:
```
#!/usr/bin/env sage
from Crypto.Util.number import bytes_to_long

p, q = random_prime(2 ^ 1024), random_prime(2 ^ 1024)
n = p*q
e = 3

assert len(flag) > e

FLAG = open("flag.txt", "rb").read().strip()
m = bytes_to_long(FLAG + b' is your challenge flag.')
c = pow(m, e, n)

print("N: ", n)
print("C: ", c)
print("e: ", e)
```

So my friend created a simple python script to decrypt the flag.

Decryption script:
```
import binascii
import gmpy2

n = 28161864534081810305839467239167774824180698442991360538137338315924601027539535041400325106523598882827263670671140966855944057889837783992080270143420119844958855679728614805589197733901663249220100214524859116110365815705699485099116276988534253521580223115836247118089590595980346272692504104976860138248959015932618979651746563030552421216691329694961700647328850519321776696007920491542096366696034760558758393690945535590284240994579352805664119144134863786797266463118165575746650538843159490903440899114347091988968775074879350009340592457617508211781199057573663246634610497629416920053419998682083393087987
e = 3
cipher_str = 762355112596222421309825166446067448121886093544068458795156044255325081286699861240486430215279901835675723822721970949307265398924333599178805487220325668055743991293697494477706560130827449405781098938392283482757063955895656607033694619449376928780098570577226994800731087835230561205556094959240210387000

gs = gmpy2.mpz(cipher_str)
gm = gmpy2.mpz(n)
ge = gmpy2.mpz(e)

root, exact = gmpy2.iroot(gs, ge)
text_output = binascii.unhexlify(format(root, 'x')).decode('utf-8')

print(text_output)
```

![image](https://github.com/warlocksmurf/ctf-writeups/assets/121353711/67c5b36e-6c9f-4895-ad90-23d8dc3544e8)

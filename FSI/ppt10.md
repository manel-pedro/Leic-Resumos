## Session Keys
Modern systems distinguish
Long-term keys != session keys
Session keys: ephemeral, data limited if corrupted
* Long-term keys:
    * Strong security requirements in storage (e.g. HSMs, smartcards)

The symmetric cryptography is more efficient and less complex.
* However there are two problems:
    * Shared long-term sysmmetric keys
    * Non-repudiation: in public key the person with private key can preduce the message. However in sysmmetric all of those with the key can produce the encrypte message and so we can not prove who encrypte


## Public Key Encryption
Anyone with pk(public key) can encrypt
Ony the one with sk(secret key) can decrypt

The asymmetric keys have thousands of bit's. Only feasible for small messages so we send as the payload of the asymmetric key the **encrypted sysmmetric key**.

* Hybrid paradigm
    1. Sender generates symmetric session key k to encrypt p
    2. Sender gets pk(create by the receiver), uses it to encrypt k
    3. Receiver gets two ciphertexts, corresponding to (1) and (2)

1. Key Generation (The Setup)

To create your keys, you follow these steps:

### The RSA problem
1. Select Two Primes: Choose two massive prime numbers, p and q. (In modern systems, these are roughly 1024 bits each).
2. Calculate the Modulus (n): Multiply them: n=p⋅q. This n is part of both your public and private keys.

3. Calculate Euler's Totient (ϕ): ϕ=(p−1)⋅(q−1). This value is the secret "magic number" that allows the math to work. This must be kept secret.

4. Choose Public Exponent (e): Usually, the number 65537 is used.

5. Compute Private Exponent (d): You find a number d such that d⋅e≡1(modϕ).

## OAEP Encryption
The problem with RSA is the same with block cipher, the same creates the same output. So the OAEP creates a x that goes into the RSA algorithm.

### Signatures
The important is to assure the authorship. After signature the document can not be falsifiable, reusable and repudiation(only one can sign, so they cann't refuse signing something)
The person that wants to sign uses a sk to sign and shared the pk, with this we can verify the singing.
It is the reverse of the asymetric encryption, because instead of anyone being able to encrypte where only as the ability to do so and every one else can verify 

Diference between MACs and Assymetric Authenticity is two verify the MAC everyone needs to know the key, so you cann't assure who signs because everyone knows the k. So the advantage with Assymetric Authenticity is only the person with the sk can sign.

## The Diffie-Hellman Protocol
Basicly each agre in a p value, then each choose a private number, for exampel a,b. 
Them each send is p elevated to the power of is number, p^a and p^b. 
Now each can compute de reciving to the power of the number they have. 
k = (g^x)^y = g^xy = g^yx = (g^y)^x

## Authenticated Diffie-Hellman

![image1](./ppt10/Screenshot%202026-01-06%20at%2000.38.33.png)

# Key Takeaways
* Key agreement allows for symmetric crypto
* In public-key settings
* Diffie-hellman allows for k to be exchanged
* Provided one cannot solve the discrete logarithm
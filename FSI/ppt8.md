### The one-time pad
> Q1: Is this secure?
>>It is perfectly secure (as long as keys are used only once)
>
> Q2: Why is this not used to encrypt everything?
>>Keys must have the same size as the messages
>>To send a 2 Gb file, I must use a 2 Gb key!
>>How can we pre-share and store such huge keys?
>>But it is used everywhere in cryptography as a building block

### Kerckhoffs's Principle

The idea that security was obtain via the encryption systems being secret
> Security through sucrity 

The Kerckhoff principle says that everthing should be public knowledge.

### key takeways

Encryption is the combination of the encryption and the decryption algorithms

Classical ciphers fail because of this main reasons

> Key space is very small
> Patterns reveal original message
> One-time pad is perfect secure, and perfect garbage, 1:1 key to message ratio. very inefficiient to use in practise.

## Block Ciphers

>
>> Encypt: E(k,p)
>> * Key k size a
>> * plaintext p size b
>> * outputs c size b
>
>> Decypt: D(k,c)
>> * Key k size a
>> * plaintext c size b
>> * outputs p size b
>
> The block cipher is invertible: k defines a permutation

## Modes of Operation

> * Block-ciphers are a primitive
>> The just work in define in small block shuncks
> * On their own, they’re not very useful
>> because they only work for specific block sizes(e.g 254 b) they cannt encrpty large files
> * There are insecure ways to encrypt with a block cipher
>> if you take a big file and enctypte block by block simpley(ECB algorithm) patters will appear
> * Encryption schemes have their own security definitions
>> Since just "scrambling blocks" isn't enough, we need a higher standard of security
> * Encryption schemes built from block ciphers
>> We take the primitive (the block cipher) and combine it with logic—like chaining the output of one block into the input of the next, or adding a random "Initialization Vector" (IV).
> * We prove encryption secure assuming a block cipher is secure
>> we prove the security by proving the building blocks
>>> "If we assume that AES is a perfect random scramble (the primitive is secure), then I can mathematically prove that AES-GCM (the scheme) is impossible to break."

### ECB Electronic-Code-Book Mode

As previous mentions is insecure because of the each block is independent and there is nothing random in the system, the blocks with equal values will iyeal an equal encrypte value, like background colour wich make the frequency analysis possible(e.g the penguin)

### CBC Cipher Block Chaining

Where each there is a IV(initialization vector).
Each bock uses the previous encrypte block to XOR before the encryption, the first blocks uses the IV.

> CBC Padding
>> * Let k >|M|be the next multiple of B (in bytes)
>> * Add k −|M|bytes with value k −|M|
>> * The last byte always reveals how much padding was added
>>      * 0x01 means 1 byte of padding with that value
>>      * 0x03 means 3 bytes of padding with that value

## CTR Counter Block Mode

This create a Key stream, this keystream is usualy the IV with a Counter(increases by each bock by one), this is encrypted and then XoR with the message bock.

> Counter mode is very efficient
>> * Key stream can be pre-processed
>> * Block cipher not applied to the message!
>> * Any part of the data can be accessed efficiently
>> * This includes read/write access
>> * Decryption/encryption can be parallelized

## Key takeways 
* AES selected via public competition
* ... as all modern ciphers are
* SubBytes; ShiftRows; MixColumns; AddRoundKey
* Currently the de facto standard for block ciphers
* Block ciphers by themselves are insecure
* So we rely on modes of encryption: (not in ECB), CBC, CTR


# Key
## Storage

> All of this uses and generates keys
>How is this done?
For Symmetric Crypto
>> Generated uniformly at random
>> Derived using a Key Derivation Function
>> From a password or low entropy secret
>> From a high-entropy master key from key exchange protocol

> For Asymmetric Crypto
>>Key generation algorithm →key pair
>>Private key holder generates both keys; publishes public key
>>Asymmetric keys are typically much larger
>> RSA keys take roughly 4096-bits for 128-bit security
>> Elliptic-curve keys take roughly 400-bits for 128-bit security
30/

## Generation
> Ideally, in an external secure hardware
>>Hardware Security Module (HSM)
>>Smartcard or similar cryptographic token

>Key wrapping
>> Long-term keys are often wrapped before storage
>>To encrypt with another key
>>Password-based encryption (low security)
>>Wrap with HW-protected master key (standard security)
>>Master key stored in trusted hardware (high security)

## Quantifying Security

> Number of steps of the best attack
> * n-bits security
>* Best attack to break the scheme requires 2n steps
>* n-bit keys cannot ever give more than n-bit security
>> then n-bits can ever give more the n-bits because the brute force allows to find the correct key

>t-bit keys could lead to n-bit security s.t. n <<t
>> Q2: When?
>> Best attack is more efficient than brute-force
>> Common in asymmetric cryptography
>> Keys must follow specific structures, not random bit strings

>Quantifying using n-bit security permits comparing schemes
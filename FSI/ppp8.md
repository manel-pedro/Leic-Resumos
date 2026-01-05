### The one-time pad
> Q1: Is this secure?
•It is perfectly secure (as long as keys are used only once)
>
> Q2: Why is this not used to encrypt everything?
•Keys must have the same size as the messages
• To send a 2 Gb file, I must use a 2 Gb key!
•How can we pre-share and store such huge keys?
•But it is used everywhere in cryptography as a building block

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
>> 
> * Encryption schemes built from block ciphers
> * We prove encryption secure assuming a block cipher is secure

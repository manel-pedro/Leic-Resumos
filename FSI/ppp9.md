Use apenas as fontes: slides_w8.pdf, slides_w9.pdf

## Finding Collisions
Collisions can be found with work √2n, much better than 2n!
>Methodology
>>Compute values like the brute-force attack

>>Store them in a data structure indexed by image value

>>Each new image value is searched in data structure
>>Repeat until a collision is found

>How many operations?
>>After n values, we checked n ∗(n−1)/2 pairs Q: why?
>>Checking 2n pairs takes roughly √2n values
>>Overall complexity is that of finding the pre-image of a hash
with n/2 bits of output (only half of the range)

The birthday paradox (not very paradoxical, just counterintuitive)

## Sponge Construction
# Preciso de ainda ver

# Key Takeaways
>Hash functions are one-way functions
>> From any sized inputs to fixed-size output
>> Easy to go from x to f (x )
>> Hard to go from f (x ) to x

>For output of 2n, collision can be found in ≈√2n = 2n
2
>> So for 2128 resistance, output must be at least 2256
>Two main constructions: MD(basiclu put the the H0 value(public) and M0 into compress, then use the M1 H1(result previous calculated of M0 and H0) to calculate the next compress) and Sponge

>Merkle-Damgård
>> Used in MD5; SHA1; SHA2
>Sponge
>> Used in SHA3 and SHAKE

> SHA-2 and SHA-3 currently the de facto standards

## Authentication and Message Integrity
Sender computes the **t** that is the MAC(k,m), k the key and m the message. Then send the **m,t** the reciver computes t' with MAC(k,m) and if the t == t' then the sender knows the k. It acceptes the message. This proves that the message is valid. 
> MACs do not give confidentiality. They provide integrity

MACs constructed from hash functions and block ciphers
Simplest construction: prefix key
MAC(k,m) = H(K ||M)
* MD yields insecure MAC!
    * Given (m,t), attacker outputs H(K ||M||pad||M′)
    * This can be computed just from t′and m′
    * Length extension attack

* A consideration in SHA-3 construction
    * Abandon MD construction
    * Include explicit keyed hash

* When instantiated with MD construction
    * HMAC is simply H((k⊕opad)||H((k⊕ipad)||m))
    * ipad and opad are constraints: align to block size

## Key Takeaways
* Keyed hashing allows for message authentication
* For hash function h, one cannot produce h(k,x ) w/o k
* Provides integrity; ciphers give confidentiality
* Just add a key as prefix!
    * Problem! Length extension attacks
* HMAC
    * Input padding and output padding, both using the key
* CMAC
    * Do AES-CBC without IV; return the last block
    * With a twist to prevent prefix extension
* Wegman-Carter
    * Use a UHF for a unique message
    * XOR it with an encryption of a nonce
    * Used in AES-GCM (next!)

## Why Authenticated Encryption?
* Any secure channel in practice uses authenticated encryption
    * Messages need to be confidential
    * Messages need to be authentic
    * Messages should not be repeated/omitted/removed

Encryption provides confidentiality

MACs provide authenticity

Authenticated public meta-information (e.g. sequence numbers) is
used to solve the third point 

## Encrypt-and-MAC
* AE with k = (k1, k2) done with parallel processing
    * c ←$ E (k1,m)
    * t ←MAC (k2,m)
    * Output: (c,t)
>Problems – The bad
>>Potentially malicious c decrypted before authentication
>>MACs not designed to ensure confidentiality!
>>Construction can be secure for some MACs...
>>>Very easy to make mistakes

>Used in SSH: MAC (k2,m||n), where n is the sequence number

## MAC-then-Encrypt
* AE with k = (k1, k2) done sequentially
    * t ←MAC (k1,m)
    * c ←$ E (k2,m||t)
    * Output: c

This is the ungly because it  need to decytption before the authentication.
And you dont know why the decryption fail, could be padding or the mac, so 
it could make the attacker now the error.

## Encrypt-then-MAC
* AE with k = (k1, k2) done sequentially
    * c ←$ E (k1,m)
    * t ←MAC (k2,c)
    * Output: c

* Advantages – The good
    * Ciphertext not decrypted unless it is authenticated
    * Useful against DoS attacks
        * MAC verification typically very fast
    * Preferred method, except in legacy systems


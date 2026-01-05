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
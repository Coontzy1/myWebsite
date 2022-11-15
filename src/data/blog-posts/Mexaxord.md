---
title: Megaxord
publishDate: 11 Nov 2022
description: BuckeyeCTF Challenge writeup for Megaxord
---

# Megaxord

## Description

Some pesky wizard stole the article I was writing. I got it back, but it's all messed up now :(

Hint: the wizard used the same magic on every character...

## Encryption Theory

Based on the problem name, it's pretty evident that the "wizard's magic" is just an XOR function. The XOR function securely encrypts bits, but also allows decryption with a given key. This encryption startegy is known as a stream cipher, but a secure stream cipher requires a completely random key that is the length of the message to be secure.

## Solution Theory

Because the same encryption (magic) is used on every character, the key length is known to be one character long. From there, brute forcing only requires at worst 256 iterations to complete.

## Solution

```py
with open('megaxord.txt', 'rb') as a:
    megaxord = a.read()


for i in range(0xFF):
    unencrypted = []
    for j in megaxord:
        unencrypted.append(int(j)^i)
    plain = ""
    for j in unencrypted:
        plain = plain + chr(j)
    if plain.find("buckeye") != -1:
        print(plain)
        print(plain[plain.find("buckeye"):plain.find("}", plain.find("buckeye"))+1])
        break
```

The final flag is found to be `buckeye{m1gh7y_m0rph1n_w1k1p3d14_p4g3}`. The plaintext is taken from the Wikipedia page for the Power Rangers media franchise.

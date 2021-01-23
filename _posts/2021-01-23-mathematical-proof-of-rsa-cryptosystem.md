---
title: Mathematical Proof of RSA CryptoSystem!
published: true
---
## [](#header-3)Before Start

I present my sincere love to N.I.H.O. for giving me the motivation to write this article. Another thanks will be to Academician Umut Kuran. He is the best computer scientist I know. He is also a very good mathematician. I'm grateful for everything he did for me

## [](#header-3)What is RSA Encryption? (Wikipedia)

RSA (Rivest–Shamir–Adleman) is a public-key cryptosystem that is widely used for secure data transmission. It is also one of the oldest. The acronym RSA comes from the surnames of Ron Rivest, Adi Shamir, and Leonard Adleman, who publicly described the algorithm in 1977. An equivalent system was developed secretly, in 1973 at GCHQ (the British signals intelligence agency), by the English mathematician Clifford Cocks. That system was declassified in 1997

In a public-key cryptosystem, the encryption key is public and distinct from the decryption key, which is kept secret (private). An RSA user creates and publishes a public key based on two large prime numbers, along with an auxiliary value. The prime numbers are kept secret. Messages can be encrypted by anyone, via the public key, but can only be decoded by someone who knows the prime numbers

![](https://hackernoon.com/hn-images/1*yNPjtfBw0UIXXiSBo6CfDw.png)

* Used in many digital certificates on the Internet.
* The most popular are asymmetric crypto structures.
* Used for small data transfer such as key transfer

As mentioned in the article, two prime numbers are needed for encryption.

## [](#header-3)RSA Encryption Proof

Actually so basic:

Decoding should be the opposite of encoding.

* dk  = decoding key
* ek  = encoding key
* pr  = private
* pub = public


suppose that dkpr(ekpub(x)) = x 

Let's create the rule between public and private keys.

```js
d.e = 1 mod(∮(n))
```
mod∮(n) in that case
```js
d.e = 1 + t ∮(n) 
```
```js
dkpr(y) = x^de = x^1+t∮(n) == (x^∮(n))^t.x(modn)
```
on more solid foundations

```js
gcd(x,n) = >>> because of the houses theorem x^∮(n) == 1(modn)
```
```js
dkpr^(y) = (x^∮(n))^t.x = 1^t.x == x(modn)
```

We mentioned that n must be a prime number. So if we accept the structure (x, q.p), x must contain p and q as a factor.


## [](#header-3)ASCII Table

![](https://cdn.sciencebuddies.org/references/ascii-table.png)

The ASCII equivalent of the letter U is 117. in that case


## [](#header-3)Let's encrypt things!

If we want to encrypt the letter "U" as an example, we need two prime numbers as in the proof.

```js
p=11 ve q=17  
```
```js
n = p.q n = 187
```
```js
T(n) = (p-1).(q-1) = 10.6 >> T(n) == 160
```
```js
1 < e < mod(T(n)) e = 3 
```
```js
de = 1mod(T(n))d = 107 de == 321
```
```js
Our public keys n=187 e=3
```

```js
m = 117
```
```js
m^e = 117^3 == 145mod(187) 
```
The result is 145. Hex equivalent of 145 is "e". Thus, the letter "u" was encrypted with RSA and transmitted to the other party as "e".


## [](#header-3)Decryption

```js
c^d = 145^107 == 117mod(187) 
```

117 ASCII to HEX = U



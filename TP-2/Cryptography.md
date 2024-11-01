# RSA

## Modular Exponentiation:
Modular exponentiation is an operation that is used extensively in cryptography and is normally written like:  2^10 mod 17 .
``` In Python there's a built-in operator for performing this operation: pow(base, exponent, modulus).```
To grab the flag, find the solution to 101^17 mod 22663
```19906.```

## Public Keys:
RSA encryption is modular exponentiation of a message with an exponent e and a modulus N which is normally a product of two primes: ```N=p⋅q```.
The most common value for e is 0x10001 or 65537.
"Encrypt" the number 12 using the exponent e=65537 and the primes p=17 and q=23. What number do you get as the ciphertext?
```bash
a = 12
e = 65537
p = 17
q = 23
k = p*q

encrypt = pow(a,e,k)
print(encrypt)
```

## Euler Tolerant:
RSA relies on the difficulty of the factorisation of the modulus N. If the prime factors can be deduced, then we can calculate the Euler totient of N 
and thus decrypt the ciphertext.
Euler's totient ϕ(N) = (p-1)*(q-1)
```bash
p = 857504083339712752489993810777
q = 1029224947942998075080348647219

et = (p-1)*(q-1)
print(et)
```

## Private Keys:
The private key d is used to decrypt ciphertexts created with the corresponding public key.
If RSA is implemented well, if you do not have the private key the fastest way to decrypt the ciphertext is to factorise the modulus which is very hard to do 
for large integers.
```In RSA, the private key is the modular multiplicative inverse of the exponent e modulo ϕ(N), Euler's totient of N.```
```private key d ≡ pow(e,−1) mod ϕ(N)?```
```bash
p = 857504083339712752489993810777
q = 1029224947942998075080348647219

e=65537
d = pow(e,-1,(p-1)*(q-1))
print(d)
```

## RSA Decryption:
```bash
N = 882564595536224140639625987659416029426239230804614613279163
e = 65537
private =  121832886702415731577073962957377780195510499965398469843281
c = 77578995801157823671636298847186723593814843845525223303932
ans = pow(c,private,N)
print(ans)
```

## RSA Signature:
Imagine you write a message m. You encrypt this message with your friend's public key: c = m^e modN.
To sign this message, you calculate the hash of the message: H(m) and "encrypt" this with your private key: S=H(m)^d modN.

```bash
from Crypto.Hash import SHA256
from Crypto.Util.number import bytes_to_long

N = 15216583654836731327639981224133918855895948374072384050848479908982286890731769486609085918857664046075375253168955058743185664390273058074450390236774324903305663479046566232967297765731625328029814055635316002591227570271271445226094919864475407884459980489638001092788574811554149774028950310695112688723853763743238753349782508121985338746755237819373178699343135091783992299561827389745132880022259873387524273298850340648779897909381979714026837172003953221052431217940632552930880000919436507245150726543040714721553361063311954285289857582079880295199632757829525723874753306371990452491305564061051059885803
d = 11175901210643014262548222473449533091378848269490518850474399681690547281665059317155831692300453197335735728459259392366823302405685389586883670043744683993709123180805154631088513521456979317628012721881537154107239389466063136007337120599915456659758559300673444689263854921332185562706707573660658164991098457874495054854491474065039621922972671588299315846306069845169959451250821044417886630346229021305410340100401530146135418806544340908355106582089082980533651095594192031411679866134256418292249592135441145384466261279428795408721990564658703903787956958168449841491667690491585550160457893350536334242689
m = "crypto{Immut4ble_m3ssag1ng}"
hash_object = SHA256.new(m.encode('utf-8'))
hash = bytes_to_long(hash_object.digest())
signature = pow(hash,d,N)
print(signature)
```

## Factoring:
These days, using primes that are at least 1024 bits long is recommended—multiplying two such 1024 primes gives you a modulus that is 2048 bits large. RSA with a 2048-bit modulus is called RSA-2048.
I used ```sympy``` to factorize it.
```bash
from sympy import factorint
number = 510143758735509025530880200653196460532653147
factors = factorint(number)
min = min(factors)
print(min)

output => 19704762736204164635843
```

## Inferious prime:

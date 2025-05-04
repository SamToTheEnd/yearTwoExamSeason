# Infosec 23 paper

## Question 1 (25 marks)

### ![img.png](img.png)

### i Computationally Secure refers to a cryptosystem being secure agaisnt an attack using a feasible amount of resources
### ii. Given enough ciphertext is important as if an attacker has too much ciphertext they could preform statistical analysis on it to work out some plaintext. with the likes of bigrams and trigrams such as "the,ing,in,an"making it easier to determine plaintext

![img_1.png](img_1.png)

### i. 2 to power of 56
### ii. No this is not secure enough. It could be broken with a brute force attack in a resonable amount of time.

![img_2.png](img_2.png)

### TKP

## Question 2

![img_3.png](img_3.png)

### a)     First 5 plaintext bits: =0 1 1 1 0. First 5 keystream bits: 1 0 1 1 0.

![img_4.png](img_4.png)
![img_5.png](img_5.png)

### i. D

### ii. 128

### iii. 64

![img_6.png](img_6.png)

### ​The forged m2′​=m2​⊕MAC1​ cancels out the intermediate MAC1​ during verification,making MAC′=MAC2​ valid for (m1′​,m2′​). This exploits CBC-MAC’s structure without optional processing.​

![img_7.png](img_7.png)

###  second preimage resistant


## Question 3

![img_8.png](img_8.png)


### i.  Integer Factorization ProblemInteger Factorization Problem
### ii. ElGamal Encryption

![img_9.png](img_9.png)

### i. Alice to Bob: eK​(rA​,rB​,iB​)

### ii. rA

![img_10.png](img_10.png)

### i. Non-repudiation 

### ii. 18≡23(mod55)18≡23(mod55)

## Question 4
![img_11.png](img_11.png)

### The STS protocol fixes DH’s authentication problems by:

- Adding digital signatures on exchanged DH values (yA,yByA​,yB​).

- Requiring certificates to verify public keys.

- Binding the DH values to the session via signatures, preventing MITM and replay attacks.

![img_12.png](img_12.png)

### op 1 ,2 ,3  permitted, op 4 denied


![img_13.png](img_13.png)

### anomaly based detection because it can detect new/unknown attacks if they deviate from normal behavior.








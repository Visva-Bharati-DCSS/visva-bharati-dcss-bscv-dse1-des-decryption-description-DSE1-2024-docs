# Public key cryptography

Public key cryptosystems are different than the conventional secret key cryptosystems in two
different ways :
| Secret key cryptosystem | Public key cryptosystem |
|-------------------------|-------------------------|
| 1. Same key used for encryption and decryption | Two different keys are used for encryption and decryption |
| 2. Sender and receiver should have the knowledge of same key | Sender and receiver should know only one of the keys from the matched pair | 
| 3. Possible to decrypt if the key is determined from plaintext and ciphertext | Not possible to decrypt if encryption key is found from plaintext and ciphertext | <br />

## Components of a Public key cryptosystem

1. Plaintext
2. Encryption Algorithm 
3. Private and Public key pair
4. Ciphertext
5. Decryption Algorithm

## Application

Two types of applications of public key cryptosystems are :
- Plaintext is encrypted using private key of the sender using the encryption 
algorithm. Knowledge of the private key is not available in the receiver side. 
The receiver decrypts using the public key.
- Plaintext is encrypted using public key of using the encryption 
algorithm. Knowledge of the private key is not available in the sender side. 
The receiver decrypts using the private key.

## Mathematical Foundation

### Fermat's theorem

If $p$ is prime and $a$ is a positive integer not divisible by $p$, then <br />
$a^{p-1} = 1(mod~p)$; or in second form <br /> 
$a^p = a(mod~p)$. In this second form, a need not be relatively prime to p.
 
### Euler's Totient function

#### Background 

For any integer $n$, let $\phi(n)$ be the number of integers less than $n$ and
relatively prime to $n$. Hence for any prime number $n$, $\phi(n)$ = $n-1$.
Let $p$ and $q$ are two prime numbers with $p \neq q$, and $n = p \times q$. <br />
$\phi(n) = \phi(pq) = \phi(p) \times \phi(q) = (p-1) \times (q-1)$.

Proof : As the
number of integers not prime to $pq$ are $p, 2p, 3p, \cdots (q-1)p$ and $q, 2q, 3q \cdots (p-1)q$. <br />
So, the total number of integers prime to $pq$ = total number
of integers less than $pq$ - total number of integers not prime to $pq$ <br />
= $(pq - 1) - [(p-1) + (q-1)] = pq - 1 -  (p+q-2) = pq - p - q + 1 = (p-1)(q-1) = \phi(p) \times \phi(q)$.

#### Theorem

For every $a$ and $n$ which are relatively prime, <br />
$a^{\phi(n)} = 1 (mod~n)$ 

## RSA algorithm

Plaintext is encrypted in blocks, where each block has a numeric equivalent 
which is less than a certain $n$, which means size of the block should be less than $log_2(n)$. In practice, the block size is chosen to be $2^i$ where <br />
$2^i \lt n \leq 2^{i+1}$. <br />
Let $M$ be the number represented by the plaintext block, and $C$ be the number 
representing the ciphertext block.<br />
$C = M^e~mod~n~and~M = C^d~mod~n$<br />
Hence $M = (M^e)^d~mod~n = M^{ed}~mod~n.$ 

Both sender and receiver are in the knowledge of n. the encryption key of the 
transmitter is $PU = \{e,n\}$. The decryption key is $PR = \{d, n\}$.

It is possible to find values of $d$, $e$, and $n$ such that $M^{ed}~mod~n = M$ for all $M$ < $n$. <br />
It is not very difficult to calculate $M^e~mod~n$ and $C^d~mod~n$ for all $M$ < $n$. <br />
But it is difficult to determine $d$ if $e$ and $n$ is known, because in
prctice, n is product of two large prime numbers p and q - and determination of
prime factors for a large n has large time complexity.

### Example : 

Let $p = 179424673$, $q = 236887691$. Hence $n = 42503496495400043$. Now If $p$ and $q$ are not known but only $n$ is known, time taken to compute the prime 
factors of $n$ using modest laptop today is slightly more than 1 sec - and the block size is only 56 bit. For longer block sizes, the time would enhance 
exponentially.   

### Setting $e$ and $d$

$M^{ed}~mod~n = M \implies ed~mod~\phi(n) = 1$, which again implies <br />
$d = e^{-1}~mod~\phi(n)$, or in other words d is a multiplicative inverse of e mod $\phi(n)$. So unless $\phi(n)$ is known, it is not possible to derive $d$ 
from $e$. 

1. Select two prime numbers $p$ and $q$.
2. Calculate $n = pq$.
3. Calculate $\phi(n) = (p-1)(q-1)$.
4. Choose an $e$ such that $e$ is relatively prime to $\phi(n)$. 
5. Determine $d$ which is a multiplicative inverse of $e$ mod $\phi(n)$.
6. Key pair : $[e, \phi(n)]$ and $[d, \phi(n)]$ are the key pairs. 

### Using RSA algorithm for encryption

1. A client (such as a browser) contacts the server with a request for data 
while sending the server its public key. <br />
- a) It chooses two prime numbers 
$p$ and $q$ sufficiently large such that the plaintext block is sufficiently 
large.
- b) Find the $\phi$ value, and select $e$ such that $e$ is relatively prime to
  $\phi$.
- c) Inform the server $[e, n]$ as public key, and compute $d$ locally.
- d) The server encrypts plaintext with the client's public key, i.e <br />
     $C = (M^e)~mod~\phi$.
- e) The client decrypts the ciphertext $C$ with the private key as $M = (C^d)~mod~\phi$.   

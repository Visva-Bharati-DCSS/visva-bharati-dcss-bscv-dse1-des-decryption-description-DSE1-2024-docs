# Standardized secret key ciphering algorithm

There are two secret key ciphering algorithm which have been standardized for
deployment in commercial standardized systems worldwide, which are still in use.They are 3DES or Triple-DES and AES ciphering algorithm.

## 3DES or Triple-DES algorithm

The core of 3DES or Triple-DES algorithm is the single-stage DES encryption; 
and chaining of three stages of DES encryption using 2 or 3 keys is called 3DES
or Triple-DES.   

### DES algorithm

DES is a multi-staged secret-key encryption alorithm, where each stage is 
based on a Feistel block cipher. Block ciphering is a scheme where a fixed size
block of plaintext is converted to a ciphertext block. Each Feistel cipher block
encrypts a 48-bit plantext with a 48-bit subkey generated from a 56-bit key.
Each stage has substitution, XOR and permutation function to achieve two 
important aspects to make the encryption difficult to break. These aspects are :
- Diffusion : Each plaintext digit affects multiple ciphertext digits; and 
change in 1 bit in plaintext results in change in multiple ciphertext bits which
are widely distributed.

- Confusion : If the attacker gets some statistical measure of the ciphertext,
it is difficult to deduce any information regarding the key.

These two aspects only leaves brute-force algorithm to break the ciphering. 

#### Flowchart :
<p align="center">
<img src=/home/tathagato/classes/2024_25/DSE1/DES-AES/DES-algorithm-flowchart.png
alt="Flowchart of DES algorithm">
</p>

The above picture shows the flowchart of the encryption algorithm. 16 48-bit subkeys are generated from a 64-bit key in a two-step process. The key generation is illustrated in the following figure.

<p align="center">
<img src=/home/tathagato/classes/2024_25/DSE1/DES-AES/des_key_gen.png
alt="Flowchart of DES algorithm">
</p>

#### Details of each step

##### Initial permutation
A permutation or interleaving is performed on the 64-bit plaintext input. The permutation matrix is shown below. 64 bit positions are shown in 8X8 matrices. Left hand side matrix shows the original bit positions and right hand side matrix shows bits of which position is placed in the sequence after permutation. For example, bit number 58 is placed in 1st position, bit number 50 is placed in 2nd postion, bit number 60 is placed in 9th position, bit number 1 is placed in 40th position etc.

$$
\begin{matrix}
1 & 2 & 3 & 4 & 5 & 6 & 7 & 8 \\
9 & 10 & 11 & 12 & 13 & 14 & 15 & 16 \\
17 & 18 & 19 & 20 & 21 & 22 & 23 & 24 \\
25 & 26 & 27 & 28 & 29 & 30 & 31 & 32 \\
33 & 34 & 35 & 36 & 37 & 38 & 39 & 40 \\
41 & 42 & 43 & 44 & 45 & 46 & 47 & 48 \\
49 & 50 & 51 & 52 & 53 & 54 & 56 & 56 \\
57 & 58 & 59 & 60 & 61 & 62 & 63 & 64 \\
\end{matrix} \implies
\begin{matrix}
58 & 50 & 42 & 34 & 26 & 18 & 10 & 2 \\
60 & 52 & 44 & 36 & 28 & 20 & 12 & 4 \\
62 & 54 & 46 & 38 & 30 & 22 & 14 & 6 \\
64 & 56 & 48 & 40 & 32 & 24 & 16 & 8 \\
57 & 49 & 41 & 33 & 25 & 17 & 9 & 1 \\
59 & 51 & 43 & 35 & 27 & 19 & 11 & 3 \\
61 & 53 & 45 & 37 & 29 & 21 & 13 & 5 \\
63 & 55 & 47 & 39 & 31 & 23 & 15 & 7 \\ 
\end{matrix}
$$

Example : Let the input plaintext be denoted as $M$ and the output after initial permutation be denoted as $IP$. <br />
If $M$ = 0000 0001 0010 0011 0100 0101 0110 0111 1000 1001 1100 1101 1110 1111, then <br />
$IP$ = 1100 1100 0000 0000 1100 1100 1111 1111 1111 0000 1010 1010 1111 0000 1010 1010, <br />
In $M$, bit 58 = 1, bit 50 = 1, bit 42 = 0, bit 34 = 0. So the first 4 bits of $IP$ = 1100. Rest can be seen similarly.

##### Generation of subkeys
DES operates on the 64-bit blocks using key sizes of 56- bits. The keys are actually
stored as being 64 bits long, but every 8th bit in the key is not used (i.e. bits numbered
8, 16, 24, 32, 40, 48, 56, and 64). So, the first step of key generation is to 
permute the 64-bit stored key (PC-1) which also removes bit numbers 8, 16 ... to get the 56-bit ciphering key.

##### PC-1 permutation
The permutation matrix is

$$
\begin{matrix}
57 & 49 & 41 & 33 & 25 & 17 & 9 \\
1 & 58 & 50 & 42 & 34 & 26 & 18 \\
10 & 2 & 59 & 51 & 43 & 35 & 27 \\
19 & 11 & 3 & 60 & 52 & 44 & 36 \\
63 & 55 & 47 & 39 & 31 & 23 & 15 \\
7 & 62 & 54 & 46 & 38 & 30 & 22 \\
14 & 6 & 61 & 53 & 45 & 37 & 29 \\
21 & 13 & 5 & 28 & 20 & 12 & 4\\
\end{matrix}
$$

Let $K$ be the 64-bit key and $K^+$ be the permuted 56-bit key.
$57^{th}$ bit of $K$ becomes $1^{st}$ bit of $K^+$, $49^{th}$ bit
of $K$ becomes the $2^{nd}$ bit of $K^+$ $\cdots$ etc. <br />
$K^+$ is split into two $28$ bit values, $C_0$ and $D_0$. This pair 
$(C_0, D_0)$ is the subkey for the first stage of Feistel encrytion.   

##### Formation of 48-bit subkeys for each Feistel stage
For Feistel stage $n, (n \in {1,2,\cdots 16})$, the 48-bit subkey $K_n$ is
generated using a two-step process. Firstly, $(C_n, D_n)$ is generated
by performing a circular left-shift by 1 or 2 bits over $(C_{n-1}, D_{n-1})$ 
depending on $n$. The number of bits for circular left shifts for each stage is
given in the table below.

| $n$ | number of shifts |
| --- | ---|
| $1$ | $1$ |
| $2$ | $1$ |
| $3$ | $2$ |
| $4$ | $2$ |
| $5$ | $2$ |
| $6$ | $2$ |
| $7$ | $2$ |
| $8$ | $2$ |
| $9$ | $1$ |
| $10$ | $2$ |
| $11$ | $2$ |
| $12$ | $2$ |
| $13$ | $2$ |
| $14$ | $2$ |
| $15$ | $2$ |
| $16$ | $1$ |

After the circular left shifts are applied over $(C_{n-1}, D_{n-1})$ to get $(C_n, D_n)$, the subkey $K_n$ for stage $n$ is generated from $(C_n, D_n)$ through another permutation (let that matrix be denoted as $PC_2$). This converts the 56-bit concatenation of $(C_n, D_n)$ to a 48-bit $K_n$. The permutation matrix is given below.

$$
\begin{matrix}
14 & 17 & 11 & 24 & 1 & 5 \\
3 & 28 & 15 & 6 & 21 & 10 \\
23 & 19 & 12 & 4 & 26 & 8 \\
16 & 7 & 27 & 20 & 13 & 2 \\
41 & 52 & 31 & 37 & 47 & 55 \\
30 & 40 & 51 & 45 & 33 & 48 \\
44 & 49 & 39 & 56 & 34 & 53 \\
46 & 42 & 50 & 36 & 29 & 32 \\
\end{matrix}
$$

Therefore, the first bit of $K_n$ is the $14^{th}$ bit of $C_nD_n$, the second bit the $17^{th}$, and so
on, ending with the $48_{th}$ bit of $K_n$ being the $32^{th}$ bit of $C_nD_n$.

##### Feistel block

Input to the Feistel block of $n^{th}$ stage are $L_{n-1},~R_{n-1}~and~K_n$.  Outputs are $L_n$ and $R_n$, which are both 32-bit numbers.  
$L_n = R_{n-1}$, and $R_n = L_{n-1} \oplus f(K_{n}, R_{n-1})$.

The function $f$ has two stages. In the first stage, 32-bit $R_{n-1}$ is permuted to be a 48-bit number, which is XOR'ed with $K_n$, and then each 6-bit of the XOR'ed value is used to perform a lookup into a table called S-Box to get a 4-bit output. There are 8 S-boxes to get a total of 32-bit output.

The permutation matrix is as follows :<br />

$$
\begin{matrix}
32 & 1 & 2 & 3 & 4 & 5 \\
4 & 5 & 6 & 7 & 8 & 9 \\
8 & 9 & 10 & 11 & 12 & 13 \\
12 & 13 & 14 & 15 & 16 & 17 \\
16 & 17 & 18 & 19 & 20 & 21 \\
20 & 21 & 22 & 23 & 24 & 25 \\
24 & 25 & 26 & 27 & 28 & 29 \\
28 & 29 & 30 & 31 & 32 & 1 \\
\end{matrix}
$$

Each S-box is a 4X16 matrix. Let $R^*_{n}$ denote the permuted $R_n$, and $Y_n$ denote $R^*_n \oplus K_n$. For each 6-bit of $Y_n$, the first and last bit taken togther determines the row index (between 0 - 3) and the other 4 bits determine the column index (between 0 - 15). Each element of S-box is a 4-bit value (between 0 - 15). Hence, the 48-bit $Y_n$ is converted to 8 6-bit values, which are used to index 8 S-box matrices to get 8 4-bit values. Hence the output of the S-box lookup is a 32-bit number. The S-box matrices are as given in the following figures.

<p align="center">
<img src=/home/tathagato/classes/2024_25/DSE1/DES-AES/sbox_1_5.png
alt="S-Box 1 to 5 of DES algorithm">
</p>

<p align="center">
<img src=/home/tathagato/classes/2024_25/DSE1/DES-AES/sbox_6_8.png
alt="S-box 6 to 8 of DES algorithm">
</p>

#### Summary of DES algorithm

Input : <br /> 
- 64-bit plaintext $PT$
- 64-bit key value $K_{gen}$

Output : <br />
- 64-bit ciphertext $CT$.

Steps :
1. $PT_{perm1} = PTPerm_1(PT)$; // $PTPerm_1$ *denotes the  initial permutation of plaintext*
2. $K_{p1}= KPermute_1(K_{gen})$ ; // $K_{p1}$ *is a 56-bit number after permuting and truncating bits* $8,16,\cdots 64$ *of* $K_{gen}$ ;
3. $(L_0,R_0)$ = Leftmost 32 bits and rightmost 32 bits of $K_{p1}$ ;
4. Feistel stage 1 :
   - 4.1. $K_1$ = $KPermute_2(RotateLeftShift(K_{p1},1))$ ; // $K_1$ *is of 48-bit*
   - 4.2. $L_1 = R_0$
   - 4.3. $R^*_0 = PTPerm_2(R_0)$ ; // $R_0$ *is permuted and extended from 32 to 48 bits in* $PTPerm_2$
   - 4.4. $Y_0$ = $R^*_0 \oplus K_1$ ;
   - 4.5. $S_0 = Sbox(Y_0)$ ;
   - 4.6. $R_1 = L_0 \oplus S_0$ ;
5. Other Feistel stages 2 - 16 computed similar to 4.



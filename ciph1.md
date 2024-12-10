# Symmetric ciphering

Symmetric encryption, or secret key encrytion has five ingredients :
- Plaintext : Input data to encrypt
- Encryption Algorithm : Substitution or transformation over plaintext
- Secret key : Input to the encryption algorithm, independent of plaintext.
  Actually a parameter of the encryption algorithm.
- ciphertext : Output after enryption.
- Decryption algorithm : Essentially the encryption mechanism run in reverse 
  manner. Mathematically, decryption algorithm = inverse of encryption 
  algorithm.

In short, symmetric encryption means encryption with a secret key, and the same
secret key is used for decryption. Also the decryption process is inverse of 
encrytion process.

<p align="center">
<img src=/home/tathagato/classes/2024_25/DSE1/pic1.jpeg
alt="Smplified Model of symmetric ciphering">
</p>

Let $X$ be the plaintext, $K$ be the ciphering key, $E$ be the encryption 
algorithm, $Y$ be the ciphertext. Then $Y = E(K,X)$.


Decryption : $X=E^{-1}(K,Y)$ 

<p align="center">
<img src=/home/tathagato/classes/2024_25/DSE1/pic2.jpeg
alt="Cryptosystem model">
</p>

Two requierments for secure use of the secret-key (symmetric) encryption:
- Even if the attacker is in possession of a number of cyphertexts and the paintexts producing those ciphertexts.
- Sender and Receiver should obtain the key in a seured fashion.

## Elementary ciphering schemes
The elementary secret key ciphering agorithms perform substitution of each letter or a group of letters in the plaintext by some other letter or group of letters in the ciphertext. 

### Monoalphabetic substitution Cipher
In these ciphering algorithm, each individual letter or symbol in plaintext is replaced only by one other letter or symbol in the ciphertext irrespective of the position of the symbol in the plaintext stream. So the mapping between each plaintext symbol and ciphertext symbol is one-to-one.

For understanding these algorithms, let us take English text as example input. Let $N_p$, ($N_p \in \{0-25\}$) is the number for a letter in the plaintext (for example, $N_p = 0$ for A, $1$ for B and so on) and $N_c$ ($N_c \in \{0-25\}$) is the number of the letter in ciphertext which is replacing the plaintext letter numbered $N_p$.  

#### Caesar Cipher
Each letter in plaintext is numbered from 1 - 26 for English alphabet. Let $N_p$ be the number of letter in plaintext, it is replaced by the letter $N_c$ in ciphertext where

$N_c = (N_p + 3)~mod~26$ .

So, A in plaintext is replaced by D, B $\to$ E, C $\to$ F $\cdots$, X $\to$ A, Y $\to$ B and Z $\to$ C uniquely. As a generalization of Caesar cipher, the factor 3 can be generalized to a value $k$ ($k \in \{1 \cdots 25\}$). So the encryption function $E$ in generalized Caesar cipher is 

$N_c = (N_p + k)~mod~26$

and the decription function $E^{-1}$ is 

$N_p = (N_c - k)~mod~26$, where $k$ is the secret key to be known to the transmitter and receiver.

Now, let a sequence of ciphertext be available to n attacker or cryptanalyst. if he knows that the input is an English text, and the algorithm is a generalized Caesar cipher, he can potentially figure out the $k$ value by seeing repeated occurences of letters.

What can be done to make life a bit more difficult to the attacker ?

#### Affine Cipher

For Affine Cipher, the encryption is done as 

$N_c = (a * N_p + b)~mod~m$, where $a$ and $m$ are co-prime. For English plaintext where alphabsets are numbered between $\{0 \cdots 25\}$, $m = 26$. So the key value is $k = \{a,b\}$.

The decryption is done as 

$N_p = (a^{-1} * N_c - b)~mod~m$, where $a^{-1}$ is the multiplicative inverse of $a$ mod $m$, which means $a*a^{-1}~mod~m = 1$.

Calculation of $a^{-1}$ is done using extended eucledian algorithm. $a^{-1}$ exists onl if $a$ and $m$ are relatively prime to each other. For example, let $a = 15$. If we find the $gcd(15, 26)$ using eucledian method where $(q, r)$ are the quotients and remainders and in each step we write below :

$26/15~:~(1,11) \implies 26 = 1*15 + 11$, ------ (1)

$15/11~:~(1,4) \implies 15 = 1*11 + 4$,$\quad$   ------ (2)

$11/4~:~(2,3) \implies 11 = 2*4 + 3$,$\quad\quad$    ------ (3)

$4/3~:~(1,1) \implies 4 = 1*3 + 1$. $\quad\quad\quad$       ------ (4)

So, $gcd(15,26) = 1$.

Now, to get the multiplicative inverse of $15~mod~26$, we need to write $1$ as a linear combination of $15$ and $26$ to get the $(q,r)$ form. Let us start bottom-up as below :

Write $4$ as a remainder of $1$ divide by $3$. So if we write 1 as a linear combination of $3$ and $4$. Essentially we write the quotient of the division $4/3$ in terms of the dividend and divisor; i.e $4$ and $3$.

$4 = 1*3 + 1 \implies 1 = 4 - 1*3$. $\quad$    -------- (5)

Similarly replace the quotient $3$ from the division $11/4$ in terms of $11$ and $4$. <br /> 
From equation (3), $3=11-2*4$.       $\quad\quad$                       ------- (6) 

From (5) and (6), <br />
 $1 = 4 - 1*(11-2*4) = -1*11 + 3*4$. $\quad\quad$       ----------(7) 

Now replace quotient $4$ from division $15/11$. Equation (2) implies 4 = 15 - 1*11$. So, From (5), (6) and (7),<br />
$1 = -1*11 + 3*(15-1*11) = 3*15 - 4*11$. $\quad$---------- (8)

Now replace quotient $11$ from division $26/11$. So from equation (1), <br />$11 = 26 - 1*15$. $\quad\quad\quad\quad$------------------- (9).

So, from (8) and (9), <br /> 
$1 = 3*15 - 4*(26 - 1*15) = 7*15 - 4*26$.

Now the quotient of $15$ is $7$. Hence $7$ is the multiplicative inverse of $15$ as $15*7$ mod $26$ = $105$ mod $26$ = $1$.

It is possible that the inverse comes out to be negative; in that case the mod 26 value need to be considered.


#### Hill Cipher
This is a multiletter cipher, which takes m successive plaintext multiletter and generates m ciphertext letters. Each ciphertext letter is generated through a linear equation involving all input letters. For example, if three plaintext letters with numbers $p_1$, $p_2$ and $p_3$ are taken together, then

$c_1 = (k_{11}p_1 + k_{12}p_2 + k_{13}p_3)~mod~26$ <br />
$c_2 = (k_{21}p_1 + k_{22}p_2 + k_{23}p_3)~mod~26$ <br />
$c_3 = (k_{31}p_1 + k_{32}p_2 + k_{33}p_3)~mod~26$ <br />

So this system of linear equations can be written as 

$$
\begin{pmatrix}
c_1 \\
c_2  \\
c_3  \\
\end{pmatrix} = 
\begin{pmatrix}
k_{11} & k_{12} & k_{13} \\
k_{21} & k_{22} & k_{23} \\
k_{31} & k_{32} & k_{33} \\
\end{pmatrix}
\begin{pmatrix}
p_1 \\
p_2  \\
p_3  \\
\end{pmatrix}~mod~26 \\
$$
or $C$ = $KP~mod~26$ <br />
Hence $P$ = $K^{-1}C$

#### Playfair Cipher

This is the best known  multiple letter encryption cipher, which treats double-letters as one single plaintext unit or symbol and translates those units into ciphertext units or symbols. <br />
For English text, a 5X5 matrix is used to store the keywords and rest of the letters not present in the keyword. If the keyword is KEYWORD, then the storage matrix is as follows :

|K|E|Y|W|O|
|---|---|---|---|---|
|R|D|A|B|C|
|F|G|H|I/J|L|
|M|N|P|Q|S|
|T|U|V|X|Z|


Now, next question is how double letter plaintext units are encrypted to double letter ciphertext units. Some rules are followed, which are as below :<br />
1. Repeated letters in the double-letter plaintext unit is split into two double letter words using X normally. For example, SMOOTH is made as SM OX OT HX before ciphering.
2. If the two plaintext letters fall in the same row, the ciphertext contains the next letters of each of them in the same row using wraparound. For example, EY in the above table is ciphered as YW, WO is ciphered as OK, YO is ciphered as WK.
3. If the two plaintext letters fall in the same column, the ciphertext contains the next letters of each of them in the same column using wraparound.
4. Otherwise, each of the two plaintext letters is replaced by the letter in the same row of itself, and column of the other letter. For example, NO is replaced by SE in ciphertext; because N is in 4th row, 2nd column and O is in 1st row, 5th column. So replacement of N is S which is in 4th row, 5th column and replacement of O is E which is in 1st row, 2nd column.

Using this method, if we cipher WE ARE NOT GOODIES, then the ciphertext would be generated as follows :
- WE -> OY (Both in first row)
- AR -> BD (Both in 2nd row)
- EN -> DU (Both in 2nd column)
- OT -> KZ (elements 1,5 and 5,1 replaced by elements 11 and 55)
- GO -> LE (elements 32 and 15 replaced by elements 35 and 12)
- OD -> EC
- IE -> GW
- SX -> QZ

So the ciphertext would be OY BDD UKZ LEECGWQZ.

How to decrypt ?
- OY -> In the same row, so the plaintext pair would be the previous letter of each in the pair, so WE.
- BD-> Same row, so AR in the same way as the previous pair.
- DU -> Same column, so EN is the plaintext.
- KZ -> elements are 11 and 55 - so the plaintext elements are elements 15 and 51 -> OT .

### Polyalphabetic ciphers
Polyalphabetic ciphers provide better protection against replay attacks using correlation information from large amount of ciphertext, because mapping between one plaintext symbol to a ciphertext symbol is not static. Some examples are shown below.

#### Vigenere cipher
This is the simplest polyalphabetic ciphering technique and very easy to implement. This method is based on arranging the letters of the alphabet in a matrix and  calculate row-column numbers of the replacement letter in ciphertext based on the cipherkey and plaintext. The matrix is called Vigenere matrix which is shown below.

<p align="center">
<img src=/home/tathagato/classes/2024_25/DSE1/vigenere_table.jpeg
alt="vigenere_table">
</p>

As an example, take the cipher key as "CIPHERKEY" and the plaintext as "PLAINTEXT". The replacement of P is the element in column C and row P, which is "R". Similarly replacement of "L" is the element in column I and row L, which is "T". Similarly, other replacement elements are found, and the ciphertext becomes RTPPRKOBR. It is notable that P, N and T in plaintext is replaced by R is ciphertext.<br />
In case cipher key is smaller than plaintext in length, the cipher key can be repeated to the required length. This perodic nature can be eliminated if cipher key is made up to the length of plaintext in a non-repeatative manner. One common way is to append part of plaintext to the cipherkey to provide a running key.  

#### Vernam Cipher
This method assigns an unique number to each letter of plaintext, an unique number to letters of cipherkey and perform bitwise XOR between those numbers. This method works perfectly for ASCII, extended ASCII or unicode representation of texts.  
The system can be represented as follows : <br />
Let $p_i$ be the $i^{th}$ bit of the plaintext,<br />
$c_i$ be the $i^{th}$ bit of the ciphertext,<br />
$k_i$ be the $i^{th}$ bit of the cipher key. <br />

$c_i = p_i~XOR~k_i$

For decipering, <br />
$p_i = c_i~XOR~k_i$

This kind of ciphering is strongest when length of cipherkey is equal to the length of plaintext. Following techniques are employed to generate long ciperkey from a short one : <br />
- the short ciphertext is prepended to the portion of plaintext to get long cipherkey; or
- short cipherkey is repeated multiple times to generate long cipherkey, or
- short cipherkey is appended with rotated versions of the short cipherkey.  

### Transposition techniques

In these techniques, the letters in plaintext are shuffled in various ways to generate ciphertext.

#### Rail-Fence cipher
A very elementary transposition cipher technique. In a 2-stage Rail-Fence cipher, the input plaintext is written as below :<br />
If plaintext is WE ARE VERY NAUGHTY,  it is written as <br />
$$
\begin{matrix} 
W~~~A~~~E~~~E~~~Y~~~A~~~G~~~T \\
~~~~~~~~E~~~R~~~V~~~R~~~N~~~U~~~H~~~Y \\
\end{matrix}
$$
The ciphertext would be generated 
by reading the letters row-wise; hence the output for this example would be <br />
WA EEY AGTE RVRNUHY .
Number of levels can be increased to make the crypananlysis bit more difficult.

#### Transposition Cipher
In this scheme, plaintext letters are written row-wise in a rectangular matrix, and they are read column-wise to generate ciphertext, but column numbers are shuffled randomly. As an example, <br />
Let the plaintext be PLEASEDONOTATTACKME, which is read row-wise into a 4X7 rectangular matrix but columns are shuffled as column 5, 2, 3, 1, 7, 4, 6. The populated matrix would look like <br />

$$
\begin{matrix}
5~~~~2~~~~3~~~~1~~~~7~~~~4~~~~6 \\
~P~~~L~~~E~~~A~~~S~~~E~~~D \\
~O~~~N~~~O~~~T~~~A~~~T~~~T \\
~A~~~C~~~K~~M~~E~~X~~X \\
\end{matrix}
$$
Now the ciphertext is generated by reading column by column starting from 1st one in sequence. So the ciphertext is <br />
ATMLNCEOKETXPOADTXSAE.<br />
To make the ciphertext more rebust, double transposition is used, where the ciphertext generated out of first transposition is fed into the second transposition as plaintext, and the ciphertext from second transposition is tansmitted as cipherkey.

#### Rotor Machine cipher
This is a type of multistage transposition cipher, where
the transposition patterns of different stages change in a similar way as rotor machines. It can be illustrated as below with an example of 2-stage transposition.
Let the symbol space contain 10 symbols : A - J. The transposition pattern of 1st stage is :<br />

$$
\begin{matrix}
Stage~1\\
A~~~~B~~~~C~~~~D~~~~E~~~~F~~~~G~~~~H~~~~I~~~~J \\
1~~~~~2~~~~~3~~~~~4~~~~~5~~~~~6~~~~~7~~~~~8~~~~~9~~~~10 \\
4~~~~~6~~~~~7~~~~~1~~~~~10~~~~~8~~~~~2~~~~~5~~~~~3~~~~~9 \\
Stage~2 \\
1~~~~~2~~~~~3~~~~~4~~~~~5~~~~~6~~~~~7~~~~~8~~~~~9~~~~10 \\
9~~~~~5~~~~~1~~~~~8~~~~~2~~~~~1~~~~~3~~~~~6~~~~~4~~~~~7 \\
A~~~~B~~~~C~~~~D~~~~E~~~~F~~~~G~~~~H~~~~I~~~~J \\
\end{matrix}
$$ 

In this state of transposition matrices, pos $1$ of input of $1^{st}$ stage is shifted to pos $4$ in the input of $2^{nd}$ stage. Pos $4$ of input in the $2^{nd}$ stage is mapped to position $8$ of the output of 2nd stage, where the symbol is E. So input symbol A is mapped to I, symbol B is mapped to J, C is mapped to A ... etc. 

The first stage mapping cyclically shifts by one position after every input, and mapping of the 2nd position shifts by one position each time the mapping of the fist stage wraps around. Hence, the mapping rule changes with every input. The stages after one shift of first stage is shown below.

$$
\begin{matrix}
Stage~1\\
A~~~~B~~~~C~~~~D~~~~E~~~~F~~~~G~~~~H~~~~I~~~~J \\
10~~~~~1~~~~~2~~~~~3~~~~~4~~~~~5~~~~~6~~~~~7~~~~~8~~~~9 \\
~~9~~~~~~4~~~~~6~~~~~7~~~~~1~~~~10~~~~8~~~~2~~~~~5~~~~~3 \\
Stage~2 \\
1~~~~~2~~~~~3~~~~~4~~~~~5~~~~~6~~~~~7~~~~~8~~~~~9~~~~10 \\
9~~~~~5~~~~10~~~~8~~~~~2~~~~1~~~~~3~~~~~6~~~~~4~~~~~7 \\
~A~~~~B~~~~C~~~~D~~~~E~~~~F~~~G~~~~H~~~~I~~~~J \\
\end{matrix}
$$ 

So, encryption of the plaintext AA involves first 'A' getting encrypted using initial states of two transposition matrices, and the second 'A' with shifted version of matrix 1 and same matrix 2. Hence, <br />
'A' : 1st pos of stage 1 input : 4th pos of stage 2 input of stage 1 -> 9th positon of stage 2 output : 'I' <br />
'A' : 10th pos of stage 1 input -> 6th pos in stage 2 input->8th position of stage 2 output : 'H'.  <br />
So AA -> IH.

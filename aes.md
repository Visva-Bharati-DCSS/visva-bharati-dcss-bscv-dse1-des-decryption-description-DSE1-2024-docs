
---
header-includes:
  - \usepackage[ruled,vlined,linesnumbered]{algorithm2e}
---
# AES encryption and Decryption

AES is another block cipher mechanism where plaintext block length = 128 bit,
and the keysize can be either 128-bit, 192-bit or 256 bits. AES has multiple 
processing stages - and number of processing stages vary alongwith the keysize.
The following table catures the possible plaintext, cipherkey and number of 
stages. Size of ciphertext = 128 bits.

| plaintext block size | cipherkey size | number of stages |
| --- | --- | --- |
| 128 bits | 128 bits | 10 |
| 128 bits | 192 bits | 12 |
| 128 bits | 256 bits | 14 |

The following figure shows a block diagram of AES encryption and Decryption
process. 
 
<p align="center">
<img src=/home/tathagato/classes/2024_25/DSE1/DES-AES/Block-diagram-for-AES-encryption-and-decryption.png
alt="Block diagram of AES algorithm">
</p>

The AES encryption algorithm is as follows : <br />
'''latex
# Algorithm 1
Just a sample algorithmn
\begin{algorithm}[H]
\DontPrintSemicolon
\SetAlgoLined
\KwResult{Write here the result}
\SetKwInOut{Input}{Input}\SetKwInOut{Output}{Output}
\Input{Write here the input}
\Output{Write here the output}
\BlankLine
\While{While condition}{
    instructions\;
    \eIf{condition}{
        instructions1\;
        instructions2\;
    }{
        instructions3\;
    }
}
\caption{While loop with If/Else condition}
\end{algorithm} 



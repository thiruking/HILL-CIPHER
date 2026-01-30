## NAME : THIRUMALAI K
## DATE : 30/01/2026
## REG NO : 212224240176
## DEPT : AIML
# HILL CIPHER
HILL CIPHER
EX. NO: 3 AIM:
 

IMPLEMENTATION OF HILL CIPHER
 
## To write a C program to implement the hill cipher substitution techniques.

## DESCRIPTION:

Each letter is represented by a number modulo 26. Often the simple scheme A = 0, B
= 1... Z = 25, is used, but this is not an essential feature of the cipher. To encrypt a message, each block of n letters is  multiplied by an invertible n × n matrix, against modulus 26. To
decrypt the message, each block is multiplied by the inverse of the m trix used for
 
encryption. The matrix used
 
for encryption is the cipher key, and it sho
 
ld be chosen
 
randomly from the set of invertible n × n matrices (modulo 26).


## ALGORITHM:

STEP-1: Read the plain text and key from the user. 
STEP-2: Split the plain text into groups of length three. 
STEP-3: Arrange the keyword in a 3*3 matrix.
STEP-4: Multiply the two matrices to obtain the cipher text of length three.
STEP-5: Combine all these groups to get the complete cipher text.

## PROGRAM 
```C
#include <stdio.h>
#include <string.h>
#include <ctype.h>

/* Key Matrix */
int keymat[3][3] = {
    {1, 2, 1},
    {2, 3, 2},
    {2, 2, 1}
};

/* Inverse Key Matrix */
int invkeymat[3][3] = {
    {-1, 0, 1},
    { 2,-1, 0},
    {-2, 2,-1}
};

char key[] = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";

/* Encode Function */
char *encode(char a, char b, char c)
{
    static char ret[4];
    int x, y, z;

    int posa = a - 65;
    int posb = b - 65;
    int posc = c - 65;

    x = posa * keymat[0][0] + posb * keymat[1][0] + posc * keymat[2][0];
    y = posa * keymat[0][1] + posb * keymat[1][1] + posc * keymat[2][1];
    z = posa * keymat[0][2] + posb * keymat[1][2] + posc * keymat[2][2];

    ret[0] = key[x % 26];
    ret[1] = key[y % 26];
    ret[2] = key[z % 26];
    ret[3] = '\0';

    return ret;
}

/* Decode Function */
char *decode(char a, char b, char c)
{
    static char ret[4];
    int x, y, z;

    int posa = a - 65;
    int posb = b - 65;
    int posc = c - 65;

    x = posa * invkeymat[0][0] + posb * invkeymat[1][0] + posc * invkeymat[2][0];
    y = posa * invkeymat[0][1] + posb * invkeymat[1][1] + posc * invkeymat[2][1];
    z = posa * invkeymat[0][2] + posb * invkeymat[1][2] + posc * invkeymat[2][2];

    ret[0] = key[(x % 26 + 26) % 26];
    ret[1] = key[(y % 26 + 26) % 26];
    ret[2] = key[(z % 26 + 26) % 26];
    ret[3] = '\0';

    return ret;
}

/* Main Function */
int main()
{
    char msg[1000];
    char enc[1000] = "";
    char dec[1000] = "";
    int n;

    printf("Simulation of Hill Cipher\n");
    printf("Enter the message: ");
    scanf("%s", msg);

    /* Convert to Uppercase */
    for (int i = 0; i < strlen(msg); i++)
        msg[i] = toupper(msg[i]);

    /* Padding with X */
    n = strlen(msg) % 3;
    if (n != 0)
    {
        for (int i = 0; i < 3 - n; i++)
            strcat(msg, "X");
    }

    printf("Padded message : %s\n", msg);

    /* Encoding */
    for (int i = 0; i < strlen(msg); i += 3)
        strcat(enc, encode(msg[i], msg[i+1], msg[i+2]));

    printf("Encoded message : %s\n", enc);

    /* Decoding */
    for (int i = 0; i < strlen(enc); i += 3)
        strcat(dec, decode(enc[i], enc[i+1], enc[i+2]));

    printf("Decoded message : %s\n", dec);

    return 0;
}
```

## OUTPUT
<img width="568" height="234" alt="image" src="https://github.com/user-attachments/assets/142dd9b3-5f09-48a4-9149-d32071e4f0ea" />


## RESULT

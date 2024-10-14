# Ex 9 - RSA Encryption Algorithm
## Aim
To implement the RSA encryption algorithm to encrypt and decrypt a given message using two prime numbers for key generation.

## Algorithm
### Input two prime numbers p and q:
Choose two distinct prime numbers to generate the RSA keys.

### Calculate n and t:
Compute n = p * q, where n is the modulus for both the public and private keys.

Compute Euler’s Totient t = (p - 1) * (q - 1).

### Choose the public key e:
Select an integer e such that 1 < e < t and gcd(e, t) = 1.

### Compute the private key d:
Compute the modular multiplicative inverse of e mod t, i.e., find d such that (e * d) % t = 1.

### Encrypt the message:
Convert the message into its ASCII equivalent.

For each character, perform encryption using the formula C = (M^e) % n, where M is the ASCII value of the character and C is the encrypted character.

### Decrypt the message:
For each encrypted character, perform decryption using the formula M = (C^d) % n, where M is the original message character.

Display the encrypted and decrypted messages.

## Program
```
#include <stdio.h>
#include <stdlib.h>
#include <math.h>
#include <string.h>

long int p, q, n, t, e, d, temp[100], m[100], en[100], i;
char msg[100];

int is_prime(long int pr) {
    for (int i = 2; i <= sqrt(pr); i++) {
        if (pr % i == 0)
            return 0;
    }
    return 1;
}

long int mod_inverse(long int e, long int t) {
    long int k = 1;
    while (1) {
        k += t;
        if (k % e == 0)
            return k / e;
    }
}

void encrypt() {
    long int pt, ct, key = e, k;
    for (i = 0; i < strlen(msg); i++) {
        pt = m[i] - 96;
        k = 1;
        for (int j = 0; j < key; j++) {
            k = (k * pt) % n;
        }
        temp[i] = k;
        en[i] = k + 96;
    }
    en[i] = -1;
    printf("\nENCRYPTED MESSAGE:\n");
    for (i = 0; en[i] != -1; i++) {
        printf("%c", (char)en[i]);
    }
}

void decrypt() {
    long int pt, ct, key = d, k;
    for (i = 0; en[i] != -1; i++) {
        ct = temp[i];
        k = 1;
        for (int j = 0; j < key; j++) {
            k = (k * ct) % n;
        }
        pt = k + 96;
        m[i] = pt;
    }
    m[i] = -1;
    printf("\nDECRYPTED MESSAGE:\n");
    for (i = 0; m[i] != -1; i++) {
        printf("%c", (char)m[i]);
    }
}

int main() {
    printf("Ex 9 - RSA Encryption Algorithm\n");
    printf("ENTER FIRST PRIME NUMBER: ");
    scanf("%ld", &p);
    if (!is_prime(p)) {
        printf("WRONG INPUT\n");
        return 1;
    }

    printf("ENTER SECOND PRIME NUMBER: ");
    scanf("%ld", &q);
    if (!is_prime(q) || p == q) {
        printf("WRONG INPUT\n");
        return 1;
    }

    printf("ENTER MESSAGE: ");
    scanf(" %[^\n]s", msg);
    for (i = 0; i < strlen(msg); i++)
        m[i] = msg[i];

    n = p * q;
    t = (p - 1) * (q - 1);

    for (e = 2; e < t; e++) {
        if (is_prime(e) && t % e != 0)
            break;
    }

    d = mod_inverse(e, t);

    encrypt();
    decrypt();

    return 0;
}
```
## Output
![image](https://github.com/user-attachments/assets/9e65be53-09e9-4126-b220-0ad0099cc702)

## Result
Thus RSA encryption algorithm to encrypt and decrypt a given message using two prime numbers for key generation has been successfully implemented.

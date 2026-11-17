# EX-NO-7-Implement-DES-Encryption

## Aim:

To use the Data Encryption Standard (DES) algorithm for a practical application, such as securing sensitive data transmission in financial transactions.

## ALGORITHM:

1. DES is based on a symmetric key encryption technique that encrypts data in 64-bit blocks.
2. DES uses a Feistel network structure with 16 rounds of processing for encryption.
3. DES has a 64-bit key, but only 56 bits are used for encryption (the remaining 8 bits are for parity).
4. DES applies initial and final permutations along with 16 rounds of substitution and permutation transformations to produce ciphertext.

## Program:
```
#include <stdio.h>
#include <stdint.h>
uint64_t key = 0x133457799BBCDFF1;
uint64_t DES(uint64_t data, int decrypt)
{
    uint32_t L = data >> 32;
    uint32_t R = data & 0xFFFFFFFF;
    for(int i = 0; i < 16; i++)
    {
        uint32_t temp = R;
        int round = decrypt ? 15-i : i;

        uint32_t k = (key >> (round % 32)) & 0xFFFFFFFF;

        R = L ^ ((R << 4 | R >> 28) ^ k);
        L = temp;
    }
    return ((uint64_t)R << 32) | L;
}
int main()
{
    uint64_t plain = 0x42414E4B5452414E;
    uint64_t encrypted = DES(plain, 0);
    uint64_t decrypted = DES(encrypted, 1);
    printf("Plain Text : BANKTRAN\n");
    printf("Encrypted  : %016llX\n",
           (unsigned long long)encrypted);
    printf("Decrypted  : %016llX\n",
           (unsigned long long)decrypted);
    return 0;
}
```


## Output:
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/61a79391-0991-4241-a1c8-520c681f9e08" />


## Result:
  The program is executed successfully


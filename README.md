# VIGENERE-CIPHER
## EX. NO: 4
 

## IMPLEMETATION OF VIGENERE CIPHER
 

## AIM:

To implement the Vigenere Cipher substitution technique using C program.

## DESCRIPTION:

To encrypt, a table of alphabets can be used, termed a tabula recta, Vigenère square,or Vigenère table. It consists of the alphabet written out 26 times in differnt rows, each
 
alphabet shifted cyclically to the left compared to the previous alphabet, corresponding to the 26 possible Caesar ciphers. At different points in the encryption process, the cipher uses adifferent alphabet from one of the rows. The alphabet used at each point repeating keyword.depends on a Each row starts with a key letter. The remainder of the row holds the letters A to Z. Although there are 26 key rows shown, you will only use as many keys as there are unique letters in the key string, here just 5 keys, {L, E, M, O, N}. For successive letters of the message, we are going to take successive letters of the key string, and encipher each message letter using its corresponding key row. Choose the next letter of the key, go along that row to find the column heading that	atches the message character; the letter at the intersection of
[key-row, msg-col] is the enciphered letter.


## ALGORITHM:

STEP-1: Arrange the alphabets in row and column of a 26*26 matrix.
STEP-2: Circulate the alphabets in each row to position left such that the first letter is attached to last.
STEP-3: Repeat this process for all 26 rows and construct the final key matrix.
STEP-4: The keyword and the plain text is read from the user.
STEP-5: The characters in the keyword are repeated sequentially so as to match with that of the plain text.
STEP-6: Pick the first letter of the plain text and that of the keyword as the row indices and column indices respectively.
STEP-7: The junction character where these two meet forms the cipher character.
STEP-8: Repeat the above steps to generate the entire cipher text.


## PROGRAM
```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <ctype.h>

#define MAX_LEN 1024

// Validates that the key contains only alphabetic characters
int is_valid_key(const char *key) {
    if (strlen(key) == 0) return 0;
    for (size_t i = 0; key[i] != '\0'; i++) {
        if (!isalpha((unsigned char)key[i])) return 0;
    }
    return 1;
}

// Strips newline character left by fgets
void strip_newline(char *str) {
    size_t len = strlen(str);
    if (len > 0 && str[len - 1] == '\n') {
        str[len - 1] = '\0';
    }
}

void vigenere(char *text, const char *key, int encrypt) {
    size_t key_len = strlen(key);
    size_t key_idx = 0;
    int direction = encrypt ? 1 : -1;

    for (size_t i = 0; text[i] != '\0'; i++) {
        if (isalpha((unsigned char)text[i])) {
            char base = isupper((unsigned char)text[i]) ? 'A' : 'a';
            int shift = toupper((unsigned char)key[key_idx % key_len]) - 'A';

            int offset = (text[i] - base) + (direction * shift);
            text[i] = base + ((offset % 26 + 26) % 26);

            key_idx++;
        }
    }
}

int main(void) {
    char text[MAX_LEN];
    char key[MAX_LEN];
    char mode_input[10];
    int encrypt = 1;

    printf("=== Vigenère Cipher ===\n");

    // Input text
    printf("Enter your text: ");
    if (fgets(text, sizeof(text), stdin) == NULL) return 1;
    strip_newline(text);

    // Input key
    while (1) {
        printf("Enter key (letters only): ");
        if (fgets(key, sizeof(key), stdin) == NULL) return 1;
        strip_newline(key);

        if (is_valid_key(key)) break;
        printf("Invalid key! Only alphabetic characters allowed.\n");
    }

    // Input operation
    while (1) {
        printf("Do you want to (E)ncrypt or (D)ecrypt? ");
        if (fgets(mode_input, sizeof(mode_input), stdin) == NULL) return 1;
        strip_newline(mode_input);

        char c = tolower((unsigned char)mode_input[0]);
        if (c == 'e') {
            encrypt = 1;
            break;
        } else if (c == 'd') {
            encrypt = 0;
            break;
        }
        printf("Invalid choice. Enter 'E' or 'D'.\n");
    }

    // Process in-place
    vigenere(text, key, encrypt);

    printf("\nResult (%sed): %s\n", encrypt ? "encrypt" : "decrypt", text);

    return 0;
}
```
## OUTPUT
<img width="390" height="142" alt="image" src="https://github.com/user-attachments/assets/af5ca4c3-6b52-4101-b84e-25a8ec2386f5" />

## RESULT

Thus the program for vigenere cipher is successfully implemented using C program.

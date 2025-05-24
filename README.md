## EX. NO:2 IMPLEMENTATION OF PLAYFAIR CIPHER

 # AIM :
To implement a program to encrypt a plain text and decrypt a cipher text using
play fair Cipher substitution technique.
# DESIGN STEPS :
Step 1:
Design of PlayFair Cipher algorithnm
Step 2:
Implementation using C or pyhton code
Step 3:
1. Create a 5x5 table using a keyword, filling the table with unique letters from
the keyword first, then the remaining letters of the alphabet (usually
omitting "Q" or combining "I" and "J").
2. Break the plaintext into digrams (pairs of two letters). If a pair has two
identical letters, insert an "X" between them. If the message length is odd,
add an "X" at the end.
3. If both letters of the digram appear in the same row, replace them with the
letters immediately to their right, wrapping around if needed.
4. If both letters appear in the same column, replace them with the letters
immediately below, wrapping around to the top if necessary.
5. If the letters are in different rows and columns, form a rectangle and replace
the letters with the opposite corners of the rectangle, keeping the same row
for each letter.
6. To decrypt, reverse the second, third, and fourth rules while keeping the first
rule the same. Drop any unnecessary "X"s added during encryption.

# PROGRAM:
```
#include<stdio.h>
#include<string.h>
#include<ctype.h>
#define MX 5
void playfair(char ch1, char ch2, char key[MX][MX])
{
int i, j, w, x, y, z;
FILE *out;
if ((out = fopen("cipher.txt", "a+")) == NULL)
{
printf("File Corrupted.");
}
for (i = 0; i < MX; i++)
{
for (j = 0; j < MX; j++)
{
if (ch1 == key[i][j])
{
w = i;
x = j;
}
else if (ch2 == key[i][j])
{
y = i;
z = j;
}
}
}
if (w == y)
{
x = (x + 1) % 5;
z = (z + 1) % 5;
printf("%c%c", key[w][x], key[y][z]);
fprintf(out, "%c%c", key[w][x], key[y][z]);
}
else if (x == z)
{
w = (w + 1) % 5;
y = (y + 1) % 5;
printf("%c%c", key[w][x], key[y][z]);
fprintf(out, "%c%c", key[w][x], key[y][z]);
}
else
{
printf("%c%c", key[w][z], key[y][x]);
fprintf(out, "%c%c", key[w][z], key[y][x]);
}
fclose(out);
}
int main()
{
int i, j, k = 0, l, m = 0, n;
char key[MX][MX], keyminus[25], keystr[10], str[25] = {0};
char alpa[26] = {'A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S',
'T', 'U', 'V', 'W', 'X', 'Y', 'Z'};
printf("\nEnter key: ");
fgets(keystr, sizeof(keystr), stdin);
keystr[strcspn(keystr, "\n")] = 0; // Remove newline character
printf("\nEnter the plain text: ");
fgets(str, sizeof(str), stdin);
str[strcspn(str, "\n")] = 0; // Remove newline character
n = strlen(keystr);
for (i = 0; i < n; i++)
{
if (keystr[i] == 'j') keystr[i] = 'i';
else if (keystr[i] == 'J') keystr[i] = 'I';
keystr[i] = toupper(keystr[i]);
}
for (i = 0; i < strlen(str); i++) {
if (str[i] == 'j') str[i] = 'i';
else if (str[i] == 'J') str[i] = 'I';
str[i] = toupper(str[i]);
}
j = 0;
for (i = 0; i < 26; i++)
{
for (k = 0; k < n; k++)
{
if (keystr[k] == alpa[i]) break;
else if (alpa[i] == 'J') break;
}
if (k == n)
{
keyminus[j] = alpa[i];
j++;
}
}
k = 0;
for (i = 0; i < MX; i++)
{
for (j = 0; j < MX; j++)
{
if (k < n)
{
key[i][j] = keystr[k];
k++;
}
else
{
key[i][j] = keyminus[m];
m++;
}
printf("%c ", key[i][j]);
}
printf("\n");
}
printf("\n\nEntered text :%s\nCipher Text :",str);
for (i = 0; i < strlen(str); i++)
{
if (str[i] == 'J') str[i] = 'I';
if (str[i + 1] == '\0') playfair(str[i], 'X', key);
else
{
if (str[i + 1] == 'J') str[i + 1] = 'I';
if (str[i] == str[i + 1]) playfair(str[i], 'X', key);
else
{
playfair(str[i], str[i + 1], key);
i++;
}
}
}
printf("\nDecrypted text:%s",str);
return 0;
}
```
# OUTPUT:
![image](https://github.com/user-attachments/assets/9b301add-be31-476c-a9cf-ab712986aa22)

# RESULT:
The program is executed successfully

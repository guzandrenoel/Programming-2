# CType Functions in C (Character Handling)

## Overview

The **ctype library** in C provides functions used to **test** and **manipulate characters**.  
These functions are commonly used for **input validation**, **text processing**, and **character classification**.

All ctype functions work on **characters** (typically `char`) and are defined in:

```c
#include <ctype.h>
```

## Character Testing Functions

These functions return **non-zero (true)** if the condition is met, otherwise **0 (false)**.

| Function     | Description                                 |
| ------------ | ------------------------------------------- |
| `isalpha(c)` | Checks if `c` is a letter (A–Z or a–z)      |
| `isdigit(c)` | Checks if `c` is a digit (0–9)              |
| `isalnum(c)` | Checks if `c` is a letter or digit          |
| `islower(c)` | Checks if `c` is a lowercase letter         |
| `isupper(c)` | Checks if `c` is an uppercase letter        |
| `isspace(c)` | Checks for whitespace (space, tab, newline) |
| `ispunct(c)` | Checks if `c` is a punctuation character    |
| `isprint(c)` | Checks if `c` is printable                  |
| `iscntrl(c)` | Checks if `c` is a control character        |


## Character Conversion Functions

These functions convert characters between letter cases.

| Function     | Description                            |
| ------------ | -------------------------------------- |
| `tolower(c)` | Converts uppercase letter to lowercase |
| `toupper(c)` | Converts lowercase letter to uppercase |

### Example: Checking Character Type

```c
#include <stdio.h>
#include <ctype.h>

int main() {
    char ch = 'A';

    if (isalpha(ch)) {
        printf("%c is a letter\n", ch);
    }

    if (isupper(ch)) {
        printf("%c is uppercase\n", ch);
    }

    return 0;
}

// Output:
// A is a letter
// A is uppercase

```

### Example: Converting Case

```c
#include <stdio.h>
#include <ctype.h>

int main() {
    char letter = 'g';

    letter = toupper(letter);
    printf("Uppercase: %c\n", letter);

    return 0;
}

// Output: Uppercase: G

```

### Example: Validating User Input

```c
#include <stdio.h>
#include <ctype.h>

int main() {
    char input;

    printf("Enter a character: ");
    scanf(" %c", &input);

    if (isdigit(input)) {
        printf("You entered a digit.\n");
    } else if (isalpha(input)) {
        printf("You entered a letter.\n");
    } else {
        printf("You entered a special character.\n");
    }

    return 0;
}

// Sample Output:
// Enter a character: A
// You entered a letter.

```
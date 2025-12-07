---
layout: default
title: "[42 Common Cursus Exam02] C: rev_wstr – Reverse Words in a String"
categories: 42Exam
tag: [C, 42, Exam, String, Algorithm]
toc: true
---

# 42 Exam02: `rev_wstr`

![42Exam](/assets/images/2025-12-07-first/first.png)


This post summarizes the classic **rev_wstr** problem from **42 Exam02**, one of the most common string‑manipulation exercises in the exam.
It tests understanding of indexing, word boundaries, minimal library usage, and careful iteration using only `write`, `malloc`, and `free`.


## Problem Description (Official Subject)

```txt
Assignment name  : rev_wstr
Expected files   : rev_wstr.c
Allowed functions: write, malloc, free

Write a program that takes a string as a parameter, and prints its words in
reverse order.

A "word" is a part of the string bounded by spaces and/or tabs, or the
begin/end of the string.

If the number of parameters is different from 1, the program will display
'\n'.

In the parameters that are going to be tested, there won't be any "additional"
spaces (meaning that there won't be additionnal spaces at the beginning or at
the end of the string, and words will always be separated by exactly one space).

Examples:

$> ./rev_wstr "You hate people! But I love gatherings. Isn't it ironic?" | cat -e
ironic? it Isn't gatherings. love I But people! hate You$
$>./rev_wstr "abcdefghijklm"
abcdefghijklm
$> ./rev_wstr "Wingardium Leviosa" | cat -e
Leviosa Wingardium$
$> ./rev_wstr | cat -e
$
$>
```


## Requirements Summary

* The program must receive **exactly one argument** (the input string).
* A **word** is a maximal sequence of characters that are **not** spaces `' '` or tabs `\t`.
* Input used for testing will **not** contain extra spaces:

  * No leading or trailing spaces
  * Exactly one space between words
* If `argc != 2`, the program must print **only a newline** and exit.
* The goal is to **reverse the order of the words** without changing the characters inside each word.

Example transformation:

* Input: `"A B C"`
* Output: `"C B A"`


## Example Inputs and Outputs

### Example 1

```bash
$> ./rev_wstr "You hate people! But I love gatherings. Isn't it ironic?" | cat -e
ironic? it Isn't gatherings. love I But people! hate You$
```

### Example 2

```bash
$> ./rev_wstr "abcdefghijklm"
abcdefghijklm
```

Only one word is present, so the output is identical to the input.

### Example 3

```bash
$> ./rev_wstr "Wingardium Leviosa" | cat -e
Leviosa Wingardium$
```

Two words, reversed.

### Example 4

```bash
$> ./rev_wstr | cat -e
$
```

No argument is given, so the program prints only a newline.


## Approach and Idea

We must:

1. Check the argument count.
2. If `argc == 2`, process `argv[1]`.
3. Traverse the string **from the end to the beginning**.
4. For every word found from right to left:

   * Detect the **end index** of the word.
   * Move left until reaching a space or the beginning → this is the **start index**.
   * Print the substring `[start, end]` using `write`.
   * If there are more words to come, print a space.
5. Finish by printing a newline.

A simple helper like `is_space()` makes it easier to treat both `' '` and `\t` as separators.
Using `ft_strlen()` allows us to start from the last valid index of the string.

This algorithm works in a **single pass from right to left** and does not require extra memory, which is perfect for exam constraints.


## Final C Implementation (Exam‑Ready)

```c
#include <unistd.h>
#include <stdlib.h>

int is_space(char c)
{
    return (c == ' ' || c == '\t');
}

int ft_strlen(const char *str)
{
    int i = 0;
    while (str[i])
        i++;
    return (i);
}

int main(int argc, char **argv)
{
    if (argc == 2)
    {
        int i = ft_strlen(argv[1]) - 1;

        while (i >= 0)
        {
            /* Skip trailing spaces/tabs if any */
            while (i >= 0 && is_space(argv[1][i]))
                i--;

            if (i < 0)
                break;

            /* Mark the end of the current word */
            int end = i;

            /* Move left until just before the word (or beginning of string) */
            while (i >= 0 && !is_space(argv[1][i]))
                i--;

            int start = i + 1;

            /* Print the word: from start to end */
            write(1, argv[1] + start, end - start + 1);

            /* If there are more words before this one, print a space */
            if (i >= 0)
                write(1, " ", 1);
        }
    }

    write(1, "\n", 1);
    return (0);
}
```


## Notes and Common Pitfalls

* **Off‑by‑one errors** are very common in this problem:

  * Make sure you correctly handle `start` and `end` indices.
  * Don’t forget that `ft_strlen()` returns the **length**, so the last valid index is `len - 1`.
* Always handle the case where the string might consist of **only one word**.
* Respect the exam’s constraints:

  * Only `write`, `malloc`, and `free` are allowed.
  * Do not use any other standard library functions (`printf`, `strlen`, etc.).
* The subject guarantees no extra spaces at the beginning or end of the string in the tests, but the backward loop is robust enough to handle trailing spaces as well.


## Takeaways

* Scanning the string **backwards** is a powerful technique for reversing word order.
* This exercise is very representative of 42 exam style
  * Minimal allowed functions
  * Manual index and boundary management
  * Edge‑case handling (no argument, single word, multiple words)
* Once you are comfortable with this pattern, similar problems like `rostring` or other word‑rearranging exercises will feel much easier.



That’s it for the **`rev_wstr`** write‑up.
You can drop this file directly into your Jekyll blog as a post and use it as a reference before your next 42 Exam02 session.

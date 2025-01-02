---
layout: single
title:  "[CodingTest] Printing a String in Java"
categories: CodingTest
tag: [CS, Java, Programming, Input/Output]
toc: true
---

![Codingtest]({{site.urls}}/assets/images/2024-08-28-PrintingaStringinJava/2.png)

# Printing a String in Java

### Problem Description

In this post, we'll explore how to take a string as input and print it in Java. This is a fundamental exercise in understanding basic input/output operations in Java programming.

**Problem Statement**

Given a string `str`, write a program that reads the string and prints it.

**Constraints**

- The length of `str` is between 1 and 1,000,000 characters.
- The string `str` contains no spaces and is provided in a single line.

### Example Input and Output

**Example Input**

```
Input #1:

HelloWorld!
```

**Example Output**

```
Output #1:

HelloWorld!
```

### Java Code Implementation

<details>
    <summary>Details</summary>

<pre><code>

import java.util.Scanner;

public class Solution {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in); // Step 1: Create a Scanner object to read input
        String a = sc.next();               // Step 2: Read a single word (without spaces) from the input
        System.out.println(a);              // Step 3: Print the input string
    }
}

</code></pre>

</details>

### Code Explanation

<details>
    <summary>Details</summary>
1. Scanner sc = new Scanner(System.in);
<br>
Here, we create an instance of the Scanner class, named sc, which reads from the standard input (System.in). This allows us to take input from the user.
<br>
<br>
2. String a = sc.next();
<br>
This line reads the next token of input as a string. The next() method of Scanner reads input until a space is encountered, making it ideal for reading a single word.
<br>
<br>
3. System.out.println(a);
<br>
Finally, this line prints the string a to the console. The println method is used to print the output followed by a newline.
<br>
<br>
</details>

### Concept Summary


- Scanner Class


The Scanner class in Java is a utility that allows for simple input reading from different input streams, like the keyboard. It's part of the java.util package, which must be imported to use the class.


- Main Method

The main method serves as the entry point for any Java program. When the program is run, execution begins here.


- Reading Input


The next() method of the Scanner object reads the next token from the input until it encounters a space. It's used to read a single word or a string without spaces.


- Printing Output


The System.out.println() method is used to print the output to the console, followed by a newline.



This program demonstrates a basic input/output operation in Java. It reads a single string from the user and prints it back, showcasing how to handle simple input and output in a Java program.

This example is a foundational exercise in Java programming, highlighting how to work with basic input and output. Understanding these concepts is crucial as they form the basis for more complex operations and interactions in Java applications. This program can be run in any standard Java environment and is a great starting point for beginners.

# Print `a` and `b`

### Problem Description

You are given two integers, `a` and `b`. Write a code to take these numbers as input and print them in the format shown in the example.

### Constraints

- 100,000 ≤ a, b ≤ 100,000

### Input/Output Example

**Input #1**

```
4 5
```

**Output #1**

```css
a = 4
b = 5

```

### Solution.java

<details>
    <summary>Details</summary>

<pre><code>
import java.util.Scanner;

public class Solution {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int a = sc.nextInt();
        int b = sc.nextInt();

        System.out.println("a = " + a);
        System.out.println("b = " + b);
    }
}
</code></pre>

</details>

### Explanation and Concept Overview

<details>
    <summary>Details</summary>

The task is to read two integers, `a` and `b`, from the user input and print them in a specified format. This is a straightforward problem that tests basic input/output operations in Java.

1. Input
<br>
    - The program uses `Scanner` to read two integers from the user.
<br>
    - `sc.nextInt()` reads the next integer from the input.

2. Output
<br>
    - The program then prints the values of `a` and `b` in the format "a = value" and "b = value".
<br>
    - This is done using `System.out.println()` where the string concatenation operator (`+`) is used to combine the text with the variable values.
<br>
</details>


### Concept Overview

- **Basic Input/Output**
    
    This problem emphasizes understanding how to take input from the user and how to output the data in a specific format. It’s fundamental for beginners to grasp how input and output work in Java.
    
- **String Concatenation**
    
    The problem also involves string concatenation, where you combine strings and variables to create a desired output format.
    
- **Using the `Scanner` Class:**
    
    The `Scanner` class is a part of the `java.util` package, and it is widely used for taking input in Java. This problem introduces or reinforces the use of `Scanner` to read integers from standard input.
    

This problem is a basic exercise in handling input and output in Java, useful for beginners to get accustomed to reading input and printing formatted output.

# Toggle Case and Print

### Problem Description

You are given a string `str` composed of English alphabets. Write a code to convert each alphabet in the string to its opposite case (uppercase to lowercase, and lowercase to uppercase) and then print the result.

### Constraints

- The length of `str` is between 1 and 20 inclusive.
- `str` consists of alphabetic characters only.

### Input/Output Example

**Input #1**

```
aBcDeFg

```

**Output #1**

```
AbCdEfG
```

※ The constraints were updated on May 3, 2023.
### Solution

<details>
    <summary>Details</summary>
    <pre><code>
import java.util.Scanner;

public class Solution {
    public static void main(String[] args) {
        // Create a Scanner object to read input
        Scanner sc = new Scanner(System.in);
        
        // Read the input string
        String a = sc.next();
        
        // Create a variable to store the result
        String answer = "";
        
        // Variable to store each character
        char c;
        
        // Loop through each character in the input string
        for(int i = 0; i < a.length(); i++) {
            // Get the character at the current position in the string
            c = a.charAt(i);
            
            // Check if the character is uppercase
            if(Character.isUpperCase(c)) {
                // Convert to lowercase and append to the result
                answer += Character.toLowerCase(c); 
            } else {
                // Convert to uppercase and append to the result
                answer += Character.toUpperCase(c);
            }
        }
        
        // Print the final result
        System.out.println(answer);        
    }
}

</code></pre>

</details>

### Conceptual Explanation
1. **Input Handling**
    - The code begins by creating a `Scanner` object to read the input string from the user. The `sc.next()` function reads the next token of input (in this case, a string) and stores it in the variable `a`.
2. **Variable Initialization**
    - The variable `answer` is initialized as an empty string. This variable will be used to store the final output after converting each character to its opposite case.
    - The variable `c` is declared to temporarily store each character from the string during the loop.
3. **Looping through the String**
    - A `for` loop iterates over each character in the string `a`. The loop runs from index `0` to the length of the string minus one.
4. **Character Case Conversion**
    - Inside the loop, the `charAt(i)` method is used to get the character at the current index `i` of the string.
    - The `Character.isUpperCase(c)` method checks if the character `c` is uppercase.
        - If `c` is uppercase, it is converted to lowercase using `Character.toLowerCase(c)`, and the result is appended to the `answer` string.
        - If `c` is lowercase, it is converted to uppercase using `Character.toUpperCase(c)`, and the result is appended to the `answer` string.


> https://docs.oracle.com/javase/8/docs/api/
> 
> - toLowerCaseConverts the character (Unicode code point) argument to lowercase using case mapping information from the UnicodeData file.
>     
>     ```
>     public static int toLowerCase(int codePoint)
>     ```
>     
>     Note that `Character.isLowerCase(Character.toLowerCase(codePoint))` does not always return `true` for some ranges of characters, particularly those that are symbols or ideographs.
>     
>     In general, [`String.toLowerCase()`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html#toLowerCase--) should be used to map characters to lowercase. `String` case mapping methods have several benefits over `Character` case mapping methods. `String` case mapping methods can perform locale-sensitive mappings, context-sensitive mappings, and 1:M character mappings, whereas the `Character` case mapping methods cannot.
>     
>     **Parameters:**`codePoint` - the character (Unicode code point) to be converted.**Returns:**the lowercase equivalent of the character (Unicode code point), if any; otherwise, the character itself.**Since:**1.5**See Also:**[`isLowerCase(int)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#isLowerCase-int-), [`String.toLowerCase()`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html#toLowerCase--)
>     
> 
> ```
> public static char toUpperCase(char ch)
> ```
> 
> Converts the character argument to uppercase using case mapping information from the UnicodeData file.
> 
> Note that `Character.isUpperCase(Character.toUpperCase(ch))` does not always return `true` for some ranges of characters, particularly those that are symbols or ideographs.
> 
> In general, [`String.toUpperCase()`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html#toUpperCase--) should be used to map characters to uppercase. `String` case mapping methods have several benefits over `Character` case mapping methods. `String` case mapping methods can perform locale-sensitive mappings, context-sensitive mappings, and 1:M character mappings, whereas the `Character` case mapping methods cannot.
> 
> **Note:** This method cannot handle [supplementary characters](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#supplementary). To support all Unicode characters, including supplementary characters, use the [`toUpperCase(int)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#toUpperCase-int-) method.
> 
> **Parameters:**`ch` - the character to be converted.**Returns:**the uppercase equivalent of the character, if any; otherwise, the character itself.**See Also:**[`isUpperCase(char)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#isUpperCase-char-), [`String.toUpperCase()`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html#toUpperCase--)
> 


**Breif**

- **`print`**


Outputs data as-is, stays on the same line.


- **`println`**


Outputs data as-is, then moves to a new line.


- **`printf`**


 Formats and outputs data according to a specified format, stays on the same line unless explicitly told to move to the next line.

### Summary

This code efficiently toggles the case of each character in a string provided by the user. It demonstrates the use of loops, conditionals, and basic string operations in Java. The approach ensures that every character is checked and converted appropriately, resulting in the desired output.

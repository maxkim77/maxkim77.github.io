---
layout: single
title:  "[CodingTest] Java : Sum of Numbers "
categories: CodingTest
tag: [CS, Java, Programming, DataStructure, Sum_Numbers]
toc: true
---

![Codingtest]({{site.urls}}/assets/images/2024-08-28-PrintingaStringinJava/2.png)


# Solving Problem 11720: Sum of Numbers

### Problem Description
You are given **N numbers** written consecutively without spaces. Write a program to calculate and print the sum of these numbers.

### Constraints
- **1 <= N <= 100**
- The input numbers are provided without spaces.

### Input Format
1. The first line contains an integer **N**, the number of digits.
2. The second line contains **N consecutive digits** without spaces.

### Output Format
- Print the sum of the given digits.

### Examples
#### Example 1
**Input:**
```
1
1
```
**Output:**
```
1
```

#### Example 2
**Input:**
```
5
54321
```
**Output:**
```
15
```

#### Example 3
**Input:**
```
25
7000000000000000000000000
```
**Output:**
```
7
```

#### Example 4
**Input:**
```
11
10987654321
```
**Output:**
```
46
```

---

### Approach
This problem is solved by iterating through each digit of the input string, converting it to an integer, and adding it to a running sum. The approach is straightforward and efficient given the constraint.

#### Steps to Solve:
1. Read the input values.
2. Convert the string of numbers into a character array.
3. Loop through each character, convert it to its numeric value, and add it to the sum.
4. Print the total sum.

---

### Java Implementation
```java
package datastruc.R1;

import java.util.*;

public class P11720 {
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int N = sc.nextInt();
        String sNum = sc.next();

        // Convert string to char array
        char cNum[] = sNum.toCharArray();
        int sum = 0;

        // Sum each digit
        for (int i = 0; i < N; i++) {
            sum += cNum[i] - '0'; // Convert char to int by subtracting '0'
        }

        System.out.println(sum);
        sc.close();
    }
}
```

---

### Explanation of the Code
1. **Input Handling**:
   - `Scanner` is used to read input.
   - `nextInt()` reads the number of digits \( N \).
   - `next()` reads the string of \( N \) digits.

2. **Character Array Conversion**:
   - The `toCharArray()` method converts the string into an array of characters, where each character represents a single digit.

3. **Summation Loop**:
   - Iterate through each character in the array.
   - Convert the character to its integer value by subtracting `'0'` (ASCII adjustment).
   - Add the integer value to the running total.

4. **Output**:
   - Print the total sum.

---

### Links
- Problem Link: [Baekjoon 11720](https://www.acmicpc.net/problem/11720)
- Source Code: [GitHub Repository](https://github.com/maxkim77/javaalgo)

---

### Summary
This solution effectively handles the constraints and uses basic string and array manipulation techniques in Java to solve the problem. The time complexity is \( O(N) \), making it efficient given the problem's limits.

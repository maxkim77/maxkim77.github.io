---
layout: single
title:  "[CodingTest] Java: Range Sum Query (Prefix Sum)"
categories: CodingTest
tag: [CS, Java, Programming, DataStructure, Range_Sum]
toc: true
---

![Codingtest]({{site.urls}}/assets/images/2024-08-28-PrintingaStringinJava/2.png)

# Solving Problem 11659: Prefix Sum for Range Queries

### Problem Description
Given **N numbers**, the task is to efficiently calculate the sum of numbers from the \(i^th\) to the \(j^th\) index for multiple queries.

### Constraints
- **1 ≤ N ≤ 100,000**
- **1 ≤ M ≤ 100,000**
- **1 ≤ i ≤ j ≤ N**
- The numbers are natural numbers (≤ 1000).

### Input Format
1. The first line contains two integers, **N** (number of numbers) and **M** (number of queries).
2. The second line contains **N numbers** separated by spaces.
3. Each of the next **M lines** contains two integers **i** and **j**, representing the range for which the sum needs to be calculated.

### Output Format
For each query, output the sum of numbers from the \(i^th\) to the \(j^th\) index.

---

### Example Input and Output
#### Example 1
**Input:**
```
5 3
5 4 3 2 1
1 3
2 4
5 5
```
**Output:**
```
12
9
1
```

#### Explanation
1. Query 1: Sum of elements from index 1 to 3 = 5 + 4 + 3 = 12.
2. Query 2: Sum of elements from index 2 to 4 = 4 + 3 + 2 = 9.
3. Query 3: Sum of elements from index 5 to 5 = 1.

---

### Approach: Prefix Sum Technique
To efficiently calculate the sum of any range \(i\) to \(j\), we use the **prefix sum array** technique.

#### Prefix Sum Formula:
Let \(S[k]\) be the sum of the first \(k\) elements of the array.

- \(S[k] = S[k-1] + A[k]\)

To calculate the sum of elements from index \(i\) to \(j\):
- \(	ext{Range Sum} = S[j] - S[i-1]\)

#### Steps:
1. Precompute the prefix sum array \(S\) such that \(S[k]\) contains the sum of the first \(k\) elements.
2. For each query, use the formula \(S[j] - S[i-1]\) to calculate the sum in constant time \(O(1)\).

#### Complexity:
- **Prefix Sum Construction**: \(O(N)\)
- **Query Handling**: \(O(1)\) per query
- **Total Complexity**: \(O(N + M)\)

---

### Java Implementation
```java
package datastruc.R1;
import java.io.*;
import java.util.*;

public class P11659 {
    public static void main(String[] args) throws IOException {
        BufferedReader bR = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer sT = new StringTokenizer(bR.readLine());
        int arrNum = Integer.parseInt(sT.nextToken());
        int queryNum = Integer.parseInt(sT.nextToken());
        long S[] = new long[arrNum + 1];

        // Construct prefix sum array
        sT = new StringTokenizer(bR.readLine());
        for (int i = 1; i <= arrNum; i++) {
            S[i] = S[i - 1] + Integer.parseInt(sT.nextToken());
        }

        // Handle queries
        for (int l = 0; l < queryNum; l++) {
            sT = new StringTokenizer(bR.readLine());
            int i = Integer.parseInt(sT.nextToken());
            int j = Integer.parseInt(sT.nextToken());
            System.out.println(S[j] - S[i - 1]);
        }
    }
}
```

---

### Explanation of the Code
1. **Input Handling**:
   - Read \(N\) (number of elements) and \(M\) (number of queries).
   - Read the \(N\) numbers into a prefix sum array.

2. **Prefix Sum Array Construction**:
   - \(S[i] = S[i-1] + A[i]\), where \(A[i]\) is the \(i^{th}\) element of the input.

3. **Query Processing**:
   - For each query \(i, j\), calculate \(S[j] - S[i-1]\) to get the sum of elements from index \(i\) to \(j\).

4. **Output**:
   - Print the result for each query.

---

### Advantages of Prefix Sum
1. **Efficient Query Handling**: Each query is handled in \(O(1)\) time, making it suitable for large inputs.
2. **Precomputation**: Although we spend \(O(N)\) to construct the prefix sum array, this is a one-time cost that significantly speeds up query handling.

---

### Links
- **Problem Link**: [Baekjoon 11659](https://www.acmicpc.net/problem/11659)
- **Source Code**: [GitHub Repository](https://github.com/maxkim77/javaalgo)

---

### Summary
This solution efficiently calculates the sum of any range \(i\) to \(j\) using the prefix sum technique. With a time complexity of \(O(N + M)\), it is well-suited for large inputs and multiple queries.

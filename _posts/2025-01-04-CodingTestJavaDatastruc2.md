---
layout: single
title: "[CodingTest] Java: Two-Pointer Technique for Good Numbers (Problem P1253)"
categories: CodingTest
tag: [CS, Java, Programming, DataStructure, Two_Pointer]
toc: true
---

![Codingtest](/assets/images/2024-08-28-PrintingaStringinJava/2.png)

# Solving Problem P1253: Counting Good Numbers with Two-Pointer Technique

### Problem Description

Given a sequence of **N integers**, the task is to **count how many of these numbers can be expressed as the sum of two distinct numbers** from the array. A number cannot be used to form itself, but duplicate values are considered distinct if they are at different positions.

### Constraints

- **1 ≤ N ≤ 2000**
- **A[i] ≤ 1,000,000,000**

### Input Format

1. The first line contains an integer **N**, the number of elements in the array.
2. The second line contains **N numbers** separated by spaces.

### Output Format

Output a single integer, the count of "good numbers" in the array.

---

### Example Input and Output

#### Example 1

**Input**
```
5
1 2 3 4 5
```

**Output**
```
3
```

#### Explanation
- `3 = 1 + 2`
- `4 = 1 + 3`
- `5 = 2 + 3`
- Thus, there are **3** "good numbers".

#### Example 2

**Input:**
```
4
0 0 0 0
```

**Output:**
```
4
```

#### Explanation
- Each `0` can be expressed as the sum of two other `0`s from different positions.
- Thus, all **4** numbers are "good numbers".

---

### Approach: Two-Pointer Technique

To efficiently count the "good numbers" in the array, we can utilize the **two-pointer technique**. Here's a step-by-step approach:

#### Steps:

1. **Sort the Array**: 
   - First, sort the array in ascending order. Sorting helps in efficiently finding pairs that sum up to a target value using two pointers.

2. **Iterate Through Each Number**: 
   - For each number in the array, consider it as the target sum and use two pointers to find if there exists a pair that sums up to this target.

3. **Initialize Two Pointers**:
   - Initialize one pointer at the start (`i = 0`) and another at the end (`j = N-1`) of the array.
   - If either pointer points to the current target index, move the pointer accordingly to avoid using the number itself.

4. **Check Sum**:
   - Calculate the sum of the numbers at the two pointers.
   - If the sum equals the target, increment the count of "good numbers" and move to the next target.
   - If the sum is less than the target, move the left pointer to the right to increase the sum.
   - If the sum is greater than the target, move the right pointer to the left to decrease the sum.

5. **Avoid Counting Duplicates**:
   - Ensure that the same pair isn't counted multiple times by breaking out of the loop once a valid pair is found.

---

### Java Implementation

```java
package datastruc.R1;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.StringTokenizer;

public class P1253 {

    public static void main(String[] args) throws IOException {
        BufferedReader bf = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(bf.readLine());
        int Result = 0;
        long A[] = new long[N];
        StringTokenizer st = new StringTokenizer(bf.readLine());
        for(int i = 0; i < N; i++){
            A[i] = Long.parseLong(st.nextToken());
        }
        Arrays.sort(A); // Sort the array in ascending order

        for(int k = 0; k < N; k++){ // Iterate through each number as the target
            long find = A[k];
            int i = 0;
            int j = N - 1; // Initialize two pointers
            while(i < j){
                if(A[i] + A[j] == find){
                    if(i != k && j != k){
                        Result++;
                        break;
                    } else if(i == k){
                        i++;
                    } else if(j == k){
                        j--;
                    }     
                }
                else if (A[i] + A[j] < find){
                    i++;
                } else{
                    j--;
                }
            }
        }
        System.out.println(Result);
        bf.close();
    }
}
```

---

### Explanation of the Code

1. **Input Handling**:
    - The program reads the number of elements `N` and the array `A` from the standard input using `BufferedReader` and `StringTokenizer` for efficient input processing.

2. **Sorting**:
    - The array `A` is sorted in ascending order using `Arrays.sort(A)`. Sorting is crucial for the two-pointer technique to work efficiently.

3. **Counting Good Numbers**:
    - The outer loop iterates through each element in the sorted array, treating each as the target sum (`find`).
    - For each target, two pointers `i` and `j` are initialized at the start and end of the array, respectively.
    - The inner loop moves the pointers based on the sum of `A[i] + A[j]` compared to the target:
        - **If the sum equals the target** and neither pointer is pointing to the target index (`k`), it's a "good number", and `Result` is incremented.
        - **If either pointer points to the target index**, the pointer is moved to avoid using the number itself.
        - **If the sum is less than the target**, the left pointer `i` is moved to the right to increase the sum.
        - **If the sum is greater than the target**, the right pointer `j` is moved to the left to decrease the sum.
    - The loop breaks once a valid pair is found for the current target.

4. **Output**:
    - After processing all elements, the total count of "good numbers" is printed.

---

### Complexity Analysis

- **Sorting**: \(O(N \log N)\)
- **Counting Good Numbers**: \(O(N^2)\)
  - Outer loop runs \(N\) times.
  - Inner loop (two-pointer search) runs \(O(N)\) for each target.
- **Total Complexity**: \(O(N^2)\)

---

### Links

- **Problem Link**: [Baekjoon P1253](https://www.acmicpc.net/problem/1253)
- **Source Code**: [GitHub Repository](https://github.com/maxkim77/javaalgo)

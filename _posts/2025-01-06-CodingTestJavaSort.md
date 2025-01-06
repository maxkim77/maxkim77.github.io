---
layout: single
title: "[CodingTest] Java: Bubble Sort Algorithm"
categories: CodingTest
tag: [CS, Java, Programming, BubbleSort, Sorting]
toc: true
---

![Codingtest](/assets/images/2024-08-28-PrintingaStringinJava/2.png)

# Solving Sorting Problems with Bubble Sort in Java

### Problem Description

Given an array of **N integers**, the task is to sort the array in ascending order using the **Bubble Sort Algorithm**.

Bubble sort is a simple comparison-based sorting technique where adjacent elements are compared and swapped to place them in the correct order.

### Input Format

1. An integer **N**, the number of elements in the array.
2. **N integers**, representing the array elements.

### Output Format

The sorted array, where each element is printed on a new line.

---

### Example Input and Output

#### Example 1

**Input:**
```
5
4 2 5 1 3
```

**Output:**
```
1
2
3
4
5
```

#### Explanation
- Initial Array: [4, 2, 5, 1, 3]
- After sorting using Bubble Sort:
  - [1, 2, 3, 4, 5]
- Each element is printed on a new line in ascending order.

---

### Approach: Bubble Sort Algorithm

The **Bubble Sort Algorithm** works by repeatedly comparing adjacent elements in the array and swapping them if they are in the wrong order. This process is repeated until the array is fully sorted.

#### Key Idea

1. During each iteration, the largest unsorted element "bubbles up" to its correct position at the end of the array.
2. The process continues for all elements until the entire array is sorted.

#### Steps

1. **Compare Adjacent Elements**:
   - If the current element is greater than the next element, swap them.
2. **Repeat** the process for all elements, reducing the effective size of the unsorted part of the array after each iteration.
3. **Stop** when no swaps are needed in a full iteration, indicating the array is sorted.

#### Complexity

- **Time Complexity:**
  - Worst Case: \( O(N^2) \) (when the array is sorted in reverse order)
  - Best Case: \( O(N) \) (when the array is already sorted, with optimization)
- **Space Complexity:** \( O(1) \) (no additional memory required apart from the input array)

---

### Java Implementation

```java
import java.util.Scanner;

public class BubbleSort {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // Input the size of the array
        int N = sc.nextInt();
        int[] arr = new int[N];

        // Input array elements
        for (int i = 0; i < N; i++) {
            arr[i] = sc.nextInt();
        }

        // Perform Bubble Sort
        for (int i = 0; i < N - 1; i++) {
            for (int j = 0; j < N - 1; j++) {
                if (arr[j] > arr[j + 1]) {
                    // Swap elements
                    int temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                }
            }
        }

        // Output the sorted array
        for (int i = 0; i < N; i++) {
            System.out.println(arr[i]);
        }

        sc.close();
    }
}
```

---

### Pseudocode

Here is the pseudocode for the Bubble Sort Algorithm:

```plaintext
BEGIN
    CREATE Scanner object to read input
    READ N (number of elements in the array)
    CREATE integer array of size N

    FOR i FROM 0 TO N-1 DO
        READ arr[i] (fill the array with input numbers)
    END FOR

    // Bubble sort algorithm
    FOR i FROM 0 TO N-2 DO
        FOR j FROM 0 TO N-2 DO
            IF arr[j] > arr[j+1] THEN
                SWAP arr[j] AND arr[j+1]
            END IF
        END FOR
    END FOR

    // Print sorted array
    FOR i FROM 0 TO N-1 DO
        PRINT arr[i]
    END FOR

    CLOSE Scanner
END
```

---

### Explanation of the Code

1. **Input Handling**:
    - The program reads the size of the array \( N \) and the array elements from the user.
    - The array is filled using a loop.

2. **Sorting (Bubble Sort)**:
    - Two nested loops are used to perform the sorting:
      - The outer loop controls the number of passes (\( N-1 \)).
      - The inner loop compares adjacent elements and swaps them if they are in the wrong order.
    - After each outer loop iteration, the largest element is guaranteed to be in its correct position.

3. **Output**:
    - The sorted array is printed line by line using a loop.

---

### Walkthrough with Example

#### Input:
```
5
4 2 5 1 3
```

#### Steps:
1. Initial Array: [4, 2, 5, 1, 3]

2. **Pass 1**:
   - Compare 4 and 2: Swap → [2, 4, 5, 1, 3]
   - Compare 4 and 5: No swap
   - Compare 5 and 1: Swap → [2, 4, 1, 5, 3]
   - Compare 5 and 3: Swap → [2, 4, 1, 3, 5]

3. **Pass 2**:
   - Compare 2 and 4: No swap
   - Compare 4 and 1: Swap → [2, 1, 4, 3, 5]
   - Compare 4 and 3: Swap → [2, 1, 3, 4, 5]

4. **Pass 3**:
   - Compare 2 and 1: Swap → [1, 2, 3, 4, 5]

5. Sorted Array: [1, 2, 3, 4, 5]

#### Output:
```
1
2
3
4
5
```

---

### Advantages and Disadvantages

#### Advantages:
- Simple and easy to understand.
- Suitable for small datasets.

#### Disadvantages:
- Inefficient for large datasets due to its \( O(N^2) \) time complexity.
- Performs unnecessary iterations even if the array is already sorted.

---

### Optimizations and Alternatives

1. **Optimization:**
   - Add a flag to check if any swaps were made in an iteration.
   - If no swaps are made, terminate the loop early.

2. **Better Algorithms:**
   - **Quick Sort** or **Merge Sort** can handle large datasets efficiently with \( O(N \log N) \) time complexity.

---

### Links

- **Bubble Sort Explanation**: [Wikipedia](https://en.wikipedia.org/wiki/Bubble_sort)
- **Source Code Repository**: [GitHub](https://github.com/maxkim77/javaalgo)

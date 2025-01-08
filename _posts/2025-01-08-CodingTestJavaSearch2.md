---
layout: single
title: "[CodingTest] Java: Binary Search (Problem P1920)"
categories: CodingTest
tag: [CS, Java, Programming, DataStructure, Binary_Search]
toc: true
---

![Codingtest](/assets/images/2024-08-28-PrintingaStringinJava/2.png)

# Solving Problem P1920: Binary Search

### Problem Description

You are given an integer **N** and an array **A** of **N** integers. Then you receive an integer **M** and **M** queries, each query being a target integer. For each target, output **1** if it exists in **A**, or **0** if it does not.

### Constraints

- 1 ≤ N ≤ 100,000 (Number of elements in the array)
- 1 ≤ M ≤ 100,000 (Number of queries)
- Array elements and search targets can be in the range of a 32-bit integer (−2,147,483,648 to 2,147,483,647)

### Input Format

1. The first line contains an integer **N**, the size of the array.
2. The second line contains **N** integers (the elements of **A**).
3. The third line contains an integer **M**, the number of queries.
4. The next line contains **M** integers (each one is a target to search for in **A**).

### Output Format

- For each of the **M** targets, print **1** if the target exists in the array **A**, otherwise print **0**.

---

### Example Input and Output

#### Example

**Input:**
```
5
4 1 5 2 3
5
1 3 7 9 5
```

**Output:**
```
1
1
0
0
1
```

**Explanation:**
- **1** is in the array → output **1**
- **3** is in the array → output **1**
- **7** is not in the array → output **0**
- **9** is not in the array → output **0**
- **5** is in the array → output **1**

---

### Concept of Binary Search

Binary search is an efficient algorithm for finding a target value within a sorted array. It repeatedly divides the search interval in half:
- Start with the entire array as the search interval.
- Compare the middle element with the target.
- If the target equals the middle element, the search is successful.
- If the target is smaller, narrow the interval to the left half.
- If the target is larger, narrow the interval to the right half.

#### Time Complexity

- Sorting the array: O(N log N)
- Binary search for each query: O(log N)
- Total for M queries: O(M log N)
- Overall complexity: O(N log N + M log N)

#### Space Complexity

- O(N): Space for the array and auxiliary data.

---

### Approach

1. **Sort the array** of size **N** to enable binary search.
2. For each target in the **M** queries:
   - Use binary search to determine whether the target exists.
   - Print **1** if found, otherwise **0**.

---

### Pseudocode

```
BEGIN
  READ N, the size of the array
  READ array A of size N
  SORT array A

  READ M, the number of queries
  FOR each query target in M:
    SET start = 0, end = N - 1, found = false

    WHILE start <= end:
      SET mid = (start + end) / 2
      IF A[mid] == target:
        found = true
        BREAK
      ELSE IF A[mid] < target:
        start = mid + 1
      ELSE:
        end = mid - 1

    PRINT 1 if found, otherwise 0
END
```

---

### Java Implementation

```java
package search;

import java.util.*;

public class P1920 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // 1. Read N and the array A
        int N = sc.nextInt();
        int[] A = new int[N];
        for(int i = 0; i < N; i++) {
            A[i] = sc.nextInt();
        }

        // 2. Sort the array for efficient binary search
        Arrays.sort(A);

        // 3. Read M and process each query
        int M = sc.nextInt();
        for(int i = 0; i < M; i++) {
            int target = sc.nextInt();
            boolean found = false;
            int start = 0;
            int end = N - 1;

            // 4. Perform binary search
            while(start <= end) {
                int mid = (start + end) / 2;
                if(A[mid] == target) {
                    found = true;
                    break;
                }
                if(A[mid] < target) {
                    start = mid + 1;
                } else {
                    end = mid - 1;
                }
            }

            // 5. Print result for this query
            System.out.println(found ? 1 : 0);
        }

        sc.close();
    }
}
```

---

### Explanation of the Code

1. **Reading Input**:
   - The size of the array \(N\) and its elements are read into an integer array `A`.
   - The size of the query set \(M\) is read, followed by the \(M\) target values.

2. **Sorting the Array**:
   - Sorting ensures that binary search can be applied. This step takes O(N log N).

3. **Binary Search for Each Query**:
   - For each target, the algorithm performs binary search over `A`.
   - A `start` pointer begins at the first element, and an `end` pointer begins at the last element.
   - The midpoint `mid` is calculated, and its value is compared to the target.
   - Depending on the comparison, the search interval is halved until the target is found or the interval is empty.

4. **Output Results**:
   - If the target is found, **1** is printed.
   - Otherwise, **0** is printed.

---

### Example Walkthrough

#### Input:
```
5
4 1 5 2 3
5
1 3 7 9 5
```

#### Execution:

1. **Sorting the Array**:
   - Input array: [4, 1, 5, 2, 3]
   - Sorted array: [1, 2, 3, 4, 5]

2. **Binary Search for Each Query**:
   - Query 1: Target = 1 → Found → Print 1
   - Query 2: Target = 3 → Found → Print 1
   - Query 3: Target = 7 → Not Found → Print 0
   - Query 4: Target = 9 → Not Found → Print 0
   - Query 5: Target = 5 → Found → Print 1

#### Output:
```
1
1
0
0
1
```

---

### Links

- **Problem Link**: [Baekjoon P1260](https://www.acmicpc.net/problem/1260)
- **Graph Traversal Reference**: [Wikipedia](https://en.wikipedia.org/wiki/Graph_traversal)

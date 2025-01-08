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

- \(1 \le N \le 100{,}000\)
- \(1 \le M \le 100{,}000\)
- Array elements and search targets can be in the range of a 32-bit integer \((\pm 2{,}147{,}483{,}647)\)

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

### Approach

1. **Sort the array** of size **N**.
2. For each target in the **M** queries:
   - Apply **binary search** to check for the target’s existence.
   - Print **1** if found, **0** otherwise.

#### Time Complexity

- Sorting takes \(O(N \log N)\).
- Each query uses binary search, which is \(O(\log N)\).
- For **M** queries, the total search time is \(O(M \log N)\).
- Overall complexity: \(O(N \log N + M \log N)\).

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

1. We **read** the integer \(N\) and then the **N** integers into array A.
2. We **sort** the array A using Arrays.sort(A).
3. We **read** \(M\), the number of queries.
4. For each query:
   - Set up two pointers, start and end, indicating the current search range.
   - While start <= end, compute the midpoint mid.
   - Compare the target with A[mid]:
     - If they match, mark found = true and break.
     - If the midpoint’s value is greater than the target, move end to mid - 1.
     - Otherwise, move start to mid + 1.
   - Print **1** if the target was found, otherwise **0**.

This completes our solution for **Baekjoon 1920** using **binary search** in Java.
---

### Links

- **Problem Link**: [Baekjoon P1260](https://www.acmicpc.net/problem/1260)
- **Graph Traversal Reference**: [Wikipedia](https://en.wikipedia.org/wiki/Graph_traversal)

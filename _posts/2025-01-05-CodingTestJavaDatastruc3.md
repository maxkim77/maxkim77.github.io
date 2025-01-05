---
layout: single
title: "[CodingTest] Java: Sliding Window Minimum (Problem P11003)"
categories: CodingTest
tag: [CS, Java, Programming, DataStructure, Sliding_Window, Deque]
toc: true
---

![Codingtest](/assets/images/2024-08-28-PrintingaStringinJava/2.png)

# Solving Problem P11003: Sliding Window Minimum Using Deque

### Problem Description

Given **N numbers** \( A_1, A_2, \dots, A_N \) and an integer \( L \), the goal is to calculate the minimum value in each sliding window of size \( L \). Specifically, for each \( i \):

\[
D_i = \min(A_{i-L+1}, \dots, A_i)
\]

When \( i - L + 1 \leq 0 \), ignore indices \( \leq 0 \) while calculating the minimum.

### Constraints

- **1 \( \leq \) L \( \leq \) N \( \leq \) 5,000,000**
- **\(-10^9 \leq A_i \leq 10^9\)**

### Input Format

1. The first line contains two integers **N** (number of elements) and **L** (window size).
2. The second line contains **N integers** \( A_1, A_2, \dots, A_N \).

### Output Format

Output the sliding window minimum values \( D_i \), separated by spaces.

---

### Example Input and Output

#### Example 1

**Input:**
```
12 3
1 5 2 3 6 2 3 7 3 5 2 6
```

**Output:**
```
1 1 1 2 2 2 2 2 3 3 2 2
```

#### Explanation
- For each window of size \( L = 3 \):
  - Window [1, 5, 2]: Minimum = 1
  - Window [5, 2, 3]: Minimum = 1
  - Window [2, 3, 6]: Minimum = 2
  - Continue similarly...

---

### Approach: Sliding Window with Deque

The problem can be efficiently solved using a **deque** (double-ended queue), which helps maintain the minimum value of the current sliding window.

#### Key Idea
- Use the deque to store indices of array elements. The deque will always maintain elements in increasing order of value.
- Ensure the deque only contains indices that fall within the current sliding window.

#### Steps

1. **Initialize** a deque to store elements' indices. This deque will always maintain indices in increasing order of values.
2. **Iterate** through the array elements:
   - Remove elements from the back of the deque if they are greater than the current element. These elements will never be the minimum in the future.
   - Add the current element's index to the deque.
   - Remove the front of the deque if it is outside the current sliding window.
   - The element at the front of the deque is the minimum for the current sliding window.
3. Append the minimum to the result for each step.

#### Complexity

- **Time Complexity:** \( O(N) \)
  - Each element is added and removed from the deque exactly once.
- **Space Complexity:** \( O(L) \), where \( L \) is the maximum size of the deque.

---

### Java Implementation

```java
package datastruc.R1;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.util.Deque;
import java.util.LinkedList;
import java.util.StringTokenizer;

public class P11003 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        StringTokenizer st = new StringTokenizer(br.readLine());
        
        int N = Integer.parseInt(st.nextToken());
        int L = Integer.parseInt(st.nextToken());
        st = new StringTokenizer(br.readLine());

        Deque<Node> mydeque = new LinkedList<>();
        for (int i = 0; i < N; i++) {
            int now = Integer.parseInt(st.nextToken());

            // Remove elements from back that are greater than the current value
            while (!mydeque.isEmpty() && mydeque.getLast().value > now) {
                mydeque.removeLast();
            }

            // Add the current element
            mydeque.addLast(new Node(now, i));

            // Remove elements from front that are out of window
            if (mydeque.getFirst().index <= i - L) {
                mydeque.removeFirst();
            }

            // Write the minimum value for the current window
            bw.write(mydeque.getFirst().value + " ");
        }

        bw.flush();
        bw.close();
    }

    static class Node {
        public int value;
        public int index;

        Node(int value, int index) {
            this.value = value;
            this.index = index;
        }
    }
}
```

---

### Pseudocode

Here is the pseudocode for the sliding window minimum algorithm:

```plaintext
BEGIN
  READ N, L
  DECLARE deque as empty

  FOR i FROM 0 TO N - 1 DO
    READ current_element

    // Remove elements from the back of deque if they are greater than the current element
    WHILE deque IS NOT EMPTY AND deque.back.value > current_element DO
      deque.pop_back()
    END WHILE

    // Add current element's index to the deque
    deque.push_back(current_element, index)

    // Remove elements from the front if they are outside the current sliding window
    IF deque.front.index <= i - L THEN
      deque.pop_front()
    END IF

    // Append the minimum (deque.front.value) to the result
    WRITE deque.front.value + " "
  END FOR
END
```

---

### Explanation of the Code

1. **Input Handling**:
    - The program reads the number of elements \( N \) and the sliding window size \( L \).
    - It also reads the \( N \) integers into a deque for processing.

2. **Deque Operations**:
    - Remove elements from the back of the deque if their value is greater than the current element. These elements will never be the minimum in future windows.
    - Remove elements from the front of the deque if they fall outside the sliding window range \([i-L+1, i]\).
    - The element at the front of the deque is guaranteed to be the minimum for the current window.

3. **Output the Result**:
    - For each window, the value at the front of the deque is written as the minimum value.

---

### Complexity Analysis

- **Time Complexity:** \( O(N) \)
  - Each element is added and removed from the deque exactly once, resulting in linear time.
- **Space Complexity:** \( O(L) \)
  - The deque contains at most \( L \) elements at any time, where \( L \) is the window size.

---

### Links

- **Problem Link**: [Baekjoon P11003](https://www.acmicpc.net/problem/11003)
- **Source Code**: [GitHub Repository](https://github.com/maxkim77/javaalgo)

---
layout: single
title: "[CodingTest] Java: Search! Counting Connected Components in a Graph (Problem P11724)"
categories: CodingTest
keywords: [CS, Java, Programming, Graph Theory, DFS, Connected Components,Serch]
toc: true
---

![Codingtest](/assets/images/2024-08-28-PrintingaStringinJava/2.png)

# Solving Problem P11724: Search! Counting Connected Components in an Undirected Graph 

### Problem Description

Given an **undirected graph** with **N vertices** and **M edges**, the task is to calculate the number of **connected components** in the graph. A **connected component** is a subset of vertices such that there is a path between any two vertices within the subset, and the subset is not connected to any other vertices outside of it.

### Constraints

- **1 ≤ N ≤ 1,000**
- **0 ≤ M ≤ N × (N - 1) / 2**
- Each edge is given as two integers, representing vertices **u** and **v**.

### Input Format

1. The first line contains two integers **N** (number of vertices) and **M** (number of edges).
2. The next **M lines** contain two integers **u** and **v**, representing an undirected edge between vertices **u** and **v**.

### Output Format

Print a single integer, the number of connected components in the graph.

---

### Example Input and Output

#### Example 1

**Input**
```
6 5
1 2
2 5
5 1
3 4
4 6
```

**Output**
```
2
```

#### Explanation
- There are two connected components
  - Component 1: {1, 2, 5}
  - Component 2: {3, 4, 6}

#### Example 2

**Input**
```
6 8
1 2
2 5
5 1
3 4
4 6
5 4
2 4
2 3
```

**Output**
```
1
```

#### Explanation
- There is one connected component containing all vertices: {1, 2, 3, 4, 5, 6}.

---

### Approach: Depth-First Search (DFS)

To solve the problem, we use **Depth-First Search (DFS)** to traverse each connected component in the graph. The idea is to start at an unvisited vertex, traverse all reachable vertices, and count the number of times we initiate a new traversal.

#### Key Idea
1. Use an adjacency list to represent the graph.
2. Maintain a visited array to keep track of visited vertices.
3. For each vertex, if it has not been visited, initiate a DFS traversal and increment the connected components count.

#### Complexity
- **Time Complexity:** \( O(N + M) \)
  - Traversing all vertices and edges in the graph.
- **Space Complexity:** \( O(N + M) \)
  - Storing the adjacency list and visited array.

---

### Java Implementation

```java
package search;

import java.io.*;
import java.util.*;

public class P11724 {
    static ArrayList<Integer>[] A;
    static boolean visited[];

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        int n = Integer.parseInt(st.nextToken());
        int m = Integer.parseInt(st.nextToken());

        // Initialize adjacency list and visited array
        A = new ArrayList[n + 1];
        visited = new boolean[n + 1];
        for (int i = 1; i <= n; i++) {
            A[i] = new ArrayList<>();
        }

        // Read edges and populate adjacency list
        for (int i = 0; i < m; i++) {
            st = new StringTokenizer(br.readLine());
            int s = Integer.parseInt(st.nextToken());
            int e = Integer.parseInt(st.nextToken());
            A[s].add(e);
            A[e].add(s); // Undirected graph
        }

        int count = 0;

        // Perform DFS for each unvisited vertex
        for (int i = 1; i <= n; i++) {
            if (!visited[i]) {
                count++;
                DFS(i);
            }
        }

        System.out.println(count);
    }

    static void DFS(int v) {
        if (visited[v]) {
            return;
        }
        visited[v] = true;
        for (int i : A[v]) {
            if (!visited[i]) {
                DFS(i);
            }
        }
    }
}
```

---

### Pseudocode

```plaintext
BEGIN
    READ n, m (number of vertices and edges)

    CREATE adjacency list A of size n + 1
    CREATE visited array of size n + 1, initialized to false

    FOR i FROM 1 TO n DO
        A[i] = new empty list
    END FOR

    FOR i FROM 0 TO m DO
        READ edge (s, e)
        ADD e to A[s]
        ADD s to A[e] (undirected graph)
    END FOR

    SET count = 0

    FOR i FROM 1 TO n DO
        IF visited[i] IS false THEN
            INCREMENT count
            CALL DFS(i)
        END IF
    END FOR

    PRINT count
END

FUNCTION DFS(v):
    IF visited[v] IS true THEN
        RETURN
    END IF

    SET visited[v] = true

    FOR each neighbor i in A[v]:
        IF visited[i] IS false THEN
            CALL DFS(i)
        END IF
    END FOR
END FUNCTION
```

---

### Explanation of the Code

1. **Graph Representation**
    - The graph is represented using an **adjacency list**, which is memory-efficient compared to an adjacency matrix for sparse graphs.

2. **DFS Traversal**
    - The DFS function recursively visits all vertices in the current connected component.
    - The `visited` array ensures that each vertex is visited only once.

3. **Counting Connected Components**
    - For each unvisited vertex, we initiate a DFS traversal and increment the connected components count.

4. **Output**
    - The final count of connected components is printed.

---

### Walkthrough with Example

#### Input:
```
6 5
1 2
2 5
5 1
3 4
4 6
```

#### Steps:
1. Build adjacency list
   - Vertex 1: [2, 5]
   - Vertex 2: [1, 5]
   - Vertex 3: [4]
   - Vertex 4: [3, 6]
   - Vertex 5: [1, 2]
   - Vertex 6: [4]

2. Perform DFS
   - Start at vertex 1, traverse {1, 2, 5} (Component 1).
   - Move to vertex 3, traverse {3, 4, 6} (Component 2).

3. Count = 2.

#### Output:
```
2
```

---

### Complexity Analysis

- **Time Complexity:** \( O(N + M) \)
  - DFS visits each vertex and edge once.
- **Space Complexity:** \( O(N + M) \)
  - For the adjacency list and visited array.

---

### Links

- **Problem Link**: [Baekjoon P11724](https://www.acmicpc.net/problem/11724)
- **Graph Theory Reference**: [Wikipedia](https://en.wikipedia.org/wiki/Graph_theory)

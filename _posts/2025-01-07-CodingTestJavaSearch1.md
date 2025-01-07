---
layout: single
title: "[CodingTest] Java: Depth-First Search (DFS) and Breadth-First Search (BFS)"
categories: CodingTest
keywords: [CS, Java, Programming, Graph Theory, DFS, BFS]
toc: true
---

![Codingtest](/assets/images/2024-08-28-PrintingaStringinJava/2.png)

# Solving Problem P1260: DFS and BFS Traversal of a Graph

### Problem Description

Given an **undirected graph** with **N vertices** and **M edges**, perform:
1. **Depth-First Search (DFS)** starting from a given vertex.
2. **Breadth-First Search (BFS)** starting from the same vertex.

For both traversals, visit vertices in ascending numerical order when multiple vertices are reachable.

### Constraints

- **1 ≤ N ≤ 1,000** (Number of vertices)
- **1 ≤ M ≤ 10,000** (Number of edges)

### Input Format

1. The first line contains three integers **N** (number of vertices), **M** (number of edges), and **V** (starting vertex).
2. The next **M lines** contain two integers **u** and **v**, representing an undirected edge between vertices **u** and **v**.

### Output Format

1. Print the order of vertices visited by DFS on the first line.
2. Print the order of vertices visited by BFS on the second line.

---

### Example Input and Output

#### Example 1

**Input:**
```
4 5 1
1 2
1 3
1 4
2 4
3 4
```

**Output:**
```
1 2 4 3
1 2 3 4
```

#### Example 2

**Input:**
```
5 5 3
5 4
5 2
1 2
3 4
3 1
```

**Output:**
```
3 1 2 5 4
3 1 4 2 5
```

#### Example 3

**Input:**
```
1000 1 1000
999 1000
```

**Output:**
```
1000 999
1000 999
```

---

### Approach: Graph Traversal with DFS and BFS

To solve the problem, we use **DFS** and **BFS** traversal algorithms. Both algorithms rely on the adjacency list representation of the graph to efficiently manage edges.

#### Depth-First Search (DFS)
- DFS uses recursion or a stack to explore as deep as possible along each branch before backtracking.
- It is implemented here using recursion.

#### Breadth-First Search (BFS)
- BFS uses a queue to explore all neighbors of a vertex before moving to the next level.
- This ensures that vertices are visited in increasing order of distance from the starting vertex.

#### Complexity
- **Time Complexity:** \( O(N + M) \)
  - Traverses all vertices and edges.
- **Space Complexity:** \( O(N + M) \)
  - Adjacency list and visited array.

---

### Java Implementation

```java
package search;

import java.util.*;

public class P1260 {
    static boolean visited[];
    static ArrayList<Integer>[] A;

    public static void main(String[] args) {
        Scanner scan = new Scanner(System.in);
        int N = scan.nextInt();
        int M = scan.nextInt();
        int Start = scan.nextInt();

        A = new ArrayList[N + 1];
        for (int i = 1; i <= N; i++) {
            A[i] = new ArrayList<Integer>();
        }

        // Read edges and populate adjacency list
        for (int i = 0; i < M; i++) {
            int S = scan.nextInt();
            int E = scan.nextInt();
            A[S].add(E);
            A[E].add(S); // Undirected graph
        }

        // Sort adjacency list for consistent traversal order
        for (int i = 1; i <= N; i++) {
            Collections.sort(A[i]);
        }

        // DFS traversal
        visited = new boolean[N + 1];
        DFS(Start);
        System.out.println();

        // BFS traversal
        visited = new boolean[N + 1];
        BFS(Start);
        System.out.println();
    }

    public static void DFS(int Node) {
        System.out.print(Node + " ");
        visited[Node] = true;
        for (int i : A[Node]) {
            if (!visited[i]) {
                DFS(i);
            }
        }
    }

    private static void BFS(int Node) {
        Queue<Integer> queue = new LinkedList<Integer>();
        queue.add(Node);
        visited[Node] = true;

        while (!queue.isEmpty()) {
            int now_Node = queue.poll();
            System.out.print(now_Node + " ");
            for (int i : A[now_Node]) {
                if (!visited[i]) {
                    visited[i] = true;
                    queue.add(i);
                }
            }
        }
    }
}
```

---

### Pseudocode

```plaintext
BEGIN
    READ N, M, V (number of vertices, edges, starting vertex)
    INITIALIZE adjacency list A[N+1] and visited array

    FOR each edge (S, E):
        ADD E to A[S]
        ADD S to A[E] (undirected graph)
    END FOR

    FOR each adjacency list A[i]:
        SORT A[i]
    END FOR

    INITIALIZE visited array to false
    CALL DFS(V)
    PRINT DFS order

    INITIALIZE visited array to false
    CALL BFS(V)
    PRINT BFS order
END

FUNCTION DFS(Node):
    PRINT Node
    SET visited[Node] = true
    FOR each neighbor i in A[Node]:
        IF visited[i] IS false THEN
            CALL DFS(i)
        END IF
    END FOR
END FUNCTION

FUNCTION BFS(Node):
    INITIALIZE queue
    ENQUEUE Node
    SET visited[Node] = true

    WHILE queue IS NOT EMPTY:
        DEQUEUE current_Node
        PRINT current_Node
        FOR each neighbor i in A[current_Node]:
            IF visited[i] IS false THEN
                ENQUEUE i
                SET visited[i] = true
            END IF
        END FOR
    END WHILE
END FUNCTION
```

---

### Explanation of the Code

1. **Graph Representation:**
    - The graph is represented using an **adjacency list** to store all edges efficiently.

2. **DFS Traversal:**
    - Recursive DFS is used to visit each vertex and its neighbors in depth-first order.
    - The `visited` array ensures that each vertex is visited only once.

3. **BFS Traversal:**
    - Iterative BFS uses a queue to process vertices level by level.
    - The `visited` array ensures that each vertex is added to the queue only once.

4. **Sorting:**
    - Sorting the adjacency list ensures that vertices are visited in ascending order when multiple options are available.

---

### Walkthrough with Example

#### Input:
```
4 5 1
1 2
1 3
1 4
2 4
3 4
```

#### Steps:
1. Build adjacency list:
   - Vertex 1: [2, 3, 4]
   - Vertex 2: [1, 4]
   - Vertex 3: [1, 4]
   - Vertex 4: [1, 2, 3]

2. Perform DFS:
   - Start at vertex 1 → Visit: 1 → 2 → 4 → 3.

3. Perform BFS:
   - Start at vertex 1 → Visit: 1 → 2 → 3 → 4.

#### Output:
```
1 2 4 3
1 2 3 4
```

---

### Complexity Analysis

- **Time Complexity:** \( O(N + M) \)
  - Traverses all vertices and edges.
- **Space Complexity:** \( O(N + M) \)
  - Adjacency list and visited array.

---

### Links

- **Problem Link**: [Baekjoon P1260](https://www.acmicpc.net/problem/1260)
- **Graph Traversal Reference**: [Wikipedia](https://en.wikipedia.org/wiki/Graph_traversal)

# 1. Graph Representations

Graphs can be represented in various forms depending on the needs of an algorithm. Understanding these representations and their properties is essential for implementing efficient graph algorithms.

## 1.1. Basic Definitions

- **Graph (G)**: A structure composed of a set of vertices V and a set of edges E connecting pairs of vertices.
- **n**: Number of vertices in the graph (|V|).
- **m**: Number of edges in the graph (|E|).

## 1.2. Naive Representations

### 1.2.1. Edge List and Vertex List

- Store graph as a list of vertices and a list of edges.
- Not efficient for lookups or neighbor queries.

### 1.2.2. Visual Diagram

- Informal visual representation.
- Useful for small examples but not computationally viable.

## 1.3. Adjacency Matrix

### 1.3.1. Definition

An n × n matrix A where:

- A[i][j] = 1 if there is an edge between vertex i and j,
- A[i][j] = 0 otherwise.

### 1.3.2. Properties

- Symmetric for undirected graphs: A[i][j] = A[j][i].
- Diagonal entries are 0 assuming no self-loops.
- Space complexity: O(n²)

### 1.3.3. Example

For graph with vertices A, B, C, D, E and edges:
- A—B, A—C, B—C, C—D

Adjacency matrix:

|   | A | B | C | D | E |
|:-:|:-:|:-:|:-:|:-:|:-:|
| A | 0 | 1 | 1 | 0 | 0 |
| B | 1 | 0 | 1 | 0 | 0 |
| C | 1 | 1 | 0 | 1 | 0 |
| D | 0 | 0 | 1 | 0 | 0 |
| E | 0 | 0 | 0 | 0 | 0 |

## 1.4. Adjacency List

### 1.4.1. Definition

A set of n linked lists where each list L[v] contains all neighbors of vertex v.

### 1.4.2. Properties

- More space-efficient for sparse graphs.
- Space complexity: O(n + m)
  - n for vertex headers
  - 2m total list entries (each edge appears twice)
  
### 1.4.3. Example

Adjacency list for the same graph (A—B, A—C, B—C, C—D):

- L[A] = [B, C]
- L[B] = [A, C]
- L[C] = [A, B, D]
- L[D] = [C]
- L[E] = []

## 1.5. Size and Complexity Comparison

| Operation                        | Adjacency Matrix | Adjacency List         |
|----------------------------------|------------------|------------------------|
| Space complexity                 | O(n²)            | O(n + m)               |
| Check if edge (u, v) exists     | O(1)             | O(degree(u))           |
| List all neighbors of vertex v  | O(n)             | O(degree(v))           |

### Note:
- Use adjacency matrix for dense graphs where fast lookups are required.
- Use adjacency list for sparse graphs where space efficiency is key.

# 2. Graph Connectivity

## 2.1. Definition of Connected Graph

A graph is said to be connected if there exists a path between every pair of vertices (u, v) ∈ V.

## 2.2. Connectivity Lower Bound

If a graph G with n vertices is connected:
- Minimum number of edges m ≥ n - 1

### Reason:

- Intuitively, to connect one additional node to an existing connected component, we need at least one new edge.
- Base case: 1 vertex ⟶ 0 edges
- For each new vertex, add at least one edge ⟹ by induction, m ≥ n - 1

# 3. Queue and Stack Data Structures

## 3.1. Queue

- **Type**: First-In, First-Out (FIFO)
- **Operations**:
  - push (enqueue): Add to back
  - pop (dequeue): Remove from front

Example:

Push A, B, C ⟶ Pop order: A, B, C

## 3.2. Stack

- **Type**: Last-In, First-Out (LIFO)
- **Operations**:
  - push: Add to top
  - pop: Remove from top

Example:

Push A, B, C ⟶ Pop order: C, B, A

# 4. Breadth-First Search (BFS)

## 4.1. Algorithm

### Pseudocode

```text
BFS(G, s):
  Initialize queue Q
  Q.push(s)
  discovered[s] = true
  while Q is not empty:
    v = Q.pop()
    for each neighbor w of v:
      if not discovered[w]:
        Q.push(w)
        discovered[w] = true
```

## 4.2. Explanation

- Visit nodes in layers: distance-1 neighbors first, then distance-2, etc.
- Uses queue to manage order of exploration.

## 4.3. Time Complexity

- Initialization: O(n)
- While-loop:
  - Each vertex enqueued once → O(n)
  - For each edge, constant-time check and enqueue → O(m)
- Total Time: O(n + m)

## 4.4. BFS Properties

- Guarantees shortest path distance
- Layered traversal: vertices discovered in order of distance from source

# 5. Depth-First Search (DFS)

## 5.1. Recursive Algorithm

### Pseudocode

```text
DFS(G, s):
  mark s as explored
  for each neighbor v of s:
    if v not explored:
      DFS(G, v)
```

## 5.2. Stack-Based Implementation

### Pseudocode

```text
DFS_stack(G, s):
  Initialize stack S
  S.push(s)
  explored[s] = false for all s
  while S is not empty:
    v = S.pop()
    if not explored[v]:
      explored[v] = true
      for each neighbor w of v:
        S.push(w)
```

## 5.3. Explanation

- The algorithm dives into one path as far as possible before backtracking
- Uses stack to manage path

## 5.4. DFS Traversal Example

Given graph:

```
A --- B --- C
|     |
G     D
      |
      E
```

Start at A, DFS possible order:
- A, B, C, D, E, G

Traversal may vary based on adjacency ordering.

## 5.5. Correctness Proof

If there's a path from s to t, DFS will explore t.

### Proof Strategy:

- Suppose not: there's a path but t not explored.
- Choose earliest unexplored vertex vi on the path from s to t.
- Its predecessor vi−1 on the path was explored.
- Since (vi−1, vi) is an edge, and vi−1 is explored, DFS must call on vi.
- Contradiction: vi was supposedly unexplored.
- Hence, DFS explores all reachable vertices.

## 5.6. Termination

- Each vertex is marked and explored only once.
- Recursive calls are only made for unexplored vertices.

## 5.7. Time Complexity

- Initialization: O(n)
- Stack operations:
  - Each vertex explored once → O(n)
  - Each edge contributes to neighbor check once → O(m)
- For adjacency list:
  - Total time = O(n + m)

# 6. BFS vs DFS Comparison

| Feature                       | Breadth-First Search     | Depth-First Search      |
|------------------------------|--------------------------|-------------------------|
| Data Structure               | Queue                    | Stack                   |
| Visiting Order               | Layers (distance-based)  | Path-like (deep first)  |
| Time Complexity              | O(n + m)                 | O(n + m)                |
| Guarantees Shortest Path     | Yes                      | No                      |
| Space Efficiency             | Depends on graph width   | Depends on graph depth  |
| Ideal for                    | Shortest path            | Topological, components |
| Push Condition               | When node first seen     | When exploring a node   |
| Pop Condition                | Explore immediately      | Explore upon popping    |

## Use Cases

- **BFS**: Shortest path discovery, level-order processing
- **DFS**: Connected components, cycle detection, topological sorting

# Summary

This lecture covered the representation of graphs and two fundamental graph traversal algorithms: breadth-first search (BFS) and depth-first search (DFS).

- Graphs can be represented using adjacency matrices, which are suited for dense graphs and allow constant-time edge existence checks, or adjacency lists, which are more space-efficient for sparse graphs and enable faster iteration over neighbors.
- The concepts of connectivity and edge bounds were introduced, including the fact that a connected graph must have at least n - 1 edges.
- Queues and stacks were reviewed as data structures supporting BFS and DFS respectively.
- BFS explores nodes in layers using a queue and guarantees finding the shortest path. Its time complexity is O(n + m).
- DFS explores as far as possible along a path before backtracking, using either recursion or a stack. It also runs in O(n + m) time.
- Both algorithms were proved to be correct, and a comparative analysis highlighted their tradeoffs and ideal applications.

The lecture emphasized understanding time complexity through degrees of nodes, operation counts, and representations, forming a quantitative foundation for analyzing future graph algorithms.
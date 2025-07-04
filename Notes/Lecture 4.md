# 1. Course Announcements

## 1.1 Homework
- **Homework 1**: Due this Saturday.
- **Homework 2**: Will be released soon; due roughly at the end of next week.
  - Focuses on graph algorithms discussed in this lecture and the next.

## 1.2 Schedule Change for Next Week
- **Flipped Classroom Model**:
  - Lectures will be pre-recorded and posted in advance.
  - Extended office hours: Monday and Wednesday, 8–10 PM.
- **Week 4 onwards**: Normal in-person schedule resumes.

# 2. Introduction to Graphs

## 2.1 Definition of a Graph
- A graph **G** is a tuple (V, E):
  - **V**: Set of **vertices** (also referred to as **nodes**)
  - **E**: Set of **edges** connecting pairs of vertices
- **Undirected Graph**: An edge (u, v) is the same as (v, u)

### 2.1.1 Example
Graph G = (V, E)

- V = {1, 2, 3, 4, 5}
- E = {(1,2), (1,3), (2,5), (3,5)}

Visual Layout:
```
1 -- 2
 \   |
  3--5
  4 (isolated)
```

- This is an undirected graph.
- (1,2) and (2,1) are the same edge.

## 2.2 Exclusions
- **No self-loops**: Edges from a node to itself are excluded.
- **No multi-edges**: Only one edge between any two nodes.

## 2.3 Real World Applications
Graphs are widely used to model various systems:

| System Type        | Vertices Represent | Edges Represent                        |
|--------------------|--------------------|----------------------------------------|
| Airport network    | Airports           | Direct flight routes                   |
| Computer networks  | Computers/servers  | Communication links                    |
| Social networks    | Users              | Friend/follow relationships            |
| Course prerequisites | Courses           | Directed edges for prerequisites       |

Example of a Directed Graph:
- CS31 ⟶ CS32 and CS33 (prerequisite structure)

# 3. Graph Terminology and Notation

## 3.1 Common Variables
- **n**: Number of vertices in graph (|V|)
- **m**: Number of edges in graph (|E|)

## 3.2 Maximum Number of Edges
- For undirected graphs with no self-loops or multi-edges:
  - Max edges: n choose 2 = n(n - 1)/2 ≈ O(n²)

## 3.3 Degree and Neighbors
- **Neighbor**: A node directly connected by an edge.
- **Degree of vertex v**: Number of edges incident to v.

Example:
```
    v
   /|\
  u w x
```
- Neighbors of v: {u, w, x}
- Degree of v: 3

## 3.4 Paths and Cycles

### 3.4.1 Path
- A **path** is a sequence of vertices v₁ to vₖ where each adjacent pair (vᵢ, vᵢ₊₁) is an edge.
- A **simple path**: No repeated vertices.

Example:
- Graph: 1 — 2 — 4
- Simple Path: [1, 2, 4]

### 3.4.2 Cycle
- A **cycle** is a path where the start and end vertices are the same.
- A **simple cycle**: No repeated vertices other than the start/end.

Example:
- Graph: 2 — 3 — 4 — 2
- Cycle: [2, 3, 4, 2]

## Note on Definitions
- A “path” in this course MAY include cycles (can have repeated vertices).
- Wikipedia’s path ≠ our path (their "walk" ~ our "path").

## 3.5 Connected Graphs
- A graph is **connected** if there exists a path between every pair of nodes (u,v).

Example:
- All nodes reachable from each other: Connected
- One or more isolated nodes: Not connected

## 3.6 Connected Component
- **Connected component of S**: Set of all nodes reachable from a node S.

## 3.7 Induced Subgraph
- A subgraph that includes all edges between nodes in the connected component.

## 3.8 Distance
- **Distance between nodes (u,v)**: Length of shortest path between them.
  - If no path exists: Distance = ∞

## 3.9 Tree
- A tree is:
  - **Connected**
  - **Acyclic** (contains no cycles)

# 4. Problem Definitions

## 4.1 ST Connectivity
- Given graph G and nodes S and T:
  - Determine whether a **path** exists from S to T

## 4.2 Distance Between S and T
- Given graph G and nodes S, T:
  - Find the **distance** (shortest path length) from S to T

## 4.3 Connected Component of S
- Find all nodes **reachable** from node S (i.e., nodes in same connected component)

# 5. Graph Traversal Overview

## 5.1 Traversal Intuition
- Simulate exploring a maze with a flashlight.
- Start at node S, expand outward step-by-step.
- Avoid visiting same node twice.

## 5.2 Graph Traversal Strategy
- Prevent infinite loops by **marking discovered nodes**
- Expand outward layer-wise: **Breadth-First Search (BFS)**

# 6. Breadth-First Search (BFS)

## 6.1 Definition and Intuition
- Explore all vertices at **distance 1**, then **distance 2**, and so on.
- Like water flooding from the source node S to neighbors.

Example:
```
Layers:
L0 = {S}
L1 = {neighbors of S}
L2 = {neighbors of L1 not in L0 or L1}
...
```

## 6.2 Pseudocode

```python
BFS(G = (V, E), s):
    L0 = {s}
    mark s as discovered
    i = 0

    while Li is not empty:
        Li+1 = empty set
        for each u in Li:
            for each edge (u,v):
                if v not discovered:
                    add v to Li+1
                    mark v as discovered
        i = i + 1
```

## 6.3 Example

```
Graph:

    S
   / \
  1   5
 /     \
4       6
 \     /
   3
  / \
 2   7
      \
       8

Layered BFS:

L0 = {S}
L1 = {1, 5}
L2 = {4, 6}
L3 = {3}
L4 = {2, 7}
L5 = {8}
```

- Each layer Lᵢ contains nodes at distance i from source S.

## 6.4 Discover Set
- Keeps track of all previously visited nodes.
- Prevents reprocessing and infinite loops.

# 7. BFS Lemma and Proofs

## 7.1 Lemma
> For each j ≥ 0, layer Lⱼ produced by BFS contains all nodes at distance exactly j from s.

### 7.1.1 Proof Technique
- Use **mathematical induction** on j.

### Base Case (j = 0)
- L₀ = {s}, and s is 0 distance from itself.

### Inductive Hypothesis
- Assume statement is true for all j ≤ k.

### Inductive Step
- Show Lₖ₊₁ consists of nodes at distance k+1.

#### Part 1: If v ∈ Lₖ₊₁ → dist(s,v) = k+1
- v must be neighbor of node u ∈ Lₖ
- So path to v is length k+1
- If shorter path to v existed, v would’ve been discovered earlier

#### Part 2: If dist(s,v) = k+1 → v ∈ Lₖ₊₁
- Let u be the predecessor of v on shortest path of length k+1
- Then u is distance k from s, hence in Lₖ
- v is neighbor of u, and since undiscovered, will be added to Lₖ₊₁

## 7.2 BFS Termination Bound
> BFS terminates after at most n iterations of the while loop

### Justification
- Each node can only be discovered once
- BFS only continues when new nodes are discovered
- Hence, layers beyond n can't exist (or Lₙ will be empty)

# 8. Applications of BFS

## 8.1 Determine ST Connectivity
```python
def is_connected(G, s, t):
    Run BFS from s
    Return True if t is discovered, False otherwise
```

## 8.2 Compute Distance
```python
def get_distance(G, s, t):
    Run BFS from s
    Return layer number containing t (distance)
    If t not discovered: return ∞
```

## 8.3 Find Connected Component
```python
def connected_component(G, s):
    Run BFS from s
    Return list of all discovered nodes
```

# 9. Summary

This lecture introduced graph algorithms with a focus on traversal-based problems. It began with formal definitions of graphs and related concepts such as neighbors, degrees, paths, cycles, connectedness, and components. The lecture employed breadth-first search (BFS) to methodically explore node reachability and distances from a source node S. The BFS algorithm was formalized, and its correctness was established through inductive proofs. Finally, practical applications—such as determining if nodes are connected, computing shortest-path distances, and extracting connected components—were demonstrated through direct use of BFS traversal.
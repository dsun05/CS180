# 1. Course Announcements

## 1.1 Homework Details
- Homework 1 was released last week and is due Saturday.
- Topics Covered: Big-O notation and Gale-Shapley algorithm.
- Grading Policy:
  - 3 problems graded on correctness.
  - Remaining problems graded on completeness (reasonable effort required for full credit).
- Algorithm Type Questions:
  - Must prove correctness.
  - Generally, must provide time complexity analysis unless otherwise specified.
- Correctness Proof Guidelines:
  - Assume an average student in the class reads your proof — must be convincing to them.
  - Obvious steps from the algorithm may not need proof (e.g., that hospitals propose in decreasing order of preference in Gale-Shapley).
  - Non-obvious claims (e.g., stability of output) require a proof.
- Time Complexity Analysis Guidelines:
  - Aim for clarity so that another student could implement your algorithm with minimal effort.
  - Discuss time complexity in light of the data structures used.
  - Nested loops can be approximated by multiplying iteration bounds.

## 1.2 Resources
- Lecture notes and video recordings posted after each lecture.
- Supplementary Notes:
  - Summaries and skeletal outlines of textbook concepts.
  - May lack examples and diagrams.
- Textbook Slides:
  - Link posted under week one resources.
  - Created for the course textbook, but not used during lectures.
  - Can enhance understanding of proofs or concepts.
- Practice Problems:
  - Textbooks, homework sets, LeetCode, and other online platforms.
- Reminder: Do not Google homework problems directly for answers.

---

# 2. Big-O Notation and Algorithm Efficiency

## 2.1 Motivation and Use
- Aim: Analyze algorithm efficiency independent of implementation or hardware.
- Measured in number of "basic steps" (e.g., addition, assignment, array indexing).
- Flexibility allows modeling differences in hardware or instruction costs.
- Big-O notation is used to describe the upper bound of the runtime.

## 2.2 Big-O Notation Definition
Let f(n) and g(n) be functions from the natural numbers to the real numbers.

> We say f(n) ∈ O(g(n)) if:
>
> ∃ constants c > 0 and n₀ ≥ 0 such that ∀ n ≥ n₀:
> f(n) ≤ c × g(n)

- f(n): Actual runtime function.
- g(n): Reference function used as an upper bound.
- c: Multiplicative constant accounting for machine-level factors.

### Diagram Description
- X-axis: Input size (n).
- Y-axis: Runtime (f(n)).
- For large enough n, f(n) is below c × g(n).

## 2.3 Example: Nested Loops

### Code Snippet:
```cpp
for (int i = 0; i < n; ++i)
  for (int j = 0; j < n; ++j)
    printf("Hello");
```

### Analysis:
- `printf` is assumed to be O(1)
- Total steps:
  - n² `printf` calls
  - n² + n loop increments
  - n² + n condition checks
  - n + 1 initializations
- Total steps ≈ 3n² + 3n + 1
- Asymptotically:
  - f(n) ∈ O(n²)

> Note: Detailed step counts are unnecessary for homework/exams. High-level reasoning suffices.

---

# 3. Properties of Big-O and Related Notations

## 3.1 Set-Theoretic Definition
- O(g(n)) is a set of functions.
- f(n) ∈ O(g(n)) indicates f belongs to this set.
- Notational shorthand:
  - f(n) = O(g(n)) (abuse of equality)

## 3.2 Algebraic Rules and Properties

| Property | Description |
|----------|-------------|
| f(n) ∈ O(f(n)) | A function is upper bounded by itself. |
| c·f(n) ∈ O(f(n)) | Multiplication by constant doesn’t change asymptotic class. |
| If f₁ ∈ O(g₁), f₂ ∈ O(g₂) ⇒ f₁ + f₂ ∈ O(max(g₁, g₂)) | Use upper bound of the dominant term. |
| If f₁ ∈ O(g₁), f₂ ∈ O(g₂) ⇒ f₁·f₂ ∈ O(g₁·g₂) | Multiplicative closure. |
| If f ∈ O(g), g ∈ O(h) ⇒ f ∈ O(h) | Transitivity property. |

## 3.3 Addition and Multiplication in Context

| Operation | Example | Result |
|-----------|---------|--------|
| Addition | Multiple parts of an algorithm | Use max(g₁, g₂) |
| Multiplication | Looping an O(1) code n times | O(n) · O(1) = O(n) |

---

# 4. Common Big-O Expression Hierarchy

From smallest to largest:

| Complexity | Name |
|------------|------|
| O(1)      | Constant time |
| O(log log n) | Doubly logarithmic |
| O(√log n), O(logⁿ n) | Sublogarithmic / polylogarithmic |
| O(n^ε), 0<ε<1 | Sublinear |
| O(n)      | Linear |
| O(n log n) | Linearithmic |
| O(n²), O(n³) | Polynomial |
| O(2ⁿ), O(3ⁿ) | Exponential |
| O(n!)     | Factorial |
| O(nⁿ)     | Super-exponential |

> Note:
> - Exponential time typically means "n in the exponent".
> - Polynomial time is considered **efficient**.

---

# 5. Theoretical Efficiency and Definitions

## 5.1 Polynomial Time
- f(n) ∈ O(nᶜ) for some constant c ≥ 1
- Composability: summing, multiplying polynomial-time functions yields polynomial-time results.
- Used widely in theoretical computer science.

### Examples:
| f(n) | Polynomial Time? |
|------|------------------|
| 3n² + 5n + 1 | Yes |
| n³ · log n   | Yes |
| 2ⁿ | No |

## 5.2 Efficient Algorithm
- Defined as an algorithm whose worst-case runtime is polynomial in the input size.

---

# 6. Little-O, Big-Omega, and Theta Notation

## 6.1 Summary Definitions

| Notation | Meaning |
|----------|---------|
| f(n) ∈ o(g(n)) | f grows strictly slower than g |
| f(n) ∈ O(g(n)) | f is asymptotically ≤ g (upper bound) |
| f(n) ∈ Ω(g(n)) | f is asymptotically ≥ g (lower bound) |
| f(n) ∈ ω(g(n)) | f grows strictly faster than g |
| f(n) ∈ Θ(g(n)) | f and g grow at the same rate (tight bound) |

## 6.2 Inclusions
- Θ(g(n)) ⊆ O(g(n)) and also ⊆ Ω(g(n))
- If f ∈ Θ(g), then f ∉ o(g) and f ∉ ω(g)

---

# 7. Time Complexity Analysis of Gale-Shapley Algorithm

## 7.1 Algorithm Overview
- Input: Preference lists for n hospitals and n students.
- Goal: Produce a stable matching.
- Key Actions:
  - Hospitals make proposals.
  - Students accept best offer.
  - Repeat until all hospitals are matched.

## 7.2 Input and Output Representations

### Input
- Hospital preference lists (n stacks): Most-preferred student on top.
- Student preference lists (transformed to 2D array later).

### Output
- Two size-n arrays:
  - `hospital[h] = s` if h is matched to student s; -1 otherwise.
  - `student[s] = h` similarly.

## 7.3 Supporting Data Structures

- Queue `free_hospitals`: Track unmatched hospitals that haven't proposed to every student.
- 2D array `student_pref[s][h]`: Rank of hospital h in student s’s preferences.

## 7.4 Step-by-Step Analysis

### Initialization Costs

| Task | Cost |
|------|------|
| Initialize `hospital`, `student` arrays | O(n) each |
| Initialize `free_hospitals` queue | O(n) |
| Convert student preference stacks to 2D array (`student_pref`) | O(n²) |

### Inner Loop Costs (Per Iteration)

| Step | Cost |
|------|------|
| Find unmatched hospital | O(1) (via queue) |
| Find next student to propose to | O(1) (pop from stack) |
| Determine if student is matched | O(1) |
| Compare two hospital rankings | O(1) (via `student_pref`) |
| Add/remove matchings | O(1) |
| Update queue | O(1) |

### Number of Iterations
- Each hospital proposes to each student at most once.
- Up to n² total proposals.
- So, O(n²) total iterations.

### Total Time Complexity

| Component | Time |
|-----------|------|
| Initialization | O(n²) |
| Matching loop | O(n²) × O(1) = O(n²) |
| **Total** | O(n²) |

> All intermediate steps are optimized for constant-time performance through appropriate data structures.

---

# 8. Summary

This lecture covered the formal foundations and practical applications of algorithm analysis using Big-O and related notations. Big-O notation provides an architecture-agnostic measure of algorithm performance focusing on input size. The lecture detailed formal definitions, equivalency rules, arithmetic properties, and a hierarchy of common functions for runtime analysis. Efficient algorithms were defined as those operating in polynomial time. Additional notations (Θ, Ω, o, ω) were introduced for more precise characterizations including tight and lower bounds.

The Gale-Shapley algorithm was revisited to analyze its time complexity in depth. By choosing appropriate data structures (arrays, stacks, queues), and identifying where to optimize access and comparisons, the algorithm was shown to operate in O(n²) time. Techniques emphasized included modular breakdown of algorithm steps, selection of data structures to enable constant-time operations, and conservative upper-bound calculations using Big-O rules.
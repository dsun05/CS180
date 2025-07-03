# 1. Overview of Course Expectations and Structure

- Sessions will be recorded, but live attendance is highly preferred.
- Sessions focus on going over concepts briefly, followed by collaborative problem-solving, discussions, and Q&A.
- The course involves proving properties of algorithms:
  - Time complexity
  - Termination
  - Correctness

# 2. Proof Techniques

## 2.1. Direct Proof

- A method in which the proof proceeds logically from assumptions to conclusion in a straightforward manner.

### Definition
If you have a statement "If A, then B", you assume A is true and logically deduce B.

### Example: Sum of Two Rational Numbers is Rational

- Let \( a/b \) and \( c/d \) be rational numbers (where \( a, b, c, d \) are integers and \( b, d ≠ 0 \)).
- Their sum:

  \[
  \frac{a}{b} + \frac{c}{d} = \frac{ad + bc}{bd}
  \]
  
  Since \( ad + bc \) and \( bd \) are integers, the result is a rational number.

## 2.2. Proof by Contradiction

- Assume the negation of the statement you want to prove.
- Derive a contradiction (a falsehood), thereby verifying that the original statement must be true.

### Example: Prove that \( \sqrt{2} \) is Irrational

1. Assume \( \sqrt{2} \) is rational, i.e. \( \sqrt{2} = a/b \), where \( \gcd(a, b) = 1 \).
2. Square both sides: \( 2 = a^2 / b^2 \) → \( 2b^2 = a^2 \)
3. Then \( a^2 \) is even → \( a \) is even → \( a = 2k \)
4. Substituting, \( 2b^2 = (2k)^2 = 4k^2 \) → \( b^2 = 2k^2 \) → \( b \) is even
5. Contradiction: both \( a \) and \( b \) are even → \( \gcd(a,b) ≠ 1 \)

Therefore, \( \sqrt{2} \) is irrational.

### Generalization Discussion

- If \( \sqrt{k} \not\in \mathbb{Z} \) for integer \( k \), then it's irrational.
- Using similar contradiction logic, one can show that if \( \sqrt{k} = a/b \), and \( \sqrt{k} \not\in \mathbb{Z} \), then both \( a \) and \( b \) would share \( \sqrt{k} \) as a factor, which violates the condition that \( \gcd(a, b) = 1 \) in integers.

## 2.3. Mathematical Induction

### Structure

- Use when you want to prove a proposition, \( P(n) \), is true for all \( n \in \mathbb{N} \):

#### Base Case
Prove \( P(1) \).

#### Inductive Step
Assume \( P(k) \) is true, and show this implies \( P(k + 1) \) is also true.

### Example: Sum of First \( n \) Positive Integers

Claim:
\[
1 + 2 + \ldots + n = \frac{n(n + 1)}{2}
\]

#### Base Case (n = 1)
\[
1 = \frac{1(1 + 1)}{2} = 1
\]

#### Inductive Step
Assume:
\[
1 + \ldots + k = \frac{k(k + 1)}{2}
\]

Consider:
\[
1 + 2 + \ldots + k + (k + 1) = \frac{k(k + 1)}{2} + (k + 1)
\]
\[
= \frac{k(k + 1) + 2(k + 1)}{2} = \frac{(k + 1)(k + 2)}{2}
\]

Therefore,
\[
P(k) \Rightarrow P(k + 1)
\]

Hence, claim holds for all \( n ≥ 1 \).

## 2.4. De Morgan’s Laws

Rules for negating logical statements:

| Original                          | Negated Form                          |
|-----------------------------------|----------------------------------------|
| \( \neg (A \lor B) \)            | \( \neg A \land \neg B \)             |
| \( \neg (A \land B) \)           | \( \neg A \lor \neg B \)             |
| \( \neg (\exists x\ P(x)) \)     | \( \forall x\ \neg P(x) \)           |
| \( \neg (\forall x\ P(x)) \)     | \( \exists x\ \neg P(x) \)           |

# 3. Asymptotic Notation

## 3.1. Motivation

- Measures complexity (usually time) of an algorithm as a function of input size \( n \).
- Avoid reliance on machine-specific or constant-factor variation.
- Focuses on how algorithm performance scales with input size.

## 3.2. Big-O Notation (O)

### Formal Definition
If \( f(n) \) and \( g(n) \) are functions, then:

\[
f(n) \in O(g(n)) \Leftrightarrow \exists c, n_0 > 0, \forall n \geq n_0: f(n) \leq c \cdot g(n)
\]

### Interpretation
- \( f(n) \) grows no faster than \( g(n) \) up to constant factors.
- Commonly used to upper bound time complexity.

### Example

| Function A | Function B | Relation    |
|------------|------------|-------------|
| 100n       | \( n^2 \)  | \( 100n \in O(n^2) \) |
| \( \log n \) | \( n \)     | \( \log n \in O(n) \) |
| \( n^k \)   | \( 2^n \)   | \( n^k \in O(2^n) \) |

## 3.3. Big-Omega (Ω)

### Definition
\[
f(n) \in \Omega(g(n)) \Leftrightarrow \exists c, n_0 > 0, \forall n \geq n_0: f(n) \geq c \cdot g(n)
\]

- Describes a lower bound.
- \( f(n) \) grows at least as fast as \( g(n) \).

## 3.4. Big-Theta (Θ)

### Definition
\[
f(n) \in \Theta(g(n)) \Leftrightarrow f(n) \in O(g(n)) \; \text{and} \; f(n) \in \Omega(g(n))
\]

- Tight bound: \( f(n) \) grows at the same rate as \( g(n) \), asymptotically.

## 3.5. Little-o

### Definition
\[
f(n) \in o(g(n)) \Leftrightarrow \forall c > 0, \exists n_0, \forall n \geq n_0: f(n) \leq c \cdot g(n)
\]

- \( f(n) \) grows strictly slower than \( g(n) \)
- Eliminates the possibility of \( f(n) \in \Theta(g(n)) \)

### Examples

| \( f(n) \)       | \( g(n) \) | Relation         |
|------------------|------------|------------------|
| \( \log n \)     | \( n \)    | \( f \in o(g) \) |
| \( n^2 \)        | \( n^3 \)  | \( f \in o(g) \) |

## 3.6. Use Cases

| Asymptotic Class | Use for       |
|------------------|---------------|
| Big-O (O)        | Upper bounds  |
| Big-Omega (Ω)    | Lower bounds  |
| Big-Theta (Θ)    | Exact bounds  |
| Little-o (o)     | Strict upper  |

## 3.7. Motivation Recap

- Notations help ignore constants, system differences, and focus on scalability.
- For example, when analyzing time complexity across models of computation or for large input values.

# 4. Gale–Shapley Algorithm (Stable Matching Problem)

## 4.1. Problem Setup

- Two sets:
  - Hospitals: \( H = \{ h_1, h_2, ..., h_n \} \)
  - Students: \( S = \{ s_1, s_2, ..., s_n \} \)

Each entity ranks all entities in the opposite set.

### Definitions

- **Matching**: A set of pairs \( (h, s) \) such that each hospital and student appears in at most one pair.
- **Perfect Matching**: Each hospital and student appear in exactly one pair.
- **Instability**: Exists when:
  - \( h \) is matched to \( s \)
  - \( h' \) is matched to \( s' \)
  - \( h \) prefers \( s' \) to \( s \)
  - \( s' \) prefers \( h \) to \( h' \)

Such situations encourage partners to break their assignment.

### Goal

- Find a perfect matching with no instabilities (i.e. find a stable matching).

## 4.2. Gale–Shapley Algorithm

### Initialization

- Start with empty matching \( M = \emptyset \)

### Main Loop

While there exists an unmatched hospital \( h \):

1. Let \( s \) be the highest-ranked student on \( h \)'s list not yet proposed to.
2. If \( s \) is unmatched:
   - Match \( h \) and \( s \)
3. If \( s \) is matched to \( h' \):
   - If \( s \) prefers \( h \) over \( h' \):
     - Match \( s \) to \( h \)
     - \( h' \) becomes unmatched
   - Else:
     - \( h \) crosses \( s \) off the list (no further proposals)

### Termination

- Return matching \( M \)

## 4.3. Analysis and Properties

### Theorem 1: Termination in at Most \( n^2 \) Steps

- Each hospital makes a proposal to each student at most once
- \( n \) hospitals × \( n \) students = \( n^2 \) total proposals at most

### Theorem 2: Always Returns a Stable Matching

- No pair \( (h, s') \) will prefer each other over their current matches when the algorithm terminates

### Theorem 3: A Stable Matching Always Exists

- Follows directly from Theorem 1 and 2
- Since Gale-Shapley always terminates and returns a stable matching, such a matching always exists.

## 4.4. Additional Notes

- The algorithm can be viewed as hospital-optimal or student-optimal depending on who proposes.
- If hospitals propose, the result is best for hospitals and worst for students (relative to all possible stable matchings).
- The output is deterministic given fixed rankings and proposal order.

# Summary

This lecture reviewed foundational proof techniques, asymptotic notation, and introduced the problem of stable matching along with the Gale-Shapley algorithm. Three proof methods were covered in depth: direct proof, proof by contradiction, and mathematical induction. De Morgan's Laws and logic negation rules were refreshed. Asymptotic notation including Big-O, Big-Omega, Big-Theta, and Little-o were defined and illustrated with examples. Finally, the Gale-Shapley algorithm was discussed with formal definitions of matching, perfect matching, and stability, followed by the algorithm’s correctness, termination, and guarantees of generating stable matchings.
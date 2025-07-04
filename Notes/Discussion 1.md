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

- Let $a/b$ and $c/d$ be rational numbers (where $a, b, c, d$ are integers and $b, d \ne 0$).
- Their sum:
$$\frac{a}{b} + \frac{c}{d} = \frac{ad + bc}{bd}$$
Since $ad + bc$ and $bd$ are integers, the result is a rational number.

## 2.2. Proof by Contradiction

- Assume the negation of the statement you want to prove.
- Derive a contradiction (a falsehood), thereby verifying that the original statement must be true.

### Example: Prove that $\sqrt{2}$ is Irrational

1. Assume $\sqrt{2}$ is rational, i.e., $\sqrt{2} = a/b$, where $\gcd(a, b) = 1$.
2. Square both sides: $2 = a^2 / b^2 \implies 2b^2 = a^2$
3. Then $a^2$ is even $\implies a$ is even $\implies a = 2k$
4. Substituting, $2b^2 = (2k)^2 = 4k^2 \implies b^2 = 2k^2 \implies b$ is even
5. Contradiction: both $a$ and $b$ are even $\implies \gcd(a,b) \ne 1$

Therefore, $\sqrt{2}$ is irrational.

### Generalization Discussion

- If $\sqrt{k} \not\in \mathbb{Z}$ for integer $k$, then it's irrational.
- Using similar contradiction logic, one can show that if $\sqrt{k} = a/b$, and $\sqrt{k} \not\in \mathbb{Z}$, then both $a$ and $b$ would share a common factor related to $k$, which violates the condition that $\gcd(a, b) = 1$.

You are correct. The `aligned` environment is the standard, but let's try a different, more universally supported presentation for the derivation to ensure it renders correctly for you.

Here is the corrected "Mathematical Induction" section with a focus on ensuring the inductive step's formatting is robust.

***

## 2.3. Mathematical Induction

### Structure

- Use when you want to prove a proposition, $P(n)$, is true for all integers $n$ from a starting point (e.g., for all $n \ge 1$).

#### Base Case
Prove the proposition is true for the first value, e.g., prove $P(1)$.

#### Inductive Step
Assume the proposition $P(k)$ is true for an arbitrary integer $k$, and then use this assumption to prove that $P(k + 1)$ must also be true.

### Example: Sum of First $n$ Positive Integers

**Claim:** For any integer $n \ge 1$, the following formula holds:
$$1 + 2 + \ldots + n = \frac{n(n + 1)}{2}$$

---

#### Base Case ($n = 1$)
We test the formula for the first case, $n=1$.
$$1 = \frac{1(1 + 1)}{2} = \frac{2}{2} = 1$$
The base case is true.

---

#### Inductive Step

**1. Inductive Hypothesis:** Assume the formula is true for some arbitrary integer $k \ge 1$:

$$
1 + 2 + \ldots + k = \frac{k(k + 1)}{2}
$$

**2. Goal:** We need to prove the formula is also true for $k+1$. We want to show:

$$
1 + 2 + \ldots + k + (k + 1) = \frac{(k+1)((k+1) + 1)}{2} = \frac{(k + 1)(k + 2)}{2}
$$

**3. Derivation:** Let's start with the left-hand side of the goal equation and use our inductive hypothesis.

$$
\begin{aligned}
\text{Sum for } k+1 &= (1 + 2 + \ldots + k) + (k + 1) \\
&= \left( \frac{k(k + 1)}{2} \right) + (k + 1) \\
&= \frac{k(k + 1)}{2} + \frac{2(k + 1)}{2} \\
&= \frac{k(k + 1) + 2(k + 1)}{2} \\
&= \frac{(k + 1)(k + 2)}{2}
\end{aligned}
$$

This result matches the right-hand side of our goal. We have successfully shown that if the formula holds for $k$, it must also hold for $k+1$.

Therefore, by the principle of mathematical induction, the claim is true for all integers $n \ge 1$.

---

## 2.4. De Morgan’s Laws

Rules for negating logical statements:

| Original | Negated Form |
| :--- | :--- |
| $\neg (A \lor B)$ | $\neg A \land \neg B$ |
| $\neg (A \land B)$ | $\neg A \lor \neg B$ |
| $\neg (\exists x\; P(x))$ | $\forall x\; \neg P(x)$ |
| $\neg (\forall x\; P(x))$ | $\exists x\; \neg P(x)$ |

# 3. Asymptotic Notation

## 3.1. Motivation

- Measures complexity (usually time) of an algorithm as a function of input size $n$.
- Avoids reliance on machine-specific or constant-factor variation.
- Focuses on how algorithm performance scales with input size.

## 3.2. Big-O Notation (O)

### Formal Definition
If $f(n)$ and $g(n)$ are functions, then:
$$f(n) \in O(g(n)) \iff \exists c, n_0 > 0, \forall n \ge n_0: f(n) \le c \cdot g(n)$$

### Interpretation
- $f(n)$ grows **no faster than** $g(n)$ up to constant factors.
- Commonly used to **upper bound** time complexity.

### Example

| Function A | Function B | Relation |
| :--- | :--- | :--- |
| $100n$ | $n^2$ | $100n \in O(n^2)$ |
| $\log n$ | $n$ | $\log n \in O(n)$ |
| $n^k$ | $2^n$ | $n^k \in O(2^n)$ |

## 3.3. Big-Omega (Ω)

### Definition
$$f(n) \in \Omega(g(n)) \iff \exists c, n_0 > 0, \forall n \ge n_0: f(n) \ge c \cdot g(n)$$

- Describes a **lower bound**.
- $f(n)$ grows **at least as fast as** $g(n)$.

## 3.4. Big-Theta (Θ)

### Definition
$$f(n) \in \Theta(g(n)) \iff f(n) \in O(g(n)) \; \text{and} \; f(n) \in \Omega(g(n))$$

- Describes a **tight bound**: $f(n)$ grows at the same rate as $g(n)$, asymptotically.

## 3.5. Little-o (o)

### Definition
$$f(n) \in o(g(n)) \iff \forall c > 0, \exists n_0, \forall n \ge n_0: f(n) < c \cdot g(n)$$

- $f(n)$ grows **strictly slower than** $g(n)$.
- This implies that $\lim_{n \to \infty} \frac{f(n)}{g(n)} = 0$.

### Examples

| $f(n)$ | $g(n)$ | Relation |
| :--- | :--- | :--- |
| $\log n$ | $n$ | $f \in o(g)$ |
| $n^2$ | $n^3$ | $f \in o(g)$ |

## 3.6. Use Cases

| Asymptotic Class | Use for |
| :--- | :--- |
| Big-O (O) | Upper bounds |
| Big-Omega (Ω) | Lower bounds |
| Big-Theta (Θ) | Exact bounds |
| Little-o (o) | Strict upper bounds |

## 3.7. Motivation Recap

- Notations help ignore constants and system differences to focus on scalability.
- Essential for analyzing algorithm efficiency for large inputs across different computational models.

# 4. Gale–Shapley Algorithm (Stable Matching Problem)

## 4.1. Problem Setup

- Two sets of equal size $n$:
  - Hospitals: $H = \{ h_1, h_2, ..., h_n \}$
  - Students: $S = \{ s_1, s_2, ..., s_n \}$
- Each entity has a ranked preference list of all entities in the opposite set.

### Definitions

- **Matching**: A set of pairs $(h, s)$ where each hospital and student appears in at most one pair.
- **Perfect Matching**: Each hospital and student appears in exactly one pair.
- **Instability**: A pair of assignments $(h, s)$ and $(h', s')$ form an instability if there exists another pair $(h, s')$ who prefer each other over their current partners. Formally:
  - $h$ is matched to $s$ and $h'$ is matched to $s'$.
  - $h$ prefers $s'$ over $s$.
  - $s'$ prefers $h$ over $h'$.
- **Stable Matching**: A perfect matching with no instabilities.

### Goal

- Find a perfect and stable matching.

## 4.2. Gale–Shapley Algorithm

### Initialization
- Start with an empty matching $M = \emptyset$.
- All hospitals are unmatched.

### Main Loop

**While** there exists an unmatched hospital $h$:
1. Let $s$ be the highest-ranked student on $h$'s list to whom $h$ has not yet proposed.
2. **If** $s$ is unmatched:
   - Match $(h, s)$ and add the pair to $M$.
3. **Else** ($s$ is currently matched to some $h'$):
   - **If** $s$ prefers $h$ over her current partner $h'$:
     - Unmatch $(h', s)$ and remove the pair from $M$.
     - Match $(h, s)$ and add the pair to $M$.
     - $h'$ becomes unmatched.
   - **Else** ($s$ prefers $h'$ over $h$):
     - $h$ remains unmatched. $s$ rejects $h$.

### Termination
- The loop terminates when no hospitals are unmatched. Return the matching $M$.

## 4.3. Analysis and Properties

### Theorem 1: Termination
The algorithm terminates in at most $n^2$ iterations.
- Each hospital proposes to each student at most once. Since there are $n$ hospitals and $n$ students, there can be at most $n \times n = n^2$ total proposals.

### Theorem 2: Stability
The algorithm always returns a stable matching.
- **Proof by contradiction**: Assume there is an instability $(h, s')$. This means $h$ prefers $s'$ to his final partner $s$, and $s'$ prefers $h$ to her final partner $h'$.
- By the algorithm's logic, $h$ must have proposed to $s'$ before proposing to $s$.
- When $h$ proposed to $s'$, she must have rejected him (either immediately or later for someone better).
- This implies $s'$ preferred her final partner $h'$ over $h$, which contradicts our assumption.

### Theorem 3: Existence of a Stable Matching
A stable matching always exists.
- This follows directly from Theorems 1 and 2. Since the Gale-Shapley algorithm always terminates and always returns a stable matching, such a matching is guaranteed to exist for any set of preferences.

## 4.4. Additional Notes

- The algorithm is **proposer-optimal**. If hospitals propose, the resulting matching is the best possible stable matching for all hospitals and the worst possible for all students.
- The output is **deterministic** for a given set of preference lists.

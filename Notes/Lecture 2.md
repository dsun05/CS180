# 1. Course Announcements and Logistics

## 1.1 Waitlist and Enrollment
- The course waitlist has significantly decreased.
- There is a decent chance waitlisted students may get in, though no guarantees are provided.
- The instructor is in communication with the enrollment office regarding additional spots.
- A few students were involuntarily dropped from the course; this issue is being addressed.

## 1.2 Piazza Access
- A student raised a concern about accessing Piazza with a non-UCLA email.
- Instructor offered to send a manual invite or generate a separate access link.

## 1.3 Homework Deadlines
- Homework 1 will be released soon.
- Original due date: Friday, Week 2.
- New due date: Saturday, Week 2 (due to Friday holiday).

# 2. Stable Matching Problem and Gale-Shapley Algorithm

## 2.1 Problem Statement
- There are `n` hospitals and `n` students.
- Each hospital has a preference list ranking students.
- Each student has a preference list ranking hospitals.
- Goals:
  - To create a matching: Each hospital and student appears in at most one pair.
  - To create a perfect matching: Each hospital is matched with exactly one student, and vice versa.
  - To ensure the matching is stable: No hospital-student pair prefers each other over their current assignments.

### Definitions

| Term              | Definition                                                                                           |
|-------------------|------------------------------------------------------------------------------------------------------|
| Matching           | A set of hospital-student pairs where no hospital or student appears in more than one pair.         |
| Perfect Matching   | A matching with all hospitals and students paired (1-to-1 bijection).                               |
| Instability        | A situation where a hospital H and student S' prefer each other over their current matches.         |
| Stable Matching    | A matching with no instabilities. No pair wants to deviate from their assigned match.              |

## 2.2 Gale-Shapley Algorithm Description
- Inputs: Preference lists for hospitals and students.
- Initially, no matches exist.
- Process:
  1. Each **unmatched hospital** proposes to the highest-ranked student on its list that hasn’t yet rejected it.
  2. Each **student**:
     - Accepts a proposal if currently unmatched.
     - If already matched, chooses the preferred between the current match and new proposal:
       - If the new offer is better, the student switches and the old hospital becomes unmatched.
       - Otherwise, they reject the new proposal.

### Example of Algorithm Steps

| Step | Hospital Action         | Student Response                  |
|------|--------------------------|-----------------------------------|
| 1    | UCLA proposes to Alice   | Alice accepts (unmatched)         |
| 2    | Cedars-Sinai proposes to Alice | Alice prefers Cedars-Sinai → accepts, dumps UCLA |
| 3    | UCLA proposes to next on list | Process continues until all matched |

### Key Mechanics:
- Hospitals propose in order of preference.
- Students only switch if the new offer is better than their current match.
- The algorithm continues until:
  - All hospitals are matched or
  - Each unmatched hospital has been rejected by all students.

## 2.3 Observations About the Algorithm

### Observation 1: Student Behaviors
- Once matched, students always remain matched.
- Students may switch to better hospitals but never become unmatched.
- Student assignments always improve or stay equally preferred.

### Observation 2: Hospital Behaviors
- Hospitals only get worse or equal matches over time.
- Hospitals propose in decreasing preference order.
- When rejected, they move on to their next preference.

## 2.4 Proofs of Properties

### Matching Termination

#### Claim: Gale-Shapley Always Terminates
- Each hospital can make at most `n` offers (1 to each student).
- At most `n` hospitals → `n²` total proposals.
- Hence, the `while` loop performs no more than `n²` iterations.

#### Proof:
Let `n` be the number of hospitals/students.
- At each step, some unmatched hospital makes a new offer.
- Each hospital makes at most `n` offers.
- Thus, the total iterations are bound by `n × n = n²`.

### Matching Validity

#### Claim: Algorithm Always Outputs a Matching
Definitions:
- A matching ensures each hospital and student appear in at most one pair.

Proof Overview:
- Hospitals stop making offers once matched.
- Students only change matches when a better hospital proposes.
- Thus, both hospitals and students end up in at most one pairing.

### Perfect Matching

#### Claim: Algorithm Produces a Perfect Matching

Proof by Contradiction:
1. Assume not perfect ⇒ some hospital H and student S are unmatched.
2. Since `#hospitals = #students`:
   - If H is unmatched, S must also be unmatched.
3. Hospitals exhaust their entire preference list ⇒ H must have proposed to S.
4. Students always accept their first proposal ⇒ S should have matched with H or someone better.
5. Contradiction: how can S be unmatched if H has proposed?

Conclusion: All H and S must be matched ⇒ perfect matching.

### Stable Matching

#### Claim: Output is Stable

Proof by Contradiction:
Assume instability involving:
- H matched with S
- H’ matched with S’
- But H prefers S’ and S’ prefers H ⇒ instability

Two Cases:

| Case                    | Explanation                                                                                                        |
|-------------------------|--------------------------------------------------------------------------------------------------------------------|
| 1. H proposed to S’     | S’ must have rejected H for someone better (H'') ⇒ final match should be better than H ⇒ contradiction            |
| 2. H never proposed to S’ | H proposed to S (less preferred) ⇒ contradicts algorithm's decreasing preference order                            |

Conclusion: Both cases lead to contradiction ⇒ algorithm must produce stable matching.

# 3. Algorithm Analysis: Efficiency and Order Notation

## 3.1 Measuring Efficiency

### Goals:
- Analyze how algorithm runtime scales with input size.
- Time efficiency is the only metric considered in this class.

### Ineffective Approaches:
- Measuring wall-clock/run-time is unreliable due to:
  - Hardware dependence
  - Operating system scheduling
  - Environmental noise

## 3.2 Alternative: Count Basic Steps

### Basic Step Types:
- Arithmetic operations: `+`, `-`, `*`, `/`
- Memory accesses
- Input/Output operations
- Pointer follow-ups and array indexing

## 3.3 Worst-Case Analysis

### Why Worst-Case?
- Robust, consistent across platforms
- Easier to analyze than average-case
- Many critical systems (e.g., planes, medical devices) require guarantees
- Average-case requires improbable accurate input distribution modeling

## 3.4 Order Notation (Big-O)

### Purpose:
- Represent asymptotic upper bounds on runtime
- Drop unnecessary details like:
  - Exact constants
  - Low-order terms

### Definition:

Let `f(n)` and `g(n)` be functions.  
We say `f(n) ∈ O(g(n))` if there exist constants `c > 0` and `n₀` such that:  
`f(n) ≤ c * g(n)` for all `n ≥ n₀`.

### Interpretation:
- For sufficiently large inputs, `f(n)` grows no faster than a constant multiple of `g(n)`.
- Illustrated as: eventually, `f(n)` curve lies below `c * g(n)` curve.

### Graphical Representation:

| N       |             f(n)              |        c * g(n)         |
|---------|-------------------------------|--------------------------|
| small   | may be greater or less        | irrelevant (before n₀)   |
| ≥ n₀    | f(n) ≤ c * g(n) always holds  | significant for analysis |

#### Example:
- Suppose `f(n) = 5n²` and `g(n) = n²`
- Then `f(n) ∈ O(n²)` because `∃ c=5` and `n₀=0` where `f(n) ≤ c*g(n)`

### Ignoring Constants
- Different machines interpret step costs differently (e.g., mult = 2 steps vs 3 steps)
- Big-O abstracts away these issues to focus on general behavior
- Precise constants aren't meaningful in asymptotic analysis

### Common Complexities:

| Big-O        | Name            | Meaning                                |
|--------------|------------------|-----------------------------------------|
| O(1)         | Constant         | Time does not depend on input size      |
| O(log n)     | Logarithmic      | Time grows slowly with input size       |
| O(n)         | Linear           | Time grows proportionally with input    |
| O(n log n)   | Linear-log       | Typical for efficient sorts             |
| O(n²)        | Quadratic        | Common for simple nested loops          |
| O(2ⁿ)        | Exponential      | Infeasible for large inputs             |
| O(n!)        | Factorial        | Very slow for even moderate n           |

# Summary

This lecture reviewed course logistics, explored the stable matching problem via the Gale-Shapley algorithm, and began formal algorithm analysis frameworks. The stable matching problem involves pairing `n` students and `n` hospitals while respecting mutual preferences and ensuring no instabilities. The Gale-Shapley algorithm provides a step-by-step process in which unmatched hospitals propose to students in descending order of preference, and students pick their most preferred offers. The lecture proved — via direct and contradiction methods — that this algorithm always terminates, returns a perfect matching, and guarantees stability.

Finally, the lecture introduced formal tools to analyze algorithm efficiency, distinguishing between practical time measurements and theoretical models. By focusing on worst-case time and abstract "basic steps", the lecture introduced order notation (Big-O), which quantifies how an algorithm's running time scales with input size, independently of hardware or constant factors.
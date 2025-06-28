# CS180 - Lecture 1 Notes (June 23)
## 1. Course Overview and Administrative Information

### 1.1 Course Description
- CS180 is an algorithms class focused on problem-solving using algorithm design and analysis.
- Entirely conducted via Zoom due to student internships.
- Attendance not mandatory but highly recommended for interactivity and engagement.

### 1.2 Teaching Staff
- **Instructor**: Alexis Korb
- **TAs**:
  - Parshon (Discussion 1A)
  - Oliver (Discussion 1B)

### 1.3 Course Materials
- **Textbook**: _Algorithm Design_ (recommended, not required to purchase)
- Lectures interpolate closely with textbook chapters.
- Updated reading schedule will be provided.

### 1.4 Platforms Used
- **GradeScope**: For homework and exam submissions.
- **Piazza**: For course-related content and Q&A.
  - Use email for personal or administrative issues only.
- **MyUCLA**: Final grade repository.

---

## 2. Course Logistics

### 2.1 Format
- Entirely on Zoom, including exams.
- Same Zoom link used for all lectures, office hours, and exams (excluding discussions/TAs).

### 2.2 Duration
- 8-week accelerated quarter (compared to typical 10 weeks).
- Some content will be cut or adjusted.

### 2.3 Exams
- **Midterm**: Monday, Week 5 — 8:00 PM to 10:00 PM
- **Final**: Friday, Week 8 — 7:00 PM to 10:00 PM
- Held via Zoom with proctoring.
- Cheat sheet policy:
  - Midterm: One double-sided sheet (typed or handwritten)
  - Final: Two double-sided sheets (can reuse midterm sheet)

### 2.4 Grading Breakdown
| Component | Weight |
|----------|--------|
| Homework | 20%    |
| Midterm  | 35%    |
| Final    | 45%    |

### 2.5 Homework Policy
- 4-5 assignments
- Three questions graded on correctness, rest on completeness.
- Late Submission Penalties:
  | Time Late     | Credit Received |
  |---------------|-----------------|
  | ≤ 3 hours     | 90%             |
  | ≤ 1 day       | 50%             |
  | > 24 hours    | 0%              |
- Solutions released after 24 hours.
- Double check submissions — no leniency for wrong uploads (unless emergencies).

### 2.6 Regrade Policy
- Regrade requests must be submitted within one week of receiving grades.
- Exception: Final exam has a reduced regrade window due to grading deadlines.

---

## 3. Enrollment and PTE Info

- Current cap: 160 students.
- Only students who need CS180 to graduate are considered for PTEs.
- PTE requests are validated by enrollment office.

---

## 4. Policies

### 4.1 Academic Integrity
- Collaboration on homework allowed, copying is not.
- Must write own solutions and list collaborators.
- Forbidden: Googling or asking AI tools for answers to specific homework questions.

### 4.2 Accessibility
- Contact CAE (Center for Accessible Education) for accommodations.
- CAE will proctor exams via Zoom for eligible students.

---

## 5. Office Hours

- **Instructor Office Hours**: 
  - Normally immediately after class.
  - Additional session: 8–9 PM this week.
  - Possible additional later sessions depending on student needs.

---

## 6. Tips for Success

### 6.1 Good Habits
- Stay on track, start assignments early.
- Ask questions during lectures or in office hours.
- Make use of the textbook and supplementary resources.
- Rewatch recordings and attend alternate time office hours if class time conflicts.

---

## 7. Topic Introduction: What is an Algorithm?

### 7.1 Definition
- A **step-by-step procedure** for solving a problem or accomplishing a task.

### 7.2 Examples
- Sorting algorithms (e.g., bubble, insertion)
- Housing assignments, shipping logistics, medical residency matching

### 7.3 Purpose of This Course
- You won't learn how to solve every problem.
- Instead, gain a **toolbox** of methods and paradigms for problem solving.

---

## 8. Algorithmic Paradigms and Complexity

### 8.1 Two Key Focus Areas
1. **Algorithm Design**: Developing algorithms for problems using common paradigms.
2. **Complexity Analysis**: Comparing algorithms based on their efficiency (time, space).

---

## 9. Nature of the Course

- **Proof Writing**: Required to rigorously prove algorithm correctness.
- **No Coding**: Only pseudocode-level descriptions expected.
- **Implementation Insight**: Algorithms should be sufficiently detailed to implement, even if not required.

---

## 10. Methodology for Solving Problems

### Steps:
1. **Understand the problem**: Play with toy examples, parse all definitions.
2. **Analyze similar problems**: Check if similar problems have known solutions.
3. **Try algorithmic paradigms**: Use known techniques like divide & conquer, greedy, DP.
4. **Analyze and modify solution**: Ensure correctness and efficiency.

---

## 11. Stable Matching Problem

### 11.1 Problem Context
- Students apply to hospitals (residency).
- Each side ranks all options on the opposite side (no ties, full rankings).

### 11.2 Notation
- Set of hospitals `H = {H1, ..., Hn}`
- Set of students `S = {S1, ..., Sn}`

### 11.3 Definitions
- **Matching**: Set of pairs (H, S) where each H and S appears at most once.
- **Perfect Matching**: Each H and S matched exactly once.
- **Stable Matching**: A perfect matching with no **instability**.

#### Instability:
Occurs if:
- Hospital H is matched with S.
- Hospital H' is matched with S'.
- But H prefers S' over S, and S' prefers H over H'.

### 11.4 Goal
Given two full preference lists, find a **stable matching** (if one exists).

### 11.5 Does A Perfect Matching Always Exist?
- Yes, because `|H| = |S|` and one can construct a trivial perfect matching (e.g., H₁ with S₁, H₂ with S₂...)

---

## 12. Example: Alice, Bob, Charlie & 3 Hospitals

### Preferences:
#### Hospitals:
| Hospital     | Preferences       |
|--------------|-------------------|
| Cedars       | Alice > Bob > Charlie |
| UCLA         | Bob > Charlie > Alice |
| Kaiser       | Alice > Charlie > Bob |

#### Students:
| Student | Preferences               |
|---------|----------------------------|
| Alice   | UCLA > Kaiser > Cedars     |
| Bob     | UCLA > Cedars > Kaiser     |
| Charlie | Kaiser > Cedars > UCLA     |

### Resulting Stable Matching:
- **UCLA ↔ Bob**
- **Kaiser ↔ Alice**
- **Cedars ↔ Charlie**

Confirm stability:
- Bob & UCLA are each other's top choice.
- Kaiser prefers Alice, who also prefers Kaiser over Cedars.
- Cedars cannot persuade Alice (her preference is higher at Kaiser).
- All pairs lack incentive to elope.

---

## 13. Can There Be Multiple Stable Matchings?

### Yes, Example:
#### Students: Alice, Bob  
#### Hospitals: UCLA, Cedars  

One stable matching:
- **UCLA ↔ Alice**
- **Cedars ↔ Bob**

Another stable matching:
- **UCLA ↔ Bob**
- **Cedars ↔ Alice**

Based on preference orders, both matchings can be stable depending on who gets first pick.

---

## 14. Gale-Shapley Algorithm

### 14.1 Purpose
To compute a stable matching efficiently (rather than brute force all permutations).

### 14.2 High-Level Pseudocode
1. Initialize empty matching `M`.
2. While some hospital `h` is unmatched and hasn't proposed to all students:
   - Let `s` be the top-ranked student `h` hasn't proposed to.
   - If `s` is unmatched, assign `(h, s)` to `M`.
   - If `s` is matched to `h'`:
     - If `s` prefers `h` over `h'`:
       - Remove `(h', s)` from `M`.
       - Add `(h, s)` to `M`.
     - Else: `s` rejects `h`.
3. Repeat until all hospitals are matched.
4. Return `M`.

### 14.3 Visual Example Walk-Through
(See section 12 again)

### Key Insights:
- Each hospital proposes in order of their preference list.
- Students always tentatively accept their best offer so far.
- Algorithm terminates with a stable matching.

---

## 15. Properties of Gale-Shapley

- Guarantees a stable matching always exists.
- Final matching is preferrable to the proposing side (here, hospitals):
  - Hospitals get their best possible stable match.
  - Students get their worst possible match among stable matches.

---

## Summary

This lecture introduced the structure, policies, and expectations of CS180, a course on algorithm design and analysis. The instructor discussed the logistics of course delivery, grading, collaboration policies, and how to succeed. The lecture introduced approaches for solving algorithmic problems, emphasizing the importance of deeply understanding problem definitions. The course launched into the stable matching problem as a foundational example, defining key terms such as matching, perfect matching, and stability. Through an illustrative example involving hospitals and students, the Gale-Shapley algorithm was introduced—an efficient method for computing stable matchings used in real-world applications like medical residencies. The lecture concluded with the proof idea that a stable matching always exists, laying the groundwork for further analysis and proofs in upcoming lectures.

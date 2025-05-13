# Functional Dependencies and Normalization Guide

## Functional Dependencies

### What is a Functional Dependency?

A functional dependency (FD) X → Y means that the values of attribute set X uniquely determine the values of attribute set Y. In other words, if two tuples have the same values for X, they must have the same values for Y.

### Example:
- `StudentID → Name, Address` means if we know a StudentID, we can determine exactly one Name and Address.
- `{CourseNum, Semester} → InstructorID` means the combination of CourseNum and Semester uniquely determines the InstructorID.

### Key Rules (Armstrong's Axioms):

1. **Reflexivity**: If Y ⊆ X, then X → Y
2. **Augmentation**: If X → Y, then XZ → YZ
3. **Transitivity**: If X → Y and Y → Z, then X → Z

### Additional Inference Rules:

4. **Union**: If X → Y and X → Z, then X → YZ
5. **Decomposition**: If X → YZ, then X → Y and X → Z
6. **Pseudotransitivity**: If X → Y and WY → Z, then WX → Z

### Attribute Closure

- The attribute closure X⁺ is the set of all attributes functionally determined by X
- Calculate X⁺ to determine if X is a superkey (X⁺ contains all attributes)
- X is a candidate key if it's a minimal superkey (no proper subset of X is a superkey)

## Normalization Forms

### First Normal Form (1NF)
- Each attribute contains only atomic (indivisible) values
- No repeating groups
- Every tuple is unique

### Second Normal Form (2NF)
- Must be in 1NF
- No partial dependencies (non-key attributes must depend on the whole key)
- A relation is in 2NF if for every non-trivial FD X → A, either:
    - X is a superkey, or
    - A is part of a candidate key

### Third Normal Form (3NF)
- Must be in 2NF
- No transitive dependencies (non-key attributes cannot depend on other non-key attributes)
- A relation is in 3NF if for every non-trivial FD X → A, at least one of:
    - X is a superkey
    - A is a prime attribute (part of some candidate key)

### Boyce-Codd Normal Form (BCNF)
- Stronger than 3NF
- For every non-trivial FD X → Y, X must be a superkey
- In simple terms: every determinant must be a candidate key

### Comparison of 3NF and BCNF
- All BCNF relations are in 3NF
- Not all 3NF relations are in BCNF
- The key difference: 3NF allows non-superkey determinants if they determine prime attributes

## Decomposition

### Lossless-Join Decomposition
- A decomposition of R into R₁ and R₂ is lossless if and only if either:
    - (R₁ ∩ R₂) → (R₁ - R₂), or
    - (R₁ ∩ R₂) → (R₂ - R₁)
- In simpler terms: the common attributes must be a superkey for at least one of the relations

### Dependency Preservation
- A decomposition preserves dependencies if every FD from the original relation is either:
    - Directly preserved in one of the decomposed relations, or
    - Derivable from the FDs in the decomposed relations

## Finding Candidate Keys

### Steps to Find Candidate Keys:
1. Identify attributes that don't appear on the right side of any FD (these must be part of every candidate key)
2. Compute the closure of these attributes
3. If the closure includes all attributes, you've found a candidate key
4. If not, add additional attributes and check again
5. Ensure minimality by checking if any attribute can be removed

## Exam Tips

1. **Know the definitions** of each normal form precisely
2. **Practice finding candidate keys** given functional dependencies
3. **Check for normal forms** systematically:
    - First check for 1NF (atomic values)
    - Then check for 2NF (no partial dependencies)
    - Then check for 3NF (no transitive dependencies)
    - Then check for BCNF (all determinants are superkeys)
4. **Test for lossless join** when decomposing relations
5. **Draw dependency diagrams** to visualize complex FD relationships

## Example Problems

### Example 1: Finding Candidate Keys
Consider relation R = (A, B, C, D, E) with FDs:
- AB → C
- CD → E
- E → A

1. Start with attributes not on the right side: B and D
2. Compute (BD)⁺ = {B, D}
3. Add C: (BCD)⁺ = {B, C, D, E, A} (all attributes)
4. Check if minimal:
    - Without B: (CD)⁺ = {C, D, E, A} (missing B)
    - Without C: (BD)⁺ = {B, D} (incomplete)
    - Without D: (BC)⁺ = {B, C} (incomplete)
5. Therefore, BCD is a candidate key

### Example 2: Normal Form Analysis
For relation R(A, B, C, D) with FDs:
- A → B
- C → D

1. Candidate keys: AC
2. A → B is a non-trivial FD where A is not a superkey
3. Therefore, R is not in BCNF
4. But B is not a prime attribute, and D is not a prime attribute
5. Therefore, R is not in 3NF either
6. Decomposition to achieve BCNF: R₁(A, B) and R₂(A, C, D)

### Example 3: Lossless Join Test
Is the decomposition R(A, B, C, D) → R₁(A, B, C) and R₂(A, D) lossless?

1. R₁ ∩ R₂ = A
2. Check if A → (A, B, C) - A = {B, C}
3. Check if A → (A, D) - A = {D}
4. If either of these FDs holds, the decomposition is lossless
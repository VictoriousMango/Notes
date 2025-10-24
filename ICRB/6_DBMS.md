# DBMS Cheat Sheet for ISRO ICRB CSE & GATE CSE

## Exam Overview
- **GATE Weightage**: 7-8 marks (5-6 questions)
- **Scoring**: High-yield, mostly numerical
- **Study Time**: Less time required, very scoring subject

---

## 1. BASIC CONCEPTS

### Data vs Information
- **Data**: Raw facts and figures about an entity
- **Information**: Processed data with context

### DBMS
- Software to interact with users, applications, and database
- Manages data capture and analysis

### Problems with File System
1. Data redundancy and inconsistency
2. Difficulty accessing data
3. Data isolation
4. Integrity problems
5. Atomicity problems
6. Concurrent access anomalies

### Data Abstraction Levels (Bottom to Top)
1. **Physical Level**: How data is stored in hardware (only DBA operates)
2. **Logical/Conceptual Level**: What data stored, relationships (entity sets, data types)
3. **View Level**: User-specific data views (highest abstraction)

### Schema vs Instance
- **Schema**: Overall design of database
- **Instance**: Data stored at a particular moment

---

## 2. ER MODEL

### Entity Types
- **Tangible**: Physical existence (Car, Pen)
- **Intangible**: Logical existence (Account, Video)
- **Entity Set**: Collection of same type entities
- **Strong Entity**: Has primary key
- **Weak Entity**: No primary key, has discriminator (partial key)
  - Represented by **double rectangle**
  - Always has **total participation** in identifying relationship
  - PK = Owner PK + Discriminator

### Attribute Types
1. **Single-valued** vs **Multi-valued** (double ellipse)
2. **Simple** vs **Composite**
3. **Stored** vs **Derived** (calculated from other attributes)
4. **Descriptive**: Attribute of relationship

### Relationship Degree
- **Unary**: One entity set (self-referential)
- **Binary**: Two entity sets (most common)
- **Ternary**: Three entity sets
- **N-ary**: N entity sets

### Cardinality Ratios
- **1:1** - One-to-One
- **1:N** - One-to-Many
- **N:1** - Many-to-One
- **N:M** - Many-to-Many

### Participation Constraints
- **Partial** (min = 0): Some entities don't participate
- **Total** (min ≥ 1): Every entity participates (double line)

### ER to Relational Conversion Rules

| Relationship Type | Table Creation | Rule |
|-------------------|----------------|------|
| 1:1 Binary | No separate table | PK of one side as FK on other (priority to total participation) |
| 1:N or N:1 Binary | No separate table | PK of 1-side as FK on N-side |
| N:M Binary | Separate table | Combine PKs of both tables as composite PK |
| Ternary/N-ary | Separate table | All PKs combined as composite PK |
| Multi-valued attribute | Separate table | Main table PK as FK + MVA as composite PK |

### Traps in ER Diagrams
- **Fan Trap**: Multiple 1:M relationships from single entity
- **Chasm Trap**: Two entities connected through third entity with partial participation

---

## 3. RELATIONAL MODEL

### Terminology
- **Relation/Table**: Set of tuples
- **Tuple/Row/Record**: Single entry
- **Attribute/Column/Field**: Property
- **Domain**: Set of permissible values
- **Degree/Arity**: Number of columns
- **Cardinality**: Number of rows

### Properties of Relations
1. Cells contain atomic values
2. Values in column are of same kind
3. Each row is unique
4. Each column has unique name
5. Row order insignificant
6. Column order insignificant
7. No two tables with same name

### Anomalies
- **Insertion**: Can't insert without irrelevant data
- **Modification**: Update at multiple locations
- **Deletion**: Unintended loss of information

---

## 4. KEYS

### Key Types
| Key Type | Definition | Formula (if applicable) |
|----------|------------|-------------------------|
| **Super Key** | Set of attributes identifying tuple uniquely | If all n attributes are keys: \(2^n - 1\) |
| **Candidate Key** | Minimal super key (no proper subset) | - |
| **Primary Key** | Selected candidate key (NOT NULL) | At most 1 per table |
| **Alternate Key** | Candidate keys not chosen as primary | - |
| **Foreign Key** | References PK of same/other table | - |
| **Composite Key** | Key with multiple columns | - |
| **Prime Attribute** | Part of any candidate key | - |
| **Non-Prime Attribute** | Not part of any candidate key | - |

---

## 5. FUNCTIONAL DEPENDENCIES (FD)

### Definition
- \(\alpha \to \beta\): For each \(\alpha\) value, precisely one \(\beta\) value exists
- If \(T_1[\alpha] = T_2[\alpha]\) then \(T_1[\beta] = T_2[\beta]\)

### FD Types
- **Trivial FD**: \(\beta \subseteq \alpha\) (always holds)
- **Non-trivial FD**: \(\beta \not\subseteq \alpha\)

### Finding FD from Instance - Quick Check
1. All \(\alpha\) values different → FD valid
2. All \(\beta\) values same → FD valid
3. Find two same \(\alpha\) values with different \(\beta\) → FD invalid

### Attribute Closure (\(X^+\))
- Set of all attributes functionally determined by X
- **If \(K^+ =\) all attributes → K is super key**

### Armstrong's Axioms (Primary Rules)
1. **Reflexivity**: \(Y \subseteq X \Rightarrow X \to Y\)
2. **Augmentation**: \(X \to Y \Rightarrow XZ \to YZ\)
3. **Transitivity**: \(X \to Y, Y \to Z \Rightarrow X \to Z\)

### Secondary Rules
4. **Union**: \(X \to Y, X \to Z \Rightarrow X \to YZ\)
5. **Decomposition**: \(X \to YZ \Rightarrow X \to Y, X \to Z\)
6. **Pseudo-transitivity**: \(X \to Y, WY \to Z \Rightarrow WX \to Z\)
7. **Composition**: \(X \to Y, Z \to W \Rightarrow XZ \to YW\)

### Equivalence of FD Sets
- \(F_1^+ = F_2^+\) OR \(F_1 \subseteq F_2^+\) and \(F_2 \subseteq F_1^+\)

### Minimal Cover (Canonical Cover)
**Steps to find:**
1. Decompose RHS to single attributes
2. Remove extraneous attributes from LHS (check closure of subsets)
3. Remove redundant FDs (check if closure matches without that FD)

---

## 6. NORMALIZATION

### Purpose
- Eliminate redundancy and inconsistent dependencies
- Each table should contain only one idea

### Normal Forms Hierarchy
\[1NF \to 2NF \to 3NF \to BCNF \to 4NF\]

### 1NF (First Normal Form)
- **All attributes must be atomic** (single-valued)
- Requirements:
  - Every row unique
  - Primary key exists
  - Unique column names
  - Order irrelevant

### 2NF (Second Normal Form)
- Must be in 1NF
- **No partial dependency** (non-prime attribute on part of candidate key)
- Partial Dependency: Non-prime depends on proper subset of candidate key

### 3NF (Third Normal Form)
**Method 1:**
- Must be in 2NF
- **No transitive dependency** (non-prime → non-prime)

**Method 2 (Direct Definition):**
- For every FD \(\alpha \to \beta\), either:
  - \(\alpha\) is super key, OR
  - \(\beta\) is prime attribute

### BCNF (Boyce-Codd Normal Form)
- For every FD \(\alpha \to \beta\):
  - **\(\alpha\) must be super key**

### Important Notes on Normal Forms
1. Relation with 2 attributes → always BCNF
2. Only trivial FDs → BCNF
3. Only simple candidate keys → always 2NF
4. Only prime attributes → always 3NF (may not be BCNF)
5. 3NF + only simple candidate keys → BCNF
6. **Every BCNF → 3NF** (but not vice versa)

### 4NF (Fourth Normal Form)
- Must be in BCNF
- **No non-trivial multivalued dependencies** (MVD)
- MVD: \(A \to\to B\) means for each A value, multiple B values exist

---

## 7. DECOMPOSITION

### Lossless Join Decomposition
**Conditions for R → R1, R2:**
1. \(Att(R1) \cup Att(R2) = Att(R)\)
2. \(Att(R1) \cap Att(R2) \neq \Phi\)
3. Common attribute is key for at least one:
   - \(Att(R1) \cap Att(R2) \to R1\) OR
   - \(Att(R1) \cap Att(R2) \to R2\)

### Dependency Preserving Decomposition
- \((F_1 \cup F_2 \cup ... \cup F_n)^+ = F^+\)

### Key Points
- Lossless join: **Must achieve at any cost**
- Dependency preservation: Desirable but sometimes sacrificed
- BCNF may not preserve dependencies
- 3NF always has dependency-preserving decomposition

---

## 8. INDEXING

### File Organization Types
| Type | Search | Insertion/Deletion |
|------|--------|-------------------|
| **Ordered** | Binary search \(O(\log n)\) | Costly (reorganization) |
| **Unordered** | Linear search \(O(n)\) | Easy (usually at end) |

### Index Types
1. **Dense Index**: Entry for every search key value
2. **Sparse Index**: Entry for some records only

### Index Access Formula
- **Number of accesses** = \(\log_2(\text{blocks in index}) + 1\)

### Primary Index
- On ordering key field
- Always sparse (one entry per block)
- **Number of index entries** = Number of blocks in data file

### Clustering Index
- On non-key ordering field
- One entry per distinct value
- **Number of entries** = Number of distinct values

### Secondary Index
- On non-ordering field
- Always dense
- Can be on key or non-key field

---

## 9. B and B+ TREES

### B-Tree Properties
- Order m means:
  - Max m children per node
  - Max (m-1) keys per node
  - Min \(\lceil m/2 \rceil\) children (except root)
  - Min \(\lceil m/2 \rceil - 1\) keys

### B+ Tree Properties
- All data at leaf level
- Internal nodes only for indexing
- Leaves linked sequentially
- More space-efficient than B-tree

### Formulas for B+ Tree (Order p)
- **Max keys in internal node**: p-1
- **Min keys in internal node**: \(\lceil p/2 \rceil - 1\)
- **Max keys in leaf node**: p-1
- **Min keys in leaf node**: \(\lceil (p-1)/2 \rceil\)

---

## 10. RELATIONAL ALGEBRA

### Basic Operations
| Operator | Symbol | Description |
|----------|--------|-------------|
| **Select** | \(\sigma_{\text{condition}}(R)\) | Horizontal filtering (rows) |
| **Project** | \(\Pi_{\text{attributes}}(R)\) | Vertical filtering (columns) |
| **Union** | \(R \cup S\) | All tuples from R or S |
| **Set Difference** | \(R - S\) | Tuples in R but not in S |
| **Cartesian Product** | \(R \times S\) | All combinations |
| **Rename** | \(\rho_{\text{new_name}}(R)\) | Change relation name |

### Derived Operations
| Operator | Symbol | Definition |
|----------|--------|------------|
| **Intersection** | \(R \cap S\) | \(R - (R - S)\) |
| **Natural Join** | \(R \bowtie S\) | Equi-join on common attributes |
| **Theta Join** | \(R \bowtie_{\theta} S\) | \(\sigma_{\theta}(R \times S)\) |
| **Division** | \(R \div S\) | Tuples in R associated with all S tuples |

### Cardinality Formulas
- **Select**: \(0 \leq |\sigma(R)| \leq |R|\)
- **Project**: \(1 \leq |\Pi(R)| \leq |R|\) (duplicates removed)
- **Union**: \(\max(|R|, |S|) \leq |R \cup S| \leq |R| + |S|\)
- **Cartesian Product**: \(|R \times S| = |R| \times |S|\)
- **Natural Join**: \(0 \leq |R \bowtie S| \leq |R| \times |S|\)

---

## 11. SQL BASICS

### Query Structure
```sql
SELECT A1, A2, ..., An
FROM r1, r2, ..., rm
WHERE condition;
```

### Key Points
- SELECT and FROM are mandatory
- WHERE is optional
- Use **DISTINCT** to eliminate duplicates (default is ALL)
- Use **\*** to select all columns

### Aggregate Functions
- **COUNT()**, **SUM()**, **AVG()**, **MIN()**, **MAX()**
- Use with **GROUP BY** for grouping
- **HAVING** clause for group conditions

### Join Types
| Join Type | Description |
|-----------|-------------|
| **INNER JOIN** | Only matching rows |
| **LEFT OUTER JOIN** | All from left + matching from right |
| **RIGHT OUTER JOIN** | All from right + matching from left |
| **FULL OUTER JOIN** | All from both tables |

---

## 12. TRANSACTIONS (ACID Properties)

### ACID
1. **Atomicity**: All or nothing (transaction manager ensures)
2. **Consistency**: Consistency-preserving transformation (programmer ensures)
3. **Isolation**: Concurrent transactions don't interfere
4. **Durability**: Changes persist after commit (recovery manager ensures)

### Transaction States
```
Active → Partially Committed → Committed
    ↓
  Failed → Aborted
```

### Problems in Concurrent Execution
1. **Lost Update** (Write-Write): Second write overwrites first
2. **Dirty Read** (Read-Write): Reading uncommitted data
3. **Unrepeatable Read**: Different values in same transaction
4. **Phantom Read**: New rows appear between reads

---

## 13. SERIALIZABILITY

### Schedule Types
- **Serial Schedule**: Transactions execute one after another (no concurrency)
- **Serializable Schedule**: Equivalent to some serial schedule

### Conflict Serializability
- Two operations **conflict** if:
  1. Belong to different transactions
  2. Access same data item
  3. At least one is write

**Test**: Draw precedence graph
- If **acyclic** → conflict serializable
- If **cyclic** → not conflict serializable

### View Serializability
**Conditions** (S1 view equivalent to S2):
1. Same initial read
2. Same final write
3. Same intermediate reads

**Note**: View serializability ⊇ Conflict serializability

---

## 14. CONCURRENCY CONTROL

### Lock Types
- **Shared Lock (S)**: Read access (multiple allowed)
- **Exclusive Lock (X)**: Write access (exclusive)

### Lock Compatibility Matrix
|   | S | X |
|---|---|---|
| **S** | ✓ | ✗ |
| **X** | ✗ | ✗ |

### Two-Phase Locking (2PL)
**Two Phases:**
1. **Growing Phase**: Acquire locks (no release)
2. **Shrinking Phase**: Release locks (no acquire)

**Types of 2PL:**

| Type | Growing Phase | Shrinking Phase | Properties |
|------|---------------|-----------------|------------|
| **Basic 2PL** | Acquire locks | Release locks | Conflict serializable, deadlock possible |
| **Strict 2PL** | Acquire locks | Release X-locks at commit | Recoverable, cascadeless |
| **Rigorous 2PL** | Acquire locks | Release all locks at commit | Recoverable, cascadeless |
| **Conservative 2PL** | Acquire all at start | Release locks | Deadlock-free |

### Deadlock Handling
**Detection**: Wait-for graph (cycle → deadlock)
**Prevention**:
- **Wait-Die**: Older waits, younger dies
- **Wound-Wait**: Older wounds younger, younger waits

### Timestamp Ordering (TSO)
- Each transaction gets unique timestamp
- **Rules**:
  - **Read(Q)**: If \(TS(T_i) < W\text{-timestamp}(Q)\) → Abort
  - **Write(Q)**: If \(TS(T_i) < R\text{-timestamp}(Q)\) or \(W\text{-timestamp}(Q)\) → Abort

**Properties**:
- Conflict serializable
- Deadlock-free
- May cause starvation
- Not all conflict serializable schedules allowed

### Thomas Write Rule
- Modified TSO
- **Blind writes** can be ignored if obsolete
- May allow view serializable schedules

---

## 15. NUMERICAL FORMULAS CHEAT SHEET

### Index Calculations
1. **Primary Index entries** = \(\lceil r/b \rceil\) where r = records, b = blocking factor
2. **Index block accesses** = \(\lceil \log_2(\text{index blocks}) \rceil + 1\)
3. **Blocking factor** = \(\lfloor \text{Block size} / \text{Record size} \rfloor\)

### B+ Tree
- **Height** = \(\lceil \log_{\lceil p/2 \rceil}(N) \rceil\) where N = number of keys
- **Minimum keys at level i** = \(2 \times (\lceil p/2 \rceil)^{i-1}\)
- **Maximum keys in tree of height h** = \(\frac{p^h - 1}{p - 1} \times (p-1)\)

### Keys Count
- **Total useful FDs for n attributes** = \(3^n - 2^{n+1} + 1\)
- **Super keys when all n attributes are keys** = \(2^n - 1\)

### Schedule Analysis
- **Maximum serial schedules for n transactions** = \(n!\)

---

## 16. QUICK TIPS FOR EXAM

### Normalization Strategy
1. Find all candidate keys first
2. Identify prime and non-prime attributes
3. Check each FD:
   - LHS not super key? → Violates BCNF
   - RHS has non-prime? → Check 3NF
   - Non-prime depends on part of key? → Violates 2NF

### Serializability Testing
1. **Conflict**: Draw precedence graph
   - Node for each transaction
   - Edge if conflicting operations (\(T_i\) before \(T_j\))
   - Cycle? → Not conflict serializable
2. **View**: Check 3 conditions (initial, final, intermediate)

### Common GATE Tricks
- "At most one" means 0 or 1
- "At least one" means 1 or more
- Total participation → minimum cardinality ≥ 1
- Weak entity always has total participation
- BCNF may lose dependency preservation
- 2PL ensures conflict serializability, not freedom from deadlock

---

## 17. IMPORTANT GATE QUESTIONS PATTERN

### High-Frequency Topics
1. **Normalization** (BCNF/3NF identification) - 2 marks
2. **Serializability** (conflict/view) - 2 marks
3. **Functional Dependencies** (closure, keys) - 1-2 marks
4. **ER to Relational** (table count) - 1 mark
5. **Indexing/B+ Trees** - 1-2 marks
6. **Transactions** (schedule conflicts) - 1-2 marks

### Question Types
- **MCQ**: Concept-based (1 mark)
- **MSQ**: Multiple correct answers (2 marks)
- **NAT**: Numerical answer (1-2 marks)

### Time Management
- Normalization: 3-4 minutes
- Serializability: 2-3 minutes
- FD/Keys: 2 minutes
- Conceptual MCQs: 30 seconds

---

## 18. MUST REMEMBER POINTS

✓ Weak entity MUST have total participation in identifying relationship  
✓ BCNF ⊂ 3NF ⊂ 2NF ⊂ 1NF  
✓ Every relation in BCNF is also in 3NF  
✓ Two-attribute relation is always in BCNF  
✓ Lossless join is MANDATORY in decomposition  
✓ 2PL guarantees conflict serializability  
✓ Strict 2PL ensures cascadeless + recoverable schedules  
✓ Timestamp ordering is deadlock-free but may starve  
✓ Primary index is always sparse; secondary can be dense  
✓ Foreign key can be NULL unless specified  
✓ SQL doesn't eliminate duplicates by default (use DISTINCT)  
✓ Natural join matches on ALL common attributes  

---

**END OF CHEAT SHEET**

**Pro Tips for Revision:**
- Practice drawing precedence graphs for serializability
- Memorize Armstrong's axioms and apply them quickly
- Always find candidate keys first in normalization problems
- For numerical problems, write formulas before calculating
- Mark important theorems and properties for quick reference

**All the Best for ISRO ICRB CSE & GATE CSE! 🎯**
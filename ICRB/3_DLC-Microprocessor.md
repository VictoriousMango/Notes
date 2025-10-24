# Digital Logic Circuits & Microprocessors - Exam Ready Cheat Sheet

## EXAM WEIGHTAGE & IMPORTANCE
- **GATE CSE**: 5-8 marks (5-6 questions), Digital Logic gets 5-6% weightage
- **ISRO ICRB CSE**: Part of 80 questions in Core Engineering (Digital Logic + Computer Organization)
- **Nature**: Mostly numerical questions, less time consuming, good scoring

---

# PART 1: DIGITAL LOGIC CIRCUITS (DLC)

## 1. BOOLEAN ALGEBRA FUNDAMENTALS

### 1.1 Basic Laws & Properties

**Idempotent Law:**
- \(a \cdot a = a\)
- \(a + a = a\)

**Associative Law:**
- \(a \cdot (b \cdot c) = (a \cdot b) \cdot c\)
- \(a + (b + c) = (a + b) + c\)

**Commutative Law:**
- \(a \cdot b = b \cdot a\)
- \(a + b = b + a\)

**Distributive Law:**
- \(a \cdot (b + c) = a \cdot b + a \cdot c\)
- \(a + (b \cdot c) = (a + b) \cdot (a + c)\)

**De-Morgan's Law:**
- \((a + b)' = a' \cdot b'\)
- \((a \cdot b)' = a' + b'\)

**Identity Law:**
- \(a + 0 = a\), \(a \cdot 0 = 0\)
- \(a + 1 = 1\), \(a \cdot 1 = a\)

**Complementation Law:**
- \(0' = 1\), \(1' = 0\)
- \(a \cdot a' = 0\), \(a + a' = 1\)

**Involution Law:**
- \((a')' = a\)

**Absorption Law:**
- \(a + ab = a\)
- \(a(a + b) = a\)

**Compensation Theorem:**
- \(ab + a'c + bc = ab + a'c\)
- \((a + b)(a' + c)(b + c) = (a + b)(a' + c)\)
- \(a + a'b = a + b\)
- \(a(a' + b) = ab\)

### 1.2 Logic Gates

| Gate | Symbol | Boolean | Properties |
|------|--------|---------|------------|
| **NOT** | Inverter | \(Y = A'\) | Unary operator |
| **AND** | · | \(Y = A \cdot B\) | Idempotent, Associative, Commutative |
| **OR** | + | \(Y = A + B\) | Idempotent, Associative, Commutative |
| **NAND** | ↑ | \(Y = (A \cdot B)'\) | Universal gate |
| **NOR** | ↓ | \(Y = (A + B)'\) | Universal gate |
| **XOR** | ⊕ | \(Y = A'B + AB'\) | Odd parity detector |
| **XNOR** | ⊙ | \(Y = A'B' + AB\) | Even parity detector |

### 1.3 XOR and XNOR Properties

**XOR Properties:**
- \(a \oplus 0 = a\)
- \(a \oplus 1 = a'\)
- \(a \oplus a = 0\)
- \(a \oplus a' = 1\)
- **Associative & Commutative**
- **Odd number of 1s gives output 1**

**XNOR Properties:**
- \(a \odot 0 = a'\)
- \(a \odot 1 = a\)
- \(a \odot a = 1\)
- \(a \odot a' = 0\)
- **Even number of 0s gives output 1**

**Relationship:**
- \(a \oplus b = (a \odot b)'\) if even number of variables
- For odd variables: XOR and XNOR behave same

### 1.4 Universal Gates (NAND & NOR)

**NAND Implementation:**
- NOT: \((a \cdot a)' = a'\)
- AND: \(((a \cdot b)')' = ab\)
- OR: \((a' \cdot b')' = a + b\)

**NOR Implementation:**
- NOT: \((a + a)' = a'\)
- OR: \(((a + b)')' = a + b\)
- AND: \((a' + b')' = ab\)

---

## 2. BOOLEAN EXPRESSION REPRESENTATION

### 2.1 Sum of Products (SOP) / Minterms

- **Minterm**: Product term with ALL variables (complemented or uncomplemented)
- n variables → 2^n minterms
- **Canonical SOP**: All product terms are minterms
- Notation: \(f = \sum m(1, 3, 5, 7)\)

**Minterm Table (3-variable):**
| Binary | Sequence | Minterm | Designation |
|--------|----------|---------|-------------|
| 000 | 0 | a'b'c' | m₀ |
| 001 | 1 | a'b'c | m₁ |
| 010 | 2 | a'bc' | m₂ |
| 011 | 3 | a'bc | m₃ |
| 100 | 4 | ab'c' | m₄ |
| 101 | 5 | ab'c | m₅ |
| 110 | 6 | abc' | m₆ |
| 111 | 7 | abc | m₇ |

### 2.2 Product of Sums (POS) / Maxterms

- **Maxterm**: Sum term with ALL variables (complemented or uncomplemented)
- n variables → 2^n maxterms
- **Canonical POS**: All sum terms are maxterms
- Notation: \(f = \prod M(0, 2, 4, 6)\)

**Maxterm Table (3-variable):**
| Binary | Sequence | Maxterm | Designation |
|--------|----------|---------|-------------|
| 000 | 0 | a + b + c | M₀ |
| 001 | 1 | a + b + c' | M₁ |
| 010 | 2 | a + b' + c | M₂ |
| 011 | 3 | a + b' + c' | M₃ |
| 100 | 4 | a' + b + c | M₄ |
| 101 | 5 | a' + b + c' | M₅ |
| 110 | 6 | a' + b' + c | M₆ |
| 111 | 7 | a' + b' + c' | M₇ |

### 2.3 Important Concepts

**Complementation:**
- Complement function: Replace variables with complements, 0↔1, AND↔OR
- \(f'(a', b', c', ..., 1, 0, \cdot, +)\)

**Duality:**
- Dual function: 0↔1, AND↔OR, variables remain same
- \(f_D(a, b, c, ..., 1, 0, \cdot, +)\)

**Self-Dual Function:**
- \(f = f_D\)
- Must be neutral (equal minterms and maxterms)
- No mutually exclusive terms in pairs
- For n variables: \(2^{2^{n-1}}\) self-dual functions

**Neutral Function:**
- Equal number of minterms and maxterms
- Required (but not sufficient) for self-dual and orthogonal functions

**Orthogonal Function:**
- \(f' = f_D\)
- Must be neutral
- Minterms and complements both present in pairs
- For n variables: \(^{2^{n-1}}C_{2^{n-2}}\) orthogonal functions

**Number of Boolean Functions:**
- With n variables: \(2^{2^n}\) different functions possible

---

## 3. KARNAUGH MAP (K-MAP) MINIMIZATION

### 3.1 K-Map Basics

**Gray Code Arrangement:**
- Adjacent cells differ by only ONE bit
- 2-variable: 4 cells
- 3-variable: 8 cells  
- 4-variable: 16 cells
- 5-variable: 32 cells (2 K-maps)
- 6-variable: 64 cells (4 K-maps)

### 3.2 Grouping Rules

1. **Every minterm must be covered**
2. **Groups must have contiguous cells** (circular/wrap-around allowed)
3. **Only horizontal or vertical grouping** (no diagonal)
4. **Group size must be power of 2** (1, 2, 4, 8, 16...)
5. **Make largest groups possible** (reduces literals)
6. **Don't cares (X/D)**: Use if helps create larger groups, otherwise ignore
7. **New implicant only if covers new minterm**

### 3.3 Key Terms

**Implicant:**
- Collection of adjacent minterms (any group)

**Prime Implicant (PI):**
- Implicant that is NOT a subset of any other implicant
- Can overlap with other PIs
- Always find ALL PIs first

**Essential Prime Implicant (EPI):**
- PI that covers at least ONE unique minterm no other PI covers
- **MUST be included in minimal expression**

**Minimal Expression:**
- Uses minimum number of literals
- All EPIs + selected non-essential PIs

### 3.4 Minimization Strategy

1. Identify all **don't care conditions**
2. Find all **Prime Implicants**
3. Identify **Essential Prime Implicants**
4. Cover remaining minterms with minimum additional PIs
5. Count: Number of PIs, EPIs, minimal expressions, literals

### 3.5 Variable Independence

- If function independent of variable X: \(f(X=0) = f(X=1)\)
- Check by setting variable to 0 and 1, if same → independent

---

## 4. COMBINATIONAL CIRCUITS

### 4.1 Half Adder

**Inputs:** A, B  
**Outputs:** Sum, Carry

| A | B | Sum | Carry |
|---|---|-----|-------|
| 0 | 0 | 0 | 0 |
| 0 | 1 | 1 | 0 |
| 1 | 0 | 1 | 0 |
| 1 | 1 | 0 | 1 |

**Equations:**
- Sum = \(A \oplus B\)
- Carry = \(A \cdot B\)

**Implementation:** 1 XOR + 1 AND gate

### 4.2 Full Adder

**Inputs:** A, B, Cin  
**Outputs:** Sum, Cout

| A | B | Cin | Sum | Cout |
|---|---|-----|-----|------|
| 0 | 0 | 0 | 0 | 0 |
| 0 | 0 | 1 | 1 | 0 |
| 0 | 1 | 0 | 1 | 0 |
| 0 | 1 | 1 | 0 | 1 |
| 1 | 0 | 0 | 1 | 0 |
| 1 | 0 | 1 | 0 | 1 |
| 1 | 1 | 0 | 0 | 1 |
| 1 | 1 | 1 | 1 | 1 |

**Equations:**
- Sum = \(A \oplus B \oplus C_{in}\)
- Cout = \(AB + BC_{in} + AC_{in}\) = \(AB + C_{in}(A \oplus B)\)

**Implementation:** 2 Half Adders + 1 OR gate

### 4.3 Ripple Carry Adder (n-bit)

**Structure:**
- n Full Adders cascaded
- Carry output of stage i → Carry input of stage i+1

**Delay Analysis:**
- Carry delay per FA = 2 gate delays
- Sum delay per FA = 1 gate delay
- **Total carry delay**: 2n gate delays
- **Total sum delay**: 2n-1 gate delays (bottleneck is carry)

**For 4-bit adder with XOR delay = 2Δ, AND/OR delay = Δ:**
- Total delay = 4 × (2 × 2Δ + Δ) = **4 × 5Δ = 20Δ**

### 4.4 Carry Look-Ahead Adder

**Key Concept:** Generate all carries in parallel

**Generate (Gi) and Propagate (Pi):**
- \(P_i = A_i \oplus B_i\) (carry propagate)
- \(G_i = A_i \cdot B_i\) (carry generate)
- \(S_i = P_i \oplus C_i\)
- \(C_{i+1} = G_i + P_i C_i\)

**Carry Equations:**
- \(C_0 = 0\) (initial carry)
- \(C_1 = G_0 + P_0 C_0\)
- \(C_2 = G_1 + P_1 G_0 + P_1 P_0 C_0\)
- \(C_3 = G_2 + P_2 G_1 + P_2 P_1 G_0 + P_2 P_1 P_0 C_0\)
- \(C_4 = G_3 + G_2 P_3 + G_1 P_2 P_3 + G_0 P_1 P_2 P_3 + C_0 P_0 P_1 P_2 P_3\)

**Implementation:**
- All carries generated through **2-level logic** (AND-OR)
- **Delay = O(log n)** vs O(n) for ripple carry
- For n-bit with fan-in 2: Time = **Θ(log n)**

### 4.5 Multiplexer (MUX)

**Definition:** Selects one of 2^n inputs based on n select lines

**2-to-1 MUX:**
- \(Y = S'I_0 + SI_1\)

**4-to-1 MUX:**
- \(Y = S_1'S_0'I_0 + S_1'S_0 I_1 + S_1 S_0'I_2 + S_1 S_0 I_3\)

**MUX Expansion:**
- Target: n×1 MUX, Given: m×1 MUX
- Number of levels K = ⌈log_m n⌉
- MUX at level i: \(x_i = n/m^{k-i+1}\)
- Maximum capacity with k levels: \(m^k × 1\)

**Boolean Function Implementation:**
- For n-variable function: Use 2^(n-1)×1 MUX + 1 inverter
- Last variable as data inputs, remaining as select lines

**Applications:**
- Data selector
- Parallel to serial conversion
- Boolean function implementation

### 4.6 Demultiplexer (DEMUX)

**Definition:** Routes single input to one of 2^n outputs based on n select lines

**1-to-4 DEMUX:**
| S1 | S0 | O3 | O2 | O1 | O0 |
|----|----|----|----|----|-----|
| 0 | 0 | 0 | 0 | 0 | I |
| 0 | 1 | 0 | 0 | I | 0 |
| 1 | 0 | 0 | I | 0 | 0 |
| 1 | 1 | I | 0 | 0 | 0 |

**Relationship with Decoder:**
- DEMUX = Decoder (if input line used as enable)

### 4.7 Decoder

**Definition:** n inputs → 2^n outputs (generates all minterms)

**2-to-4 Decoder:**
| I1 | I0 | O3 | O2 | O1 | O0 |
|----|----|----|----|----|-----|
| 0 | 0 | 0 | 0 | 0 | 1 |
| 0 | 1 | 0 | 0 | 1 | 0 |
| 1 | 0 | 0 | 1 | 0 | 0 |
| 1 | 1 | 1 | 0 | 0 | 0 |

**Types:**
- **Active High Decoder:** Output = AND gates (direct minterms)
- **Active Low Decoder:** Output = NAND gates (use with NAND at 2nd level)

**Boolean Function Implementation:**
- Express function as SOP
- Use n-to-2^n decoder + OR gates
- OR gate inputs = minterms of function

**Decoder Expansion:**
- Target: m×n, Given: p×q
- Number of levels: K = ⌈m/p⌉
- Decoders at level i: \(x_i = n/q^{k-i+1}\)
- Total decoders needed
- Maximum capacity: \(p^k × q^k\)

**Example:** 6-to-64 from 3-to-8 decoders
- Levels = ⌈6/3⌉ = 2
- Total decoders = 1 + 8 = **9 decoders**

### 4.8 Encoder

**Definition:** 2^n inputs → n outputs (inverse of decoder)

**4-to-2 Encoder:**
| I3 | I2 | I1 | I0 | O1 | O0 |
|----|----|----|----|----|-----|
| 0 | 0 | 0 | 1 | 0 | 0 |
| 0 | 0 | 1 | 0 | 0 | 1 |
| 0 | 1 | 0 | 0 | 1 | 0 |
| 1 | 0 | 0 | 0 | 1 | 1 |

**Equations:**
- \(O_0 = I_1 + I_3\)
- \(O_1 = I_2 + I_3\)

**Priority Encoder:**
- Multiple inputs can be high simultaneously
- Highest priority input determines output
- Example: I3 > I2 > I1 > I0

---

## 5. SEQUENTIAL CIRCUITS

### 5.1 Latches vs Flip-Flops

| Feature | Latch | Flip-Flop |
|---------|-------|-----------|
| **Sensitivity** | Level-sensitive | Edge-sensitive |
| **Triggering** | Transparent when enable HIGH | Triggered on clock edge |
| **Stability** | Less stable | More stable |
| **Speed** | Faster | Slower |

### 5.2 SR Latch (NOR-based)

| S | R | Qn | Qn+1 | State |
|---|---|-------|-------|-------|
| 0 | 0 | 0 | 0 | Hold |
| 0 | 0 | 1 | 1 | Hold |
| 0 | 1 | X | 0 | Reset |
| 1 | 0 | X | 1 | Set |
| 1 | 1 | X | X | **Invalid** |

**SR Flip-Flop (with Clock):**
- Add AND gates with Clock/Enable
- \(Q_{n+1} = S + R'Q_n\) (when \(SR = 0\))

### 5.3 JK Flip-Flop

**Characteristics Table:**
| J | K | Qn | Qn+1 |
|---|---|-----|-------|
| 0 | 0 | 0 | 0 |
| 0 | 0 | 1 | 1 |
| 0 | 1 | X | 0 |
| 1 | 0 | X | 1 |
| 1 | 1 | 0 | 1 |
| 1 | 1 | 1 | 0 |

**Characteristic Equation:**
- \(Q_{n+1} = JQ_n' + K'Q_n\)

**Excitation Table:**
| Qn | Qn+1 | J | K |
|----|-------|---|---|
| 0 | 0 | 0 | d |
| 0 | 1 | 1 | d |
| 1 | 0 | d | 1 |
| 1 | 1 | d | 0 |

**Function Table:**
| J | K | Qn+1 |
|---|---|-------|
| 0 | 0 | Qn (Hold) |
| 0 | 1 | 0 (Reset) |
| 1 | 0 | 1 (Set) |
| 1 | 1 | Qn' (Toggle) |

**Key Feature:** Resolves SR=11 invalid state by toggling

### 5.4 T Flip-Flop (Toggle)

**Characteristics Table:**
| T | Qn | Qn+1 |
|---|-----|-------|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

**Characteristic Equation:**
- \(Q_{n+1} = T \oplus Q_n = TQ_n' + T'Q_n\)

**Excitation Table:**
| Qn | Qn+1 | T |
|----|-------|---|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

**From JK:** Tie J and K together → T flip-flop

### 5.5 D Flip-Flop (Data/Delay)

**Characteristics Table:**
| D | Qn | Qn+1 |
|---|-----|-------|
| 0 | X | 0 |
| 1 | X | 1 |

**Characteristic Equation:**
- \(Q_{n+1} = D\)

**Excitation Table:**
| Qn | Qn+1 | D |
|----|-------|---|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

**Key Feature:** Output tracks input (no ambiguity)

### 5.6 Flip-Flop Conversions

**Steps:**
1. Write **Characteristics Table** of target FF
2. Write **Excitation Table** of given FF
3. Determine excitation values for characteristics table
4. Use K-map to get simplified expressions
5. Draw circuit diagram

**Example: D to T Conversion**
- Characteristics of T: \(Q_{n+1} = T \oplus Q_n\)
- Excitation of D: \(D = Q_{n+1}\)
- Result: \(D = T \oplus Q_n\)

---

## 6. COUNTERS & REGISTERS

### 6.1 Counter Types

**Synchronous Counter:**
- All FFs triggered by same clock simultaneously
- Faster (delay = T_FF + T_CC)
- More complex design
- Can count in any sequence

**Asynchronous/Ripple Counter:**
- FFs triggered sequentially
- Slower (delay = n × T_FF + T_CC)
- Simple design
- Fixed count sequence (UP/DOWN)

**Counter Properties:**
- **Free-running counter**: Maintains all possible states
- **Self-starting counter**: Works from any initial state
- **If free-running → self-starting** (not vice versa)

### 6.2 MOD Counters

**MOD-n counter:** Counts from 0 to n-1, then repeats

**Number of FFs required:**
- For MOD-n: Minimum = ⌈log₂ n⌉ FFs

**Examples:**
- MOD-8: 3 FFs (counts 0-7)
- MOD-10: 4 FFs (counts 0-9, unused: 10-15)
- MOD-258: ⌈log₂ 258⌉ = 9 FFs

### 6.3 Counter Analysis Steps

1. Draw circuit diagram
2. Write characteristic equations for each FF
3. Create present state → next state table
4. Determine counting sequence
5. Check if self-starting/free-running

### 6.4 Counter Design Steps

1. Determine number of FFs needed
2. Create state transition table
3. Write excitation table for chosen FF type
4. Use K-maps to minimize input equations
5. Draw circuit diagram

### 6.5 Shift Registers

**Types by Operation:**

| Type | Input | Output | Clocks (Write) | Clocks (Read) | Total |
|------|-------|--------|----------------|---------------|-------|
| **SISO** | Serial | Serial | n | n-1 | 2n-1 |
| **SIPO** | Serial | Parallel | n | 0 | n |
| **PISO** | Parallel | Serial | 1 | n-1 | n |
| **PIPO** | Parallel | Parallel | 1 | 0 | 1 |

**Applications:**
- Data conversion (serial ↔ parallel)
- Delay elements
- Arithmetic operations (shift left = ×2, shift right = ÷2)

### 6.6 Special Counters

**Ring Counter:**
- Circular shift register
- Only ONE FF set at any time
- n FFs → n states
- Unused states = 2^n - n

**Johnson Counter (Twisted Ring):**
- Complemented output of last FF → first FF
- n FFs → 2n states
- Sequence: 0→1→3→7→15→14→12→8→0 (for 4-bit)

---

## 7. NUMBER SYSTEMS & CODES

### 7.1 Number System Conversions

**Decimal to Binary:**
- Divide by 2, collect remainders (bottom to top)

**Binary to Decimal:**
- Multiply each bit by 2^position, sum all

**Binary to Octal:**
- Group 3 bits from right

**Binary to Hexadecimal:**
- Group 4 bits from right

### 7.2 Signed Number Representations

**Sign-Magnitude:**
- MSB = sign (0=+, 1=-)
- Remaining bits = magnitude
- Range: -(2^(n-1) - 1) to +(2^(n-1) - 1)
- **Problem:** Two representations for zero (+0, -0)

**1's Complement:**
- Positive: Same as binary
- Negative: Complement all bits
- Range: -(2^(n-1) - 1) to +(2^(n-1) - 1)
- **Problem:** Two zeros (00000000, 11111111)

**2's Complement (Most Used):**
- Positive: Same as binary
- Negative: 1's complement + 1
- Range: -2^(n-1) to +(2^(n-1) - 1)
- **Advantage:** Single zero, easy arithmetic
- **Check overflow:** Sign bits of operands same but result different

**4-bit Examples:**
| Decimal | Sign-Mag | 1's Comp | 2's Comp |
|---------|----------|----------|----------|
| +7 | 0111 | 0111 | 0111 |
| +0 | 0000 | 0000 | 0000 |
| -0 | 1000 | 1111 | - |
| -1 | 1001 | 1110 | 1111 |
| -7 | 1111 | 1000 | 1001 |
| -8 | - | - | 1000 |

### 7.3 Binary Codes

**BCD (Binary Coded Decimal):**
- Each decimal digit → 4 bits
- Weighted code (8-4-2-1)
- Valid: 0000 to 1001
- Invalid: 1010 to 1111
- Example: 395₁₀ = 0011 1001 0101 BCD

**Excess-3 Code:**
- BCD + 3
- Self-complementing (9's complement by bit inversion)
- Unweighted code
- Example: 395₁₀ = 0110 1100 1000 XS-3

**Gray Code:**
- Adjacent values differ in only ONE bit
- **Binary to Gray:** \(G_i = B_i \oplus B_{i+1}\)
- **Gray to Binary:** \(B_i = G_i \oplus B_{i+1}\)
- Unweighted, no arithmetic operations
- **Application:** Position encoders, error correction

---

## 8. IMPORTANT FORMULAS & QUICK REFERENCE

### 8.1 Delay Calculations

**Ripple Carry Adder (n-bit):**
- Carry delay = 2n gate delays
- Sum delay = 2n-1 gate delays

**Carry Look-Ahead Adder:**
- Delay = O(log n)

**Ripple Counter (n-bit):**
- Delay = n × T_FF + T_CC

**Synchronous Counter:**
- Delay = T_FF + T_CC

### 8.2 Counting Formulas

**Number of Functions:**
- n variables → 2^(2^n) Boolean functions

**Self-Dual Functions:**
- n variables → 2^(2^(n-1)) functions

**Orthogonal Functions:**
- n variables → C(2^(n-1), 2^(n-2)) functions

**MUX/DEMUX Expansion:**
- Levels = ⌈log_m n⌉
- Total units = Σ(n/m^i) for i=1 to K

### 8.3 Memory Requirements

**n-bit Counter:**
- States = 2^n
- Unused states = 2^n - (counting sequence length)

**Shift Register (n-bit):**
- SISO: 2n-1 clocks total
- SIPO: n clocks
- PISO: n clocks
- PIPO: 1 clock

---

# PART 2: COMPUTER ORGANIZATION & MICROPROCESSORS

## 1. COMPUTER ORGANIZATION BASICS

### 1.1 Von Neumann Architecture

**Components:**
1. **Processing Unit:** ALU + Processor Registers
2. **Control Unit:** Instruction Register + Program Counter
3. **Memory:** Stores data and instructions
4. **External Mass Storage**
5. **Input/Output Mechanisms**

**Key Features:**
- **Stored Program Concept**
- **Sequential Execution**
- **Same memory for data and instructions**

### 1.2 Memory Hierarchy

**Levels (Fastest to Slowest):**
1. **Registers** (CPU)
2. **Cache** (L1, L2, L3)
3. **Main Memory (RAM)**
4. **Secondary Storage** (Hard Disk, SSD)
5. **Tertiary Storage** (Tape, Optical)

**Characteristics:**
- **Access Time:** Registers < Cache < RAM < Disk
- **Capacity:** Registers < Cache < RAM < Disk
- **Cost per bit:** Registers > Cache > RAM > Disk

### 1.3 Instruction Cycle

1. **Fetch:** Retrieve instruction from memory
2. **Decode:** Interpret instruction
3. **Execute:** Perform operation
4. **Store:** Write result back

---

## 2. MICROPROCESSOR FUNDAMENTALS

### 2.1 Addressing Modes

**1. Immediate Addressing:**
- Operand is part of instruction
- Example: `MVI A, 50H` (Move immediate 50H to A)
- **Fast, but limited data size**

**2. Direct Addressing:**
- Address of operand given in instruction
- Example: `LDA 2050H` (Load A from address 2050H)
- **Simple, fixed address**

**3. Register Addressing:**
- Operand in register
- Example: `MOV A, B` (Move B to A)
- **Fastest, limited registers**

**4. Register Indirect Addressing:**
- Register contains address of operand
- Example: `MOV A, M` (M = memory location pointed by HL)
- **Flexible, one level indirection**

**5. Indexed Addressing:**
- Effective Address = Base + Index
- **Used for array access**

**6. Relative Addressing:**
- Effective Address = PC + Offset
- **Used in branching instructions**

### 2.2 Instruction Types

**Data Transfer:**
- MOV, MVI, LDA, STA, XCHG, PUSH, POP

**Arithmetic:**
- ADD, ADI, SUB, SUI, INR, DCR, DAD

**Logical:**
- ANA, ANI, ORA, ORI, XRA, XRI, CMP

**Branch:**
- JMP, JC, JNC, JZ, JNZ, CALL, RET

**Control:**
- NOP, HLT, DI, EI

### 2.3 Flags (Status Register)

**8085 Flags:**
| Flag | Bit | Condition |
|------|-----|-----------|
| **S** (Sign) | D7 | Result MSB = 1 (negative) |
| **Z** (Zero) | D6 | Result = 0 |
| **AC** (Aux Carry) | D4 | Carry from bit 3 to 4 |
| **P** (Parity) | D2 | Even parity = 1 |
| **CY** (Carry) | D0 | Carry from MSB |

---

## 3. PIPELINING

### 3.1 Pipeline Basics

**Stages (5-stage):**
1. **IF:** Instruction Fetch
2. **ID:** Instruction Decode
3. **EX:** Execute
4. **MEM:** Memory Access
5. **WB:** Write Back

**Benefits:**
- Increased throughput
- Better CPU utilization

**Speedup:**
- Ideal Speedup = Number of stages
- Actual Speedup = (Time without pipeline) / (Time with pipeline)

### 3.2 Pipeline Hazards

**1. Structural Hazards:**
- Hardware resource conflict
- **Solution:** Add more hardware, stall pipeline

**2. Data Hazards:**
- RAW (Read After Write)
- WAR (Write After Read)
- WAW (Write After Write)
- **Solutions:** Forwarding, Stalling, Reordering

**3. Control Hazards:**
- Branch instructions
- **Solutions:** Branch prediction, Delayed branching

---

## 4. CACHE MEMORY

### 4.1 Cache Mapping

**1. Direct Mapping:**
- Block address mod Number of cache lines
- **Simple, fast, high conflict misses**

**2. Fully Associative:**
- Block can go anywhere
- **Flexible, slow search, expensive**

**3. Set-Associative:**
- n-way: Each set has n blocks
- Block maps to set, then any line in set
- **Balance between direct and fully associative**

### 4.2 Cache Replacement Policies

- **LRU** (Least Recently Used)
- **FIFO** (First In First Out)
- **LFU** (Least Frequently Used)
- **Random**

### 4.3 Write Policies

**Write Hit:**
- **Write-Through:** Update cache and memory
- **Write-Back:** Update cache, write to memory later (dirty bit)

**Write Miss:**
- **Write Allocate:** Load block to cache, then write
- **No Write Allocate:** Write directly to memory

---

## 5. I/O ORGANIZATION

### 5.1 I/O Methods

**1. Programmed I/O:**
- CPU polls device status
- **Simple, wastes CPU time**

**2. Interrupt-Driven I/O:**
- Device interrupts CPU when ready
- **Better CPU utilization**

**3. DMA (Direct Memory Access):**
- Device transfers data directly to/from memory
- **CPU only involved at start/end**
- **Most efficient for bulk transfers**

### 5.2 Interrupt Handling

**Steps:**
1. Complete current instruction
2. Save PC and flags
3. Disable interrupts
4. Jump to ISR (Interrupt Service Routine)
5. Execute ISR
6. Restore context
7. Enable interrupts
8. Return to interrupted program

---

## 6. EXAM-SPECIFIC TIPS

### 6.1 GATE CSE Focus Areas

**High Weightage:**
1. K-Map minimization (2-3 marks)
2. Sequential circuit analysis (2-3 marks)
3. Counter design (2 marks)
4. Adder circuits (1-2 marks)
5. MUX/DEMUX implementation (1-2 marks)

**Problem Types:**
- **Numerical:** K-map, delay calculations
- **Circuit Analysis:** Given circuit → find sequence/output
- **Design:** Given specification → design circuit

### 6.2 ISRO ICRB Focus Areas

**Important Topics:**
1. Boolean algebra simplification
2. Logic gate implementation
3. Flip-flop conversions
4. Counter sequences
5. Number system conversions
6. Basic computer organization

**Exam Strategy:**
- Focus on fundamentals
- Practice numerical problems
- Memorize standard circuits
- Time management (2 marks in ~2 minutes)

### 6.3 Common Mistakes to Avoid

1. **K-Map:** Missing prime implicants, wrong grouping
2. **Flip-Flops:** Confusing excitation vs characteristic tables
3. **Counters:** Not checking self-starting property
4. **Number Systems:** Sign extension errors in 2's complement
5. **Timing:** Not considering propagation delays

### 6.4 Quick Revision Checklist

**Before Exam:**
- [ ] Boolean laws (all 10)
- [ ] XOR/XNOR properties
- [ ] K-map grouping rules
- [ ] All flip-flop tables (4 types)
- [ ] Counter types and delays
- [ ] Number system conversions
- [ ] Addressing modes (6 types)
- [ ] Pipeline hazards (3 types)
- [ ] Cache mapping techniques
- [ ] Standard gate counts (Half Adder, Full Adder)

---

## 7. PRACTICE PROBLEM PATTERNS

### 7.1 K-Map Problems

**Type 1:** Given function, find minimal SOP/POS
- Draw K-map
- Identify all PIs and EPIs
- Form minimal expression

**Type 2:** Given don't cares, find number of minimal expressions
- Multiple ways to cover optional minterms
- Count all valid combinations

**Type 3:** Function independence
- Set variable to 0 and 1
- If results same → independent

### 7.2 Sequential Circuit Problems

**Type 1:** Given circuit, find counting sequence
- Write equations for each FF
- Create state table
- Trace through states

**Type 2:** Design counter for given sequence
- Choose FF type
- Write excitation table
- Use K-map for input equations

**Type 3:** Analyze registers
- Identify type (SISO/SIPO/PISO/PIPO)
- Calculate clock cycles needed

### 7.3 Arithmetic Circuit Problems

**Type 1:** Delay calculation
- Count gate delays in critical path
- Consider carry propagation

**Type 2:** Overflow detection
- Check sign bits in 2's complement
- Same operand signs, different result sign → overflow

**Type 3:** Adder/Subtractor operation
- 2's complement for subtraction
- End-around carry handling

---

## APPENDIX: KEY FORMULAS SUMMARY

1. **Boolean Functions:** \(2^{2^n}\) with n variables
2. **Self-Dual Functions:** \(2^{2^{n-1}}\) with n variables
3. **Ripple Adder Delay:** 2n (carry), 2n-1 (sum)
4. **CLA Delay:** O(log n)
5. **MOD-n Counter FFs:** ⌈log₂ n⌉
6. **Ring Counter States:** n (with n FFs)
7. **Johnson Counter States:** 2n (with n FFs)
8. **MUX Expansion Levels:** ⌈log_m n⌉
9. **2's Complement Range:** -2^(n-1) to 2^(n-1)-1
10. **Pipeline Speedup:** Ideal = k stages

---

**EXAM READY - ALL THE BEST! 🎯**
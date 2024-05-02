

### Decidability 
- If there exists a TM that decides A, then there exists a DFA that recognizes A. **[False]**
- If A is decidable, then $\overline{A}$ is decidable.**[True]**
- If A is Turing-recognizable, then $\overline{A}$ is Turing-recognizable. **[False]**
- For any language A, A $ ≤_m \overline{A}$. **[False]**
- If A is decidable and B ⊆ A, then B is decidable. **[False]**
- If A is decidable, then A* is decidable. **[True]**
- 

### Complexity



- If A is NP-hard, A must be in PSPACE. [False]
  - The halting problem is NP-hard, but not PSPACE -- it's undecidable 
- If A is NP-complete, A must be in PSPACE. [True]

- P ⊆ (NP ∩ co-NP) [True]










---

### Closure Properties of Languages

#### Regular Languages closed under
- **Union ∪, Intersecion ∩** (De Morgan's Law)
- concatenation, star, and complementation.
-  

#### CFL is closed under:
Let the start variables for L1 and L2 be S1 and S2 respectively. 
- **Union**
  - CFG for L1 ∪ L2: S → S1|S2
- **concatenation** 
  - CFG for L1 ∪ L2: S → S1S2
- **star***
  - CFG for L1*: S → S1S|ε
- NOT intersection 

#### Decidable languages
- **Union ∪, Intersecion ∩**
  - **Desider for L1 ∪ L2**: on input x, run M1 and M2 on x, and accept iff either accepts. (accept iff both accepts for intersection)
- **complementation**
  - Desider for complement L1: On input x, run M1 on x, and accept if M1 rejects, and reject if M1 accepts.
- **concatenation**
  - Desider for L1L2: On input x, for each of the |x|+1 ways to divide x as yz: run M1 on y and M2 on z, and accept if both accept. Else reject.
- **Kleene star \***
  - Desider for L1*: 
  - On input x, if x = ε accept. Else, for each of the 2|x|−1 ways to divide x into w1 . . . wk (wi ≠ ε): run M1 on each wi and accept if M1 accepts all. Else reject.
  - 

#### Turing-Recognizable Languages are closed under:
- **Union ∪, Intersecion ∩**
  - Recognizer for **L1 ∪ L2**: 
  - On input x, run M1 and M2 on x, and accept iff either accepts. (accept if both accept for intersection.)
- **concatenation** 
  - Recognizaer for L1L2:
  - On input x, for each of the |x|+1 ways to divide x into x1x2: run M1 on x1 and M2 on x2, and accept if both accept.
- **star\***
  - Recognizaer for **L1\***: On input x, if x = ε accept. Else, for each of the 2|x|−1 ways to divide x as w1 . . . wk (wi ̸= ε): run M1 on each wi, accept if M1 accepts all wi
- NOT complementation (if the complement is recognizable as well it'd be decidable)

#### P is closed under
- **Union ∪, Intersecion ∩**
- **complement**
- **concatenation**, **star**


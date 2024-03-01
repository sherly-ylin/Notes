### Content
- [1. Regular Languages, DFA, NFA](#1-regular-languages-dfa-nfa)
- [2. Context-Free Languages, PDA](#2-context-free-languages-pda)
- [3. Turing Machine](#3-turing-machine)
  - [Ch. 1-3 Summary](#ch-1-3-summary)
- [4. Decidability](#4-decidability)
    - [Theorems](#theorems)

## 1. Regular Languages, DFA, NFA


## 2. Context-Free Languages, PDA


## 3. Turing Machine


### Ch. 1-3 Summary 
$DFA \subset NFA$

**Conversion**
DFA <-> NFA
DFA -> CFG
NFA -> PDA
DFA -> PDA (NFA -> DFA -> PDA)

Reg exp -> CFG
Reg exp -> NFA

$[regular] \subset [context-free]\subset [decidable]\subset [Turing-recognizable]$

## 4. Decidability 
Def: A language $A$ is decidable if $\exist$ a TM $M$ s.t. $\forall$ string x,
- $x \in A$ => $M$ accepts $x$
- $x \notin A$ => $M$ rejects $x$ 

> **Showing that the language is decidable is the same as showing that the computational problem is decidable**


#### Theorems
The following languages are all decidable
- All regular languages
  - Whether a string is in a regular language
- All context-free languages
- $A_{DFA}$ = { $⟨B, w⟩$ | $B$ is a DFA that accepts input string $w$}
- $E_{DFA}$ = { $⟨A⟩$ | $A$ is a DFA and $L(A) = \empty$ }
- $A_{CFG}$ = { $⟨G, w⟩$ | $G$ is a CFG that generates $w$}
- $EQ_{DFA}$ = { $⟨A,B⟩$ | $A, B$ are DFAs and $L(A)=L(B)$} 

    - whether A and B recognize the same language
    - Deciding $EQ_{DFA}$ is ***reducible*** to deciding $E_{DFA}$:

      - Symmetic difference of L(A) and L(B)
      - $L(C) = (L(A)\cap \overline{L(B)}) \cup (L(B)\cap \overline{L(A)})$
      - $L(C) =\empty $ if L(A) = L(B) 


$EQ_{CFG}$ = { $⟨G,H⟩$ | $G, H$ are CFGs and $L(G)=L(H)$} 
  
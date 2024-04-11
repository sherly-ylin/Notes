### Content
- [1. Regular Languages, DFA, NFA](#1-regular-languages-dfa-nfa)
    - [DFA](#dfa)
    - [NFA](#nfa)
    - [Regular Language](#regular-language)
    - [Regular Expressions](#regular-expressions)
    - [Nonregular Language](#nonregular-language)
      - [Pumping Lemma](#pumping-lemma)
- [2. Context-Free Languages, CFG, PDA](#2-context-free-languages-cfg-pda)
    - [PDA](#pda)
    - [Context-Free Grammar (CFG)](#context-free-grammar-cfg)
      - [Pumping Lemma for CFL](#pumping-lemma-for-cfl)
- [3. Turing Machine](#3-turing-machine)
    - [Variants of TMs](#variants-of-tms)
  - [Ch. 1-3 Summary](#ch-1-3-summary)
    - [Closure of Languages](#closure-of-languages)
- [4. Decidability](#4-decidability)
  - [Decidable Languages](#decidable-languages)
  - [Undecidable Languages](#undecidable-languages)
- [5. Reducibility](#5-reducibility)

## 1. Regular Languages, DFA, NFA

#### DFA 
- 5-tuple ($Q, \Sigma, \delta, q_0, F$):
  - states 
  - input alphabet
  - transition functions $\delta: Q \times \Sigma \rightarrow Q$
  - start state
  - accept states

#### NFA 
- = DFA 5-tuple ($Q, \Sigma, \delta, q_0, F$) but
- $\delta: Q \times \Sigma_{\epsilon} \rightarrow P(Q)$
- $\epsilon$ can be a symbol 
- can have multiple arrow leaving a states with save input
- each arrow creates a copy, accept if at least 1 copy ends up in accept state

**DFA $\leftrightarrow$ NFA**
Every DFA is an NFA
EVery NFA can be converted into equivalent DFA

#### Regular Language 
> **A language is regular $\iff$ a DFA recognizes it $\iff$ a regexp  describes it**

#### Regular Expressions

- $a, a\in \Sigma$
- Null string $\epsilon$
- Empty set $\emptyset$
- If $r_1$ and $r_2$ are regexp, so are:
  - $r_1r_2$ (concatenation)
  - $r_1 \cup r_2$
  - $r_1r_2$ (anything in $r_1$ concat w/ anything in $r_2$)
  - $r_1^*$, $r_2^*$ (Kleene closure, any number of things in $r_2$ concat together)

$\downarrow$ Order of operations: 
- $*$ star
- concatenation ($\circ$ often omit)
- $\cup$ union

Regular expressions describes regular languages

#### Nonregular Language

$\{0^n 1^n|n≥0\}$ is not regular

##### Pumping Lemma
If $A$ is regular $\implies \exists$ $p$ s.t. $\forall s\in A$, $s$ can be split into 3 parts $s=xyz$ 
&emsp;&emsp; s.t&nbsp; 1) $\forall i ≥0, xy^iz \in A$
&emsp;&emsp;&emsp;&emsp; 2) $|y|>0$
&emsp;&emsp;&emsp;&emsp; 3) $|xy|≤p$


## 2. Context-Free Languages, CFG, PDA
**All DFA can be converted into equivalent CFG**
$(DFA\rightarrow CFG)$
$(regexp\rightarrow CFG)$
$(NFA\rightarrow PDA)$: "Do whatever the NFA does, ignore the stack"


#### PDA
- NFA with a stack
- 6-tuple $(Q,\Sigma,\Gamma$(stack alphabet)$, \delta, q_0, F)$
- $\delta: Q \times \Sigma \times \Gamma \rightarrow Q \times \Gamma$
- $\delta(q_0, 1, a)=(q_1, b)$ 
  - ≈ "currenly in $q_0$, if read input 1, go to state $q_1$, replace the 'a' on top of stack with a 'b' " 
  - (s$q_0\rightarrow q_1$ arrow: "1, a$\rightarrow$b")
- Accept if input & stack both empty + in accept states

#### Context-Free Grammar (CFG)
$(V, \Sigma, R, S)$ = (variables, terminals, rules, start variable)

> **Context-Free Languages (CFLs)**
> **A language is context-free $\iff$ a CFG generates it $\iff$ a PDA recognizes it**

$\{a^n b^n c^n|n≥0\}$ is not context-free
##### Pumping Lemma for CFL
If $A$ is CFL $\implies \exists$ $p$ s.t. $\forall s\in A$, $s$ can be split into 5 parts $s=uvxyz$ 
&emsp;&emsp; s.t&nbsp; 1) $\forall i ≥0, uv^ixy^iz \in A$
&emsp;&emsp;&emsp;&emsp; 2) $|vy|>0$
&emsp;&emsp;&emsp;&emsp; 3) $|vxy|≤p$


## 3. Turing Machine


#### Variants of TMs 

- Multitape TM
- Nondeterministic TM

All reasonable variants of TMs are **equivalent**


### Ch. 1-3 Summary 
DFA $\subset$ NFA
Every regular language is context-free


**Conversion**
DFA $\leftrightarrow$ NFA
DFA $\rightarrow$ CFG
NFA $\rightarrow$ PDA
DFA $\rightarrow$ PDA (NFA $\rightarrow$ DFA $\rightarrow$ PDA)

Regexp $\rightarrow$ CFG
Regexp $\rightarrow$ NFA

$[\text{regular}] \subset [\text{context-free}]\subset [\text{decidable}]\subset [\text{Turing-recognizable}]$

#### Closure of Languages
<table>
<tr>
<td>

Regular Languages are closed under:
- union, intersection (De Morgan's Law)
-  concatenation, star, and complementation.
- 
</td>
</tr>
<tr>
<td>

**CFL** is closed under:
- Union, concatenation and star*
</td>

<td>

- ∀L1,L2∈CFL, **L1∪L2 ∈ CFL**
Let the start variables for L1 and L2 be S1 and S2 respectively
CFG for L1∪L2: **S → S1|S2**
- ∀L1, L2 ∈ CFL, **L1L2 = {w1w2 : w1 ∈ L1 ∧ w2 ∈ L2} ∈ CFL**
CFG for L1∪L2: **S → S1S2**
- ∀L1 ∈ CFL, **L1*∈CFL**
CFG for L1*: **S → S1S|ε**
</td>

</tr>
<tr>
<td>

**Decidable Languages** are closed under:

- Union ∪, Intersecion ∩ 
- complementation
- concatenation °
- star*,
</td>
<td>

• Desider for **L1 ∪ L2**: 
On input x, run M1 and M2 on x, and accept iff either accepts, rejects if both rejects. (Similarly for intersection.)
• Desider for **L1**: 
On input x, run M1 on x, and accept if M1 rejects, and reject if M1 accepts.
• Desider for **L1L2:** 
On input x, for each of the |x|+1 ways to divide x as yz: run M1 on y and M2 on z, and accept if both accept. Else reject.
• Desider for **L*1**: On input x, if x = ε accept. Else, for each of the 2|x|−1 ways to divide x as w1 . . . wk (wi ̸= ε): run M1 on each wi and accept if M1 accepts all. Else reject.

</td>
</tr>

<tr>
<td>

**Turing-Recognizable Languages** are closed under:
- Union ∪, Intersecion ∩ 
- concatenation °, star*
- NOT complementation
</td>
<td>

• Recognizer for **L1 ∪ L2**: 
On input x, run M1 and M2 on x, and accept iff either accepts. (Similarly for intersection.)
• Desider for **L1**: 
On input x, run M1 on x, and accept i$$f M1 rejects, and reject if M1 accepts.
• Desider for **L1L2:** 
On input x, for each of the |x|+1 ways to divide x as yz: run M1 on y and M2 on z, and accept if both accept. Else reject.
• Desider for **L*1**: On input x, if x = ε accept. Else, for each of the 2|x|−1 ways to divide x as w1 . . . wk (wi ̸= ε): run M1 on each wi and accept if M1 accepts all. Else reject.

</td>
</tr>
</table>


## 4. Decidability 
Def: A language $A$ is decidable if $\exist$ a TM $M$ s.t. $\forall$ string x,
- $x \in A$ => $M$ accepts $x$
- $x \notin A$ => $M$ rejects $x$ 

Def: a decider is a Tusring machine that halts for every input 
> **Showing that the language is decidable is the same as showing that the computational problem is decidable**


### Decidable Languages
The following languages are all decidable:
<table>
<tr>
<td>

**All regular languages**
(Decides whether a string is in a regular language)

</td>
<td>

Let $A$ be a regular language, then there exits a DFA D that recignizes it. Let $M$ be decider for $A_{DFA}$.
Construct a decider $S$ for A:
```
given input w, 
run D on w: 
  if D accepts w: accepts w;
  else (D rejects w): rejects w;
```

</td>
</tr>

<tr>
<td>

**All context-free languages**
(Decides whether a string is in a context-free language)

</td>
</tr>

<tr>
<td>

$A_{DFA}$
= $\{⟨B, w⟩$ | $B$ is a DFA that accepts input string $w\}$
(Whether a DFA accepts a specific string)

</td>
</tr>

<tr>
<td>

$E_{DFA}$
= $\{⟨A⟩$ | $A$ is a DFA and $L(A) = \empty\}$
(Whether a DFA accepts nothing)

</td>
</tr> 

<tr>
<td>

$A_{CFG}$
= $\{ ⟨G, w⟩ | G \text{ is a CFG that generates } w\}$
(Whether a CFG generates a string)

</td>
</tr>

<tr>
<td>

$EQ_{DFA}$ 
= $\{⟨A,B⟩ | A, B \text{ are DFAs and } L(A)=L(B)\}$
(Whether two DFAs recognize the same language)

</td>
<td>

Deciding $EQ_{DFA}$ is ***reducible*** to deciding $E_{DFA}$:
  - Symmetic difference of L(A) and L(B)
  - $L(C) = (L(A)\cap \overline{L(B)}) \cup (L(B)\cap \overline{L(A)})$
  - $L(C) =\empty $ if L(A) = L(B) 
  
</td>
</tr>

<tr>
<td>

$EQ_{CFG}$ 
= $\{⟨G,H⟩ | G, H\text{ are CFGs and } L(G)=L(H)\}$ 
(Whether 2 CFGs generates the same language)

</td>
</tr>
</table>
### Undecidable Languages

$A_{TM}$ - Turing-recognizable
$\overline{A_{TM}}$ - **not** Turing-recognizable
$HALT_{TM}$ - Turing-recognizable
$E_{TM}$ - **not** Turing-recognizable
$\overline{E_{TM}}$ - Turing-recognizable

$EQ_{TM}$ - **not** Turing-recognizable





**Theorem: A language A is decidable $\iff$ A and its complement $\overline{A}$ are both Turing-recognizable (co-Turing-recognizable).**

## 5. Reducibility 
$A≤_mB \iff \overline{A}≤_m\overline{B}$ 
$A≤_mB \implies A≤B$ 

<table>
<tr>
<td>"General" Reducibility 

$A≤B$ </td>
<td>Mapping Reducibility 

$A≤_m B$ </td>
</tr>

<tr>
<td>

- A is **reducible** to B
- Given a decider for B, we can create a decider for A
- A undecidable => B undecidable
  
</td>

<td>

-  A is **mapping-reducible** to B

-  $\exists$ a computible function $f$ s.t. $\forall$ string $w$,

-  $w\in A \iff f(w) \in B$
-  A undecidable => B undecidable
-  A not Turing-recognizable => B not Turing-recognizable

</td>
</tr>

<tr>
<td>

- $A_{TM} ≤ HALT_{TM}$
- $A_{TM} ≤ E_{TM}$
- $E_{TM} ≤ EQ_{TM}$

</td>

<td>

- $E_{TM} ≤_m EQ_{TM}$
- $A_{TM} ≤_m HALT_{TM}$
- $A_{TM} ≤_m \overline{E_{TM}}$
  

</td>
</tr>
</table>

To show $A≤_mB$: 
show the contrapositive of [*A undecidable => B undecidable*]
i.e. **[ *b decidable => A decidable* ]**



DFA = NFA < DPDA < PDA < DTM



---

**Some T/F Questions**
- If there exists a TM that decides A, then there exists a DFA that recognizes A. ***(False)***

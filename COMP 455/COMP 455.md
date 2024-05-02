### Content
- [1. Regular Languages, DFA, NFA](#1-regular-languages-dfa-nfa)
    - [Regular Language \& Regular Expressions](#regular-language--regular-expressions)
    - [Nonregular Language](#nonregular-language)
    - [Pumping Lemma](#pumping-lemma)
- [2. Context-Free Languages, CFG, PDA](#2-context-free-languages-cfg-pda)
    - [PDA](#pda)
    - [Context-Free Grammar (CFG)](#context-free-grammar-cfg)
      - [Pumping Lemma for CFL](#pumping-lemma-for-cfl)
- [3. Turing Machine](#3-turing-machine)
    - [Variants of TMs](#variants-of-tms)
  - [Ch. 1-3 Summary](#ch-1-3-summary)
- [4. Decidability](#4-decidability)
  - [Decidable Languages](#decidable-languages)
      - [All regular languages](#all-regular-languages)
    - [All context-free languages](#all-context-free-languages)
    - [TMs](#tms)
  - [Undecidable Languages](#undecidable-languages)
- [5. Reducibility](#5-reducibility)
    - ["General" Reducibility $A≤B$](#general-reducibility-ab)
    - [Mapping Reducibility $A≤\_m B$](#mapping-reducibility-a_m-b)
- [7. Time Complexity](#7-time-complexity)
    - [Thms \& Corollary](#thms--corollary)
  - [Class P, NP](#class-p-np)
- [8 Space Complexity](#8-space-complexity)
      - [Savitch's Thm](#savitchs-thm)
      - [TQBF is PSPACE-complete](#tqbf-is-pspace-complete)

## 1. Regular Languages, DFA, NFA

**DFA** 
- 5-tuple ($Q, \Sigma, \delta, q_0, F$):
  - states 
  - input alphabet
  - transition functions $\delta: Q \times \Sigma \rightarrow Q$
  - start state
  - accept states
- for a DFA M, L(M) is regular language
**NFA**
- = DFA 5-tuple ($Q, \Sigma, \delta, q_0, F$) but
- $\delta: Q \times \Sigma_{\epsilon} \rightarrow P(Q)$
- $\epsilon$ can be a symbol 
- can have multiple arrow leaving a states with save input
- each arrow creates a copy, accept if at least 1 copy ends up in accept state

**DFA $\leftrightarrow$ NFA**
Every DFA is an NFA
EVery NFA can be converted into equivalent DFA

#### Regular Language & Regular Expressions
> **A language is regular $\iff$ a DFA recognizes it $\iff$ a regexp  describes it**

**Regular Expressions**
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


Tips: 
- regular languages are finite sets 
- when there's no pattern - nonregular
  - { $a^p$ | p is prime. } is not regular. 
- concatenation of pattern(regular) and a non-pattern(not regular) is not regular
- whenever we need to store unbounded count - nonregular
  - $\{0^n 1^n|n≥0\}$ is nonregular
  - ab*a
- Patterns of $W$, $W^r$ and $x$ , $y$

#### Pumping Lemma
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
  - ($q_0\rightarrow q_1$ arrow: "1, a$\rightarrow$b")
  - "currenly in $q_0$, if read input 1, go to state $q_1$, replace the 'a' on top of stack with a 'b' " 
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
- = DFA with infinite tape
- 7-tuple $(Q,\Sigma,\Gamma$(tape alphabet)$, \delta, q_0, q_{accept}, q_{reject})$
- $\delta: Q \times \Gamma \rightarrow Q \times \Gamma \times \lbrace{L,R}\rbrace$
- $\delta(q_0, a)=(q_1, b, R)$ 
- arrow from q0 --> q1 : (a -> b, R)
- read a on tape, write b over a, move tape head right (don't write if no b)
- for all TMs, running M on input w will either: accept, reject, or loop.
  
#### Variants of TMs 

- Multitape TM
- Nondeterministic TM

All reasonable variants of TMs are **equivalent**, just different runtime


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



## 4. Decidability 
Def: A language $A$ is decidable if $\exist$ a TM $M$ s.t. $\forall$ string x,
- $x \in A$ => $M$ accepts $x$
- $x \notin A$ => $M$ rejects $x$ 

Def: a decider is a Turing machine that halts for every input 
> **Showing that the language is decidable is the same as showing that the computational problem is decidable**


### Decidable Languages
The following languages are all decidable:

##### All regular languages
- (Decides whether a string is in a regular language)
- Show $A_{DFA} ≤ A$:
- Let $A$ be a regular language, then there exits a DFA D that recignizes it. Let $M$ be decider for $A_{DFA}$.
- Construct a decider $S$ for A:
```
given input w, 
run D on w: 
  if D accepts w: accepts w;
  else (D rejects w): rejects w;
```

#### All context-free languages
(Decides whether a string is in a context-free language)

#### TMs
- $A_{DFA}$, $E_{DFA}$, $EQ_{DFA}$
- $A_{CFG}$, $EQ_{CFG}$

$A_{DFA}$ = $\{⟨B, w⟩$ | $B$ is a DFA that accepts input string $w\}$
(Whether a DFA accepts a specific string)

$E_{DFA}$ = $\{⟨A⟩$ | $A$ is a DFA and $L(A) = \empty\}$

$A_{CFG}$ = $\{ ⟨G, w⟩ | G \text{ is a CFG that generates } w\}$
(Whether a CFG generates a string)


$EQ_{DFA}$ = $\{⟨A,B⟩ | A, B \text{ are DFAs and } L(A)=L(B)\}$
(Whether two DFAs recognize the same language)
- Deciding $EQ_{DFA}$ is ***reducible*** to deciding $E_{DFA}$:
  - Symmetic difference of L(A) and L(B)
  - $L(C) = (L(A)\cap \overline{L(B)}) \cup (L(B)\cap \overline{L(A)})$
  - $L(C) =\empty $ if L(A) = L(B) 
  

$EQ_{CFG}$ = $\{⟨G,H⟩ | G, H\text{ are CFGs and } L(G)=L(H)\}$ 
(Whether 2 CFGs generates the same language)


### Undecidable Languages

Turing-recognizable
- $A_{TM}$
- $HALT_{TM}$ 
- $\overline{E_{TM}}$ 

Not Turing-recognizable
- $\overline{A_{TM}}$
- $E_{TM}$
- $EQ_{TM}$ 




**Thm: A language A is decidable $\iff$ $A$ and $\overline{A}$ are both Turing-recognizable (co-Turing-recognizable).**

## 5. Reducibility 
$A≤_mB \iff \overline{A}≤_m\overline{B}$ 
$A≤_mB \implies A≤B$ 

#### "General" Reducibility $A≤B$
- A is **reducible** to B
- Given a decider for B, we can create a decider for A
- A undecidable => B undecidable

In class:
- $A_{TM} ≤ HALT_{TM}$
- $A_{TM} ≤ E_{TM}$
- $E_{TM} ≤ EQ_{TM}$

#### Mapping Reducibility $A≤_m B$
-  A is **mapping-reducible** to B
-  $\exists$ a computible function $f$ s.t. $\forall$ string $w$, $w\in A \iff f(w) \in B$
-  A undecidable => B undecidable
-  A not Turing-recognizable => B not Turing-recognizable

In class:
- $E_{TM} ≤_m EQ_{TM}$
- $A_{TM} ≤_m HALT_{TM}$
- $A_{TM} ≤_m \overline{E_{TM}}$
  

$A≤_mB \leftrightarrow \overline{A} ≤_m\overline{B}$ -- same reduction f

To show $A≤_mB$: show the contrapositive of [**A undecidable => B undecidable**] i.e. **[b decidable => A decidable]**



DFA = NFA < DPDA < PDA < DTM



---



## 7. Time Complexity

#### Thms & Corollary
- If A is nonregular, then A ∈ TIME(f(n)) for any f(n) = O(nlogn)
- $\rightarrow$ there's no O(n) decider for {$0^k1^k | k≥0$}
- If A is regular, then A ∈ TIME(n)
- $t(n)$-time MTDTM can be converted to $O(t^2(n))$ time STDTM
- $t(n)$-time STNTM can be converted to $2^{O(t(n))}$ time STDTM
  - $t(n)$-time STNTM $\rightarrow??t^k(n)$ time STDTM?? - P v NP
  
### Class P, NP
- **TIME (t(n))** = {A | A decidable by an O(t(n)) time DTM}.
- **NTIME (t(n))** = {A | A decidable by an O(t(n)) time NTM}.

- **P** = { A | $\exist$ poly-time *STDTM* that decides A} 
  - $\cup_k$TIME($n^k$).
- **NP** = { A | $\exist$ poly-time *STNTM* that decides A} 
  - = {A | $\exist$ poly-time verifier for A} 
  - = $\cup_k$NTIME($n^k$)
- $coNP = \overline{NP}$

PATH ∈ P
COMPOSITES ∈ NP
COMPOSITES = {$ x $ | $ \exists $ p, q > 1 s.t. $x=p*q$} $\in NP$
$A_{TM}$ ∈ NP-hard

- To prove a langauge A is in P: give a poly-time decider, usually by using abother poly-time decider for another language
- To prove a langauge A is in NP: give a poly-time verifier
  - A verifier is a TM/algorithm s.t A = {w | $\exist$ string c s.t V accepts <w,c>}
  - c = certificated, proposed solution
```
Poly-time verifier for HAMPATH:
  c(G,s,t) = a Hamiltonian Path from s to t 
  V(<G,s,t>, c): 
    Check if c is an s-t HamPath. 
    if so: accept, else: reject
```


## 8 Space Complexity
- **SPACE (f(n))** = {A | A decidable by an O(t(n)) space STDTM}.
- **NSPACE (f(n))** = { A | A decidable by an O(t(n)) space STNTM}.

PSPACE = $\cup_k$SPACE($n^k$)
NPSPACE=$\cup_k$NSPACE($n^k$)

**Facts:**
- TIME($t(n)$) $\subseteq$ SPACE($t(n)$)
- SPACE($t(n$)) $\subseteq$ TIME($2^{t(n)}$)

P $\subseteq$ NP $\subseteq$ PSPACE = NPSPACE $\subseteq$ EXPTIME $\subseteq$ EXPSPACE
##### Savitch's Thm
$\forall f$ s.t. f(n)≥ n, NPSPACE($f(n)$) $\subseteq$ PSPACE($f^2(n)$)
-direct result: PSPACE = NPSPACE


##### TQBF is PSPACE-complete
**PSPACE-complete** = in PSPACE & PSPACE-hard (∀A in PSPACE, A≤pB)
The TQBF problem is a generalization of SAT.
**TQBF = {⟨φ⟩ | φ is a true fully quantified Boolean formula}.**
ex) φ = ∀x ∃y [(x ∨ y) ∧ (x ∨ y)] is a true QBF (y = x makes φ = 1).

**Facts**: 
- ∃y∀x[φ] is stronger than ∀x∃y[φ]
  - ∃y∀x[φ] = there exists a y that works for all x
  - ∀x∃y[φ] = there exists a y for each chosen x
- B is PSPACE-hard => B is NP-hard 

**SAT ≤p TQBF**
```
f(φ):
  return ∃x1 ∃x2...∃xn[φ]
```


**TQBF ≤ Formula-Game**

```
f(φ):
  return φ
```

**Formula-Game**
- **input**: QBF φ = \<quantifiers>[Ψ], a quantified boolean formula
- **players**: player E want to show Ψ is true, player A wants to show it's false
- **game**: for each variable xi, in φ, if xi is bound to ∃, player E assign a value to xi, if it's bound to a ∀, player A assign.
- Formula-Game = {φ | player E can force a win}


**Generalized Geography**
- input: a directed graph G, start vertex x, and two players alternate picking vertices in G, s.t the chosen vertices must collectively form a path in G 
- (no repeat vertices); the first player to get “stuck” loses. 
- GenGeo = {<G, s> | player 1 can force a win}
- PSPACE-hard

**Formula-Game ≤ GenGeo**

# Knowledge

#### Knowledge-based agents:

Agents that reason by operating on internal representations of knowledge.

#### Sentence:

An assertion about the world in a knowledge representation language

## Propositional Logic

A type of logic based on propositions.

### Propositional Symbols:

_P_ - _Q_ - _R_

### Logical Connectives:

¬ (not), ∧ (and), ∨ (or), → (implication) and ↔ (biconditional)

#### Not (¬)

| _P_   | ¬*P*  |
| ----- | ----- |
| false | true  |
| true  | false |

#### And (∧)

| _P_   | _Q_   | _P_ ∧ _Q_ |
| ----- | ----- | --------- |
| false | false | false     |
| false | true  | false     |
| true  | false | false     |
| true  | true  | true      |

#### Or (∨)

| _P_   | _Q_   | _P_ ∨ _Q_ |
| ----- | ----- | --------- |
| false | false | false     |
| false | true  | true      |
| true  | false | true      |
| true  | true  | true      |

#### Implication (→)

| _P_   | _Q_   | _P_ → _Q_ |
| ----- | ----- | --------- |
| false | false | true      |
| false | true  | true      |
| true  | false | false     |
| true  | true  | true      |

If _P_ is false, then it doesn't matter what _Q_ is, it'll always evaluate the implication to true.

#### Biconditional (↔)

| _P_   | _Q_   | _P_ ↔ _Q_ |
| ----- | ----- | --------- |
| false | false | true      |
| false | true  | false     |
| true  | false | false     |
| true  | true  | true      |

Kind of like an "if and only if" statement.

#### Model:

Assignment of a truth value to every propositional symbol (a "possible world").

#### Knowledge base:

A set of sentences known by a knowledge-based agent.

#### Entailment:

_α_ ⊨ _β_

In every model in which sentence **α** is true, sentence **β** is also true.

#### Inference:

The process of deriving new sentences from old ones.

Example:

**_P_** : It is a Tuesday.  
**_Q_** : It is raining.  
**_R_** : Harry will go for a run.

**_KB_**: (**_P_** ∧ ¬**_Q_**) → **_R_**

Inference: **_R_**

## Inference Algorithms

Algorithms that allows us to draw conclusions.

Does KB ⊨ α ?

### Model Checking:

- To determine if **KB** ⊨ _α_:
  - Enumerate all possible models.
  - If in every model where **KB** is true, _α_ is true, then **KB** entails _α_
  - Otherwise, **KB** does not entail _α_

**_P_** : It is a Tuesday **_Q_** : It is raining. **_R_** : Harry will go for a run.

**KB**: (**_P_** ∧ ¬**_Q_**) → **_R_**

**_P_** is true.  
**_Q_** is true.

Query: **_R_**

| **_P_** | **_Q_** | **_R_** | **_KB_** |
| ------- | ------- | ------- | -------- |
| false   | false   | false   | false    |
| false   | false   | true    | false    |
| false   | true    | false   | false    |
| false   | true    | true    | false    |
| true    | false   | false   | false    |
| true    | false   | true    | true     |
| true    | true    | false   | false    |
| true    | true    | true    | false    |

#### Knowledge Engineering:

The process of taking a problem and figure out how to represent knowledge in a way that a computer can understand.

## Inference Rules

Rules that we can apply to knowledge to get new forms of knowledge.

```
  Premise
―――――――――――
 Conclusion
```

### Modus Ponens

```
α → β
  α
―――――
  β
```

Example:

If it is raining, then Harry is inside (α → β).  
It is raining (α).  
Harry is inside (β).

### And elimination

If both α and β are true, then one of them must also be true.

```
α ∧ β
―――――
  α
```

Example:

Harry is friends with Ron and Hermione (α ∧ β).  
Harry is friends with Hermione (β).

### Double Negation Elimination

If the premise is `not(not(α))`, then the conclusion is α.

```
¬(¬α)
―――――
  α
```

Example:

It is not true that Harry did not pass the test (¬(¬α)).  
Harry passed the test (α).

### Implication Elimination

If α implies β, then either not α or β is true.

```
 α → β
―――――――
¬α ∨ β
```

Example:

If it is raining, then Harry is inside (α → β).
It is not raining or Harry is inside (¬α ∨ β).

### Biconditional Elimination

α is true if and only if β is true, in which case α imples β and β implies α.

```
        α ↔ β
―――――――――――――――――――――
  (α → β) ∧ (β → α)
```

Example:

It is raining if and only if Harry is inside (α ↔ β).  
If it is raining, then Harry is inside, and if Harry is inside, then it is raining ((α → β) ∧ (β → α)).

### De Morgan's Law

If it is not true that α and β, then either not α or not β.

```
  ¬(α ∧ β)        Inverse:  ¬(α ∨ β)
―――――――――――――             ―――――――――――――
   ¬α ∨ ¬β                   ¬α ∧ ¬β
```

Example:

It is not true that both Harry and Ron passed the test (¬(α ∧ β)).  
Harry did not pass the test or Ron did not pass the test (¬α ∨ ¬β).

### Distributive Property

It works the same way as the distributive law in maths.

```
    (α ∧ (β ∨ γ))           (α ∨ (β ∧ γ))
―――――――――――――――――――――   ―――――――――――――――――――――
  (α ∧ β) ∨ (α ∧ γ)       (α ∨ β) ∧ (α ∨ γ)
```

### Resolution

```
 P ∨ Q       P ∨ Q1 ∨ Q2 ∨ ...∨ Qn        P ∨ Q              P ∨ Q1 ∨ Q2 ∨ ...∨ Qn
  ¬P                ¬P                   ¬P ∨ R              ¬P ∨ R1 ∨ R2 ∨ ...v Rm
―――――――   ――――――――――――――――――――――――――――   ―――――――   ―――――――――――――――――――――――――――――――――――――――――
   Q          Q1, ∨ Q2 ∨ ...∨ Qn          Q ∨ R      Q1 ∨ Q2 ∨ ...∨ Qn ∨ R1 ∨ R2 ∨ ...∨ Rm
```

Example:

Ron is in the Great Hall or Hermione is in the library (P ∨ Q).  
Ron is not in the Great Hall (¬P).  
Hermione is in the library.

Ron is in the Great Hall or Hermione is in the library (P ∨ Q).  
Ron is not in the Great Hall or Harry is sleeping (¬P ∨ R).  
Hermione is in the library or Harry is sleeping (Q ∨ R).

#### Theorem Proving:

- Initial state: starting knowledge base.
- Actions: inference rules.
- Transition model: new knowledge base after inference.
- Goal test: check statement we're trying to prove.
- Path cost function: number of steps in proof.

#### Clause:

A disjunction of literals.

Example:

_P_ ∨ _Q_ ∨ _R_

### Conjuctive normal form:

A logical sentence that is a conjuction of clauses.  
We can turn any sentence into a CNF by applying inference rules to it.

Example:

(_A_ ∨ _B_ ∨ _C_) ∧ (_D_ ∨ _¬E_) ∧ (_F_ ∨ _G_)

### Conversion to CNF

- Eliminate biconditionals
  - turn (α ↔ β) into (α → β) ∧ (β → α)
- Eliminate implications
  - turn (α → β) into ¬α ∨ β
- Move ¬ inwards using De Morgan's Laws
  - e.g. turn ¬(α ∧ β) into ¬α ∨ ¬β
- Use distributive law to distribute ∨ wherever possible

Example:

```
    (P ∨ Q) → R
        ↓
eliminate implication
        ↓
    ¬(P ∨ Q) ∨ R
        ↓
  De Morgan's Law
        ↓
    (¬P ∧ ¬Q) ∨ R
        ↓
  distributive law
        ↓
  (¬P ∨ R) ∧ (¬Q ∨ R)
```

Conversion to CNF comes in handy when trying to use the resolution inference rule because when we convert a formula to CNF we get back clauses.

### Inference by Resolution

#### Factoring:

When there are duplicate variables, we can eliminate them without affecting the meaning of the sentence.

Example:

```
   P ∨ Q ∨ S
  ¬P ∨ R ∨ S
――――――――――――――
  (Q ∨ S ∨ R)
```

#### Empty clause:

The empty clause always evaluate to false.

Example:

```
   P
   ¬P
―――――――
  ()
```

### Algorithm

To determine if **_KB_** ⊨ _α_:

- Check if (**_KB_** ∧ ¬*α*) is a contradiction?

  - If so, then **_KB_** ⊨ _α_.
  - Otherwise, no entailment.

To determine if **_KB_** ⊨ _α_:

- Convert (**_KB_** ∧ ¬*α*) to Conjunctive Normal Form.
- Keep checking to see if we can use resolution to
  produce a new clause.
  - If ever we produce the empty clause (equivalent
    to False), we have a contradiction, and **_KB_** ⊨ _α_.
  - Otherwise, if we can't add new clauses, no
    entailment.

Example:

Does (A ∨ B) ∧ (¬B ∨ C) ∧ (¬C) entail A?

```
(A ∨ B) ∧ (¬B ∨ C) ∧ (¬C) ∧ (¬A)
              ↓
          Resolution
              ↓
     (¬B ∨ C) - (¬C) → (¬B)
              ↓
          Resolution
              ↓
      (A ∨ B) - (¬B) → (A)
              ↓
          Resolution
              ↓
          (¬A) - (A)
              ↓
              ()
```

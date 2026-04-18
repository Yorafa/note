# Binary Relations

**Binary Relations**: Denote a relation over a set $A$ be $R$, if the relation is binary relation, then $\forall a,b \in A$

-   if $a$ relates $b$ under relation $R$, denote as $aRb$
-   else $a\not R b$

Some Property of Binary Relations $R$ over a set $A$ may have:

-   irreflexive: $\forall a \in A, a\not R a$ 
-   reflexive: $\forall a \in A, aRa$ 
-   asymmetric: $\forall a,b \in A,  aRb\implies b\not R  a$
-   symmetric: $\forall a,b \in A,  aRb\implies bRa$
-   antisymmetric: $\forall a,b\in A (aRb\land bRa \implies a=b)$
-   transitive: $\forall a,b,c \in A, aRb \land bRc \implies aRc$
-   connected: $\forall a,b \in A, a\ne b \implies aRb \lor bRa$
-   cyclic: $\forall a,b,c\in A, aRb\land bRc \implies cRa$
-   irreflexive $\land$ transitive $\implies$ asymmetric

**Strict (partial) Order**: a binary relation $R$ over a set $A$ is _irreflexive, asymmetric(not necessary) and transitive_

-   e.g.: Dependencies, Little-o, $\sub$, etc.

**Strict Total Order**: a binary relation $R$ over a set $A$ is strict order and connected

-   e.g.: Dictionary Order,  etc.

**Hasse Diagram**: $\forall R, R$ is strict order over a set $A$,  $\forall a,b \in A$, Hasse diagram has a edge $a\to b \iff a Rb \land \nexists c, aRc \land cRb$

Notice: it (binary relation) is very different with the binary operation of group theory.

**Partial Order**: a binary relation $R$ over a set $A$ is _reflexive, antisymmetric and transitive_

**Total Order**: a binary relation $R$ over a set $A$ is partial order and connected.

**Equivalence Relation**: a binary relation $R$ over a set $A$ is _reflexive, symmetric and transitive_

-   e.g. $=$, modular $(\equiv_n): a =b(mod \ n), a,b,n\in \N$
-   cyclic and reflexive $R \implies$ $R$ is equivalence relation 

**Equivalence Class**:  Let $R$ be Equivalence Relation on a set $A$, $\forall a\in A$, the Equivalence Class of $a$ respect to $R$, denoted $[a]_R$ has property $[a]_R = \{b\in A: aRb\}$

-   $\forall a,b \in A, [a]_R= [b]_R \iff aRb$ (lemma)

**Partition**: let $A$ be any set, and $X$ be a collection of subsets of $A$. $\forall a\in A, \exists S\in X, a\in S \implies X$ is a partition of $A$

-   Let $R$ be an equivalence relation on a set $A$. The set of Equivalence Classes is a partition of $A$. 
-   Or we can say $\forall a \in A, \exists [a]_R, a\in[a]_R, [a]_R$ is unique
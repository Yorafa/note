# Amortized Analysis

We average the time that required to perform a sequence of data-strcuture operations over all the operations performed in the **Amortized Analysis**. That is, amortized analysis is also a time complexity analysis technique that is used to analyze the average time complexity of an algorithm or operation but without probabilistic analysis. In addtion, amortized analysis guarantees that the average performance of each operation in the worst case.


## Aggregate Analysis

We first define $\forall n$ a sequence of $n$ operations takes worst-case time $T(n)$ in total. Then, the average cost or **amortized cost** of worst case per operation is $T(n)/n$. 

## Accounting Method

We assign differing charges to different operations with some operations charge which may pay more/less than they actually cost, and the **amortized cost** is the amount we charge for each operation (the assigned one). When an operation's amortized cost exceeds its acutal cost, we assign the difference to specific objects in the data structure as **credit**.  Credit help to pay for later opeations whose amortized ccost less than their actually cost.

we want to make sure we have an overall balance of zero. That is, the total amount of credit we assign to the data structure is bigger or equal to the total amount of charge we assign to the data structure so that we approach the actual cost of the sequence of operations. That is, the total amortized cost of a sequence of operations provides an upper bound on the total actual cost of the sequence.

## Dynamic Tables

Dynamic Table in CLRS is the same as dynamic array we talked about in the lecture. By using double extension, we can make sure the load factor always satisfies $0.5 \le \alpha \le 1$.
- Notice, an empty table with $\alpha = 1$
- Notice, when we extend the table, we actually copy all the elements in the old table to the new table so that we have worst-case time $O(n)$ for a single insertion

We can not hard to get $\sum_{i}^n c_i \le 3n$ where we only have $i$ cost when $i$ is power of 2 so that we have average cost $O(1)$ for each insertion. As we continued on accounting method, we give each element 3 credits. Moreover, 1 credit use for insertion, 1 credit use for moving to new table, and 1 credit use for giving other elements who has 0 credit. Therefore, for each insertion, we always have enough credit to pay for the insertion.

Furthrmore, if we don't use the double extension, instead of multiply something $(1 + \beta)$, we we charge $1 + \frac{1}{\beta}$ on copying so that we will have $2 + \frac{1}{\beta}$ credits for each element.
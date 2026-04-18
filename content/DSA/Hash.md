Hash rather than a data structure, it's more like a algorithm. It provide $O(1)$ time complexity to quickly access the elements. We want to find a efficient bi-jection function to store data.

Ingredients to make hash table:

- universe: set of all possible keys $U = |U|$ very large, otherwise we could use direct access something like array
- For a hash table, T, $|T| = m$, $T$ is an array and $m$ depends, as big as needed.
- a hash function $h: U \to \{0,1, \ldots,m-1\}$
- load factor $\alpha = \frac{|U|}{|T|} = n/m$, if $\alpha$ is too big, we need to rehash. Load factor is the average number of elements in a chain.

That's, we have space $T[h(u)]$, and following method:

`search(k):` look for $T[h(k)]$

`insert(k):` change in $T[h(k)]$

`delete(k):` remove k from $T[h(k)]$

Normally, we create a hash function with division method, multiplication method

- division method: $h(k) = k \mod m$
- multiplication method: $h(k) = \lfloor m(kA \mod 1)\rfloor$, where $A = (\sqrt{5}-1)/2$ is the golden ratio, and $m$ is the size of the table, $kA \mod 1 = kA - \lfloor kA \rfloor$ is the fractional part of $kA$.

For a hash table, we also can do **chaining**. That is, we have a linked list in each slot of the hash table. We can use a linked list to store the elements that have the same hash value.

In a hashing, we also define the situation **open addressing** when all elements occupy the hash table itself.

## Hashing with Chaining

We define load factor $\alpha = \frac{n}{m}$, where $n$ is the number of elements in the table, and $m$ is the size of the table, or we would like to say the average number of elements in a chain.

| Operation | Worst-case Running Time | Average-case Running Time |
| :-------: | :---------------------: | :-----------------------: |
|  Search   |       $\Theta(n)$       |    $\Theta(1+\alpha)$     |
|  Insert   |       $\Theta(n)$       |    $\Theta(1+\alpha)$     |
|  Delete   |       $\Theta(n)$       |    $\Theta(1+\alpha)$     |

## Open Addressing

In open addressing, each table entry contains either an element or NIL. We have three methods to deal with collision:

- linear probing: $h(k,i) = (h(k) + i) \mod m$
- quadratic probing: $h(k,i) = (h(k) + c_1i + c_2i^2) \mod m$
- double hashing: $h(k,i) = (h_1(k) + ih_2(k)) \mod m$
- i is the number of full slots

Linear probing suffer from primary clustering problem where whenever we reach a non-empty slot, we will rise the i which increasing the average searching time.

Quadratic probing is better than linear probing, but it still suffer from Secondary clustering problem where the iniital probe position equal implies their probe sequence will be the same.

Double hashing is the best method among the three, it requires two relative prime hash functions.

Double hashing provide distinct probe sequence where use $\Theta(m)$ space which better than $\Theta(m^2)$ space of quadratic probing and linear probing.

In open addressing, the load factor is bounded where $\alpha \le 1$ since $n \le m$.

| Operation |   Average-case Running Time    |
| :-------: | :----------------------------: |
|  Search   | $\Theta(1+\frac{1}{1-\alpha})$ |
|  Insert   | $\Theta(1+\frac{1}{1-\alpha})$ |
|  Delete   | $\Theta(1+\frac{1}{1-\alpha})$ |

## something more

Even though the worse-case running time of hash table operations are worse than that of AVL trees, the average-case running time of hash table operations are much better than the running time of AVL trees.

You are asked to implement your own hash map. What are good things to do?

1. Use a prime number modulus in your hash function
2. Design a hash function that spreads hashes evenly
3. Implement some sort of method to handle collisions (i.e. chaining, linear probing, etc.)

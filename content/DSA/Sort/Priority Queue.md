# Priority Queue

Priority Queue is an ADT that the item in it will be sorted in given priority. Basically, there are 3 operation of a priority queue where we can insert, find the max priority item and extract the max priority queue.

`Insert(PQ, x, priority):` Add x into  PQ with the priority queue PQ

`FindMax(PQ):` Return the item in PQ with the highest priority

`ExtractMax(PQ):` Remove and return an item from PQ with the highest priority.

## Implement

The easiest implement of a priority queue we can just simply use the heap. See more about heap.


## Worst-Case Time complexity

| Operation | Time Complexity |
|:---------:|:---------------:|
| Insert    | O(log n)        |
| FindMax   | O(1)            |
| ExtractMax| O(log n)        |

# Quick Sort

When we talk about the quick sort method we always saids about the random quick sort. Quicksort basically is a divide and conquer algorithm. It works by selecting a 'pivot' element from the array and partitioning the other elements into two sub-arrays, according to whether they are less than or greater than the pivot. Those sub-arrays are then sorted recursively. The deterministic version will take a fix pivot, and the random version will take a random pivot.

The maximum expected running time of deterministic quick sort is longer than random quick sort.

## Implement

```python
def quick_sort(arr):
    if len(arr) <= 1:
        return arr
    pivot = random.choice(arr)
    smaller, larger = partition(arr, pivot)
    smaller = quick_sort(smaller)
    larger = quick_sort(larger)
    return smaller + larger
    
def partition(arr, pivot):
    smaller = [x for x in arr if x <= pivot]
    larger = [x for x in arr if x > pivot]
    return smaller, larger
```

## Worst-Case Time Complexity

We have $T(n) = T(n-1) + T(0) + \Theta(n) = T(n-1) + \Theta(n)$. By the master theorem, we have $T(n) = \Theta(n^2)$.

| Algorithm | Best Case | Average Case | Worst Case |
| :---: | :---: | :---: | :---: |
| Deterministic Quick Sort | $O(n\log n)$ | $O(n\log n)$ | $O(n^2)$ |
| Random Quick Sort | $O(n\log n)$ | $O(n\log n)$ | $O(n^2)$ |

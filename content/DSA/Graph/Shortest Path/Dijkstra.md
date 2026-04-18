#dijkstra 
只能用于非负权图
定义`dis[v]` 为起点到点`v`的最短路，与Bellman-Ford不同的地方在于 Dijkstra 可以有序遍历边，这使得其速度有提高，但相应的无法应用于负数环。
Dijkstra从起点开始，将与起点相连的边添加进子图中，并做与Bellman-Ford相同的松弛操作`dis[v] = min(dis[v], dis[u] + w[u][v])`.
时间复杂度：`O(n^2 + m) = O(n^2)`

在稀疏图(即 `m = O(n)`) 中可以使用优先队列优化到`O(mlogn)`. 而在稠密图(即 `m = O(n^2)`) 中,优先队列则没有优势.

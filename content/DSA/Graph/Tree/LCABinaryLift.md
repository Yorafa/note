与[快速幂](../../快速幂)相同的思想。用于在一个总数有`n`个`node`的节点的树上，以`log(n)`时间复杂度下快速寻找最早公共ancestor，其中`ancestor[i][j]`表示`i`位的第`2^j`个先祖。

这样以来，我们要找第`k`个先祖也就是找$k= \sum_{i = 0}^{n} = a_i2^i$

举个例子，找第`k = 3`个先祖，也就是说`ancestor[ancestor[curr][0]][1]`或者`ancestor[ancestor[curr][1]][0]`. 用大白话来说就是寻找太爷爷，而太爷爷不光是是爷爷的爸爸，也是爸爸的爷爷。

```python
def LCABL:
	def __init__(self, root):
		# 题目不一定总给root, 但总归是要建图建树
		graph = traverse(root) # traverse需要自己实现，总之是用于建图的一个func
		n = len(graph)
		nbits = n.bit_length()
		ancestor = [[-1 for _ in range(nbits)] for _ in range(n)]
		dis = [0] * n
		dfs(root.id) # 通过traverse或者dfs等方式更新dis, 即在树上的哪一层
		             # 以及更新ancestor[i][0]即他们的父亲都是谁
		for i in range(nbits):
			for j in range(n): # 这里假设了id是[0, n - 1]，如果不是需要自己更改
				if ancestor[j][i] == -1:
					continue
				# 爷爷是父亲的父亲
				ancestor[j][i + 1] = ancestor[ancestor[j][i]][i]
		# 存进class结构中
		self.dis = dis
		self.ancestor = ancestor
	def get_kth_ancestor(self, k, curr):
		nbits = k.bit_length()
		for i in range(nbits):
			if (k >> i) & 1:
				curr = self.ancestor[curr][i]
		return curr
	def get_lca(self, x, y):
		if depth[x] > depth[y]:
			x, y = y, x
		# 现在确保了y的深度大, 接下来使两者高度相同
		y = self.get_kth_ancestor(depth[y] - depth[x], y)
		if x == y:
			return x
		for i in range(len(self.ancestor[x]) - 1, -1, -1):
			px, py = self.ancestor[x][i], self.ancestor[y][i]
			if px == py:
				# 如果祖先相同说明，前面在\sum_{j = 0}^{n} = a_j2^j [0, j] 之间
				#可能还有相同祖先
				continue
			# 太爷爷是爷爷的爸爸
			x, y = px, py
		# for loop实际上找的一直都是[0, j] 之间最后一个不同的数
		# 所以返回他们的parent
		return self.ancestor[x][0]
```

### 例题

[Number of Ways to Assign Edge Weights II](https://leetcode.com/problems/number-of-ways-to-assign-edge-weights-ii/)

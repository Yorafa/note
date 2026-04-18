由AhoCorasick提出了的自动机，在[Trie](./Trie)上使用[KMP](./KMP)进行多模字符串匹配

其中`fail`基于[KMP](KMP)算法，确保当前`s[i] != p[j]`时可以回到上一个`s[i - 1] = p[k]`的点以便于继续比较`s[i]`与`p[k+1]`从而节省了完全从头开始 匹配的时间

其中`last`保留了上一个匹配成功的点，即另一个pattern的match，这样当我们成功匹配一个pattern的时候才不会错过另一个pattern. 例如给定多pattern `ps = ["abcabc", "abc", "dcabc"]` 在如果一个字符串match到`abcabc`或`dcabc`，那么它也一定match到`abc`，这时我们就可以直接通过`last`回溯找到所有的matched pattern而不用再从头开始再重新跑一遍

```python
class TrieNode:
	def __init__(self):
		self.son = [None] * 26 # 或128，256这取决于字符
		self.fail = None       # 记录上一个最近kmp匹配点
		self.last = None       # 如果当前匹配成功，还可以通过last回溯所有的成功匹配
		self.len = 0
		
class AhoCorasick:
	def __init__(self):
		self.root = TrieNode()
		
	def put(self, s):
		curr = self.root
		for i, son in enumerate(curr.son):
			if not son:
				curr.son[i] = TrieNode()
			curr = curr.son[i]
		curr.len = len(s)
		
	def build_fail(self):
		curr = self.root
		curr.fail = curr.last = curr
		q = deque()
		for i, son in enumerate(curr.son):
			if not son:
				curr.son[i] = curr # 因为没有任何匹配所以直接回到开头重新做匹配
				continue
			son.fail = son.last = curr # 第一层的没有fail和last所以回到开头
			q.append(son)
		while q:
			curr = q.popleft()
			for i, son in enumerate(curr.son):
				if not son:
					curr.son[i] = curr.fail.son[i] # 匹配失败回到最近匹配
												   # 即 k = p[k - 1]
					continue
				son.fail = curr.fail.son[i]
				# 判断是否上次匹配是一个完整匹配，如果不是继续往前回溯
				# 因为我们每次的判断都是一样的，所以不需要写一个while去判断每个之前
				#的last是否是完整的，在if下可以得知curr.fail.last要么是完整的要么是
				#self.root
				son.last = son.fail if son.fail.len else son.fail.last
				q.append(son)
				
```

## 参考例题
[Construct String with Minimum Cost](https://leetcode.com/problems/construct-string-with-minimum-cost/)
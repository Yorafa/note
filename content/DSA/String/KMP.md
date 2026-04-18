KMP全称是Knuth–Morris–Pratt algorithm，用`O(m + n)`的时间复杂度从字符串`s`中找到匹配串`p`.
此外还可以与[Trie](./Trie)结合([AC自动机](./AC自动机))用于解决多模式匹配问题。

KMP的核心思想是如果`s[i] != p[j]`, 那么`j`快速回到`k`使得`s[i+k:i-1]` 和 `p[:k]`保持一样。如果`s[i] != p[k]`那么继续回退。这么做实际上是通过调整`j`在`p`的位置以高效利用在`i`和`j`之前`s`和`p` 匹配上的部分

如何给 `p` 记录前面匹配的部分呢？自己和自己对比
```python
kmp = [0] * len(p)
curr_match_len = 0
for i, c in enumerate(p):
	while curr_match_len != 0 and c != p[curr_match_len]:
		curr_match_len = p[curr_match_len - 1]
	if c == p[curr_match_len]:
		curr_match_len += 1
	p[i] = curr_match_len
```
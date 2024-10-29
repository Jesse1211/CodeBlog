+++
authors = ["Jesse"]
title = "DFS"
date = "2024-10-13"
tags = [
    "hugo",
    "markdown",
    "css",
    "html",
    "shortcodes",
]
categories = [
    "theme demo",
    "syntax",
]
series = ["Theme Demo"]
aliases = ["migrate-from-jekyl"]
+++

## O(n \* m)

### Tree

```python
dfs(res, root, value) {
    if (!root):
        return

    if (value = root.val):
        res.add(root)
        return

    for option : options:
        做选择
        dfs(res, newRoot, newValue)
        撤销选择
}
```

1. base case: if == null
2. inductive case: if can make recursive call
3. return false if needed

低阶
{{< notice question >}}
98, 100, 112, 129, 145, 226, 257, 404, 572, 938
{{< /notice >}}

高阶
{{< notice warning >}}
113, 114, 124, 235, **250**, **236**, **333**, 437, 530, **536**, **865**, 1367

- Inorder traversal: left root right
- Preorder traversal: root, left, right
- Postorder traversal: left, right, root

**105**, **173**, **270**, **285**, **426**, 530
{{< /notice >}}

---

### dfs Helper function (e.g. Permutation - 找到所有可能性)

```JAVA
dfs(options, visited, cur, res, index){
	// base case
	if index reaches limit {
		res.add(new cur);
		return;
	}

    visitedValue = new HashSet<>();    // 如果有duplication, 这里要做一个visitedValue Set防重, 不需要删除
	for (all possible steps : i) {
		if i in visited {
			continue;
		}
		visited.add(i);
		cur.add(i);
		dfs(options, visited, i, res, newIndex);
		cur.remove(cur.size() - 1);
		visited.remove(i);
	}
}
```

- dfs helper function 看情况使用
- 一般是四个 param: (所有选项, 当前 index, res, cur)
- **如果结果有序: 需要用 index; 如果无序: 可以用 set 来防重**

1. base case: index 或者 cur 达到上限
2. inductive:
   - recursive call with new index & cur
     - **cur.add()** + dfs(...) + **cur.remove()**
   - 如果是更改 input, 需要快慢指针 swap 来代替 cur 和 res
   - dfs()/main()中可以加 set 来防重
     - 取决于题型: 前后 add + remove, 或者设定 true / false
     - 取决于题型: set 保存 value 还是 index

{{< notice question >}}
17, 39, 40, 46, 47, 77, 78, 90, 131, 216, 419, 1079
{{< /notice >}}

{{< notice warning >}}
22, 79, 93, 207, 386, **526**, 547
{{< /notice >}}

---

### Trie

{{< notice warning >}}
211, 212
{{< /notice >}}

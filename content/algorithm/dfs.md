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
dfs(root, value) {
    if (!root):
        return false

    if (value = root.val):
        return true

    return dfs(root.left, newValue) || dfs(root.right, newValue)
}
```

1. base case: if == null
2. inductive case: if can make recursive call
3. return false if needed

{{< notice question >}}
98, 100, **105**, 112, **113**, **114**, 129, 226, **235**, **236**, 572, 1650

- 114 有点可怕
  {{< /notice >}}

{{< notice note >}}

- Inorder traversal: left root right
- Preorder traversal: root, left, right
- Postorder traversal: left, right, root

{{< /notice >}}

---

### dfs Helper function (e.g. Permutation - 找到所有可能性)

```python
dfs(options, visited, cur, res, index){
	// base case
	if index reaches limit {
		res.add(new cur);
		return;
	}

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
- _如果结果有序: 需要用 index; 如果无序: 可以用 set 来防重_

1. base case: index 或者 cur 达到上限
2. inductive:
   - recursive call with new index & cur
     - **cur.add()** + dfs(...) + **cur.remove()**
   - 如果是更改 input, 需要快慢指针 swap 来代替 cur 和 res
   - dfs()/main()中可以加 set 来防重
     - 取决于题型: 前后 add + remove, 或者设定 true / false
     - 取决于题型: set 保存 value 还是 index

{{< notice question >}}
17, **22**, 39, 40, 46, **47**, 77, 78, 79, **90**, **93**, **131**, **207**, 216, 526, **547**, 1079
{{< /notice >}}

---

### Matrix (个人喜好 BFS)

{{< notice question >}}
**212** - highlight: Trie!
{{< /notice >}}

+++
authors = ["Jesse"]
title = "DFS"
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

- [x] 98 - ⭐️ 经典 BST validation
- [x] 113 - ⭐️ 经典 DFS, recursion 前 list.add(), 后 list.removeLast(). base case res.add(new ArrayList<>(list))
- [ ] 114
- [ ] 124
- [ ] 129
- [ ] 145
- [ ] 226
- [ ] 235
- [ ] 236
- [ ] 250
- [ ] 257
- [ ] 298
- [ ] 333
- [ ] 404
- [ ] 430
- [ ] 449 - ❤️ ⭐️⭐️⭐️⭐️ Tree Serialization, postorder, Stack, dfs
- [ ] 572
- [ ] 865
- [ ] 938
- [ ] 1367
- [ ] 1530 - ❤️ ⭐️⭐️⭐️⭐️⭐️
- [ ] 1650

{{< /notice >}}

---

- Inorder traversal: left root right
- Preorder traversal: root, left, right
- Postorder traversal: left, right, root

低阶
{{< notice question >}}
173, 270, **437**, **510**, 530
{{< /notice >}}
高阶
{{< notice warning >}}
105, 106, 285, 426
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
17, 22, 39, 46, 77, 78, 79, **131**, 216, 386, 419
{{< /notice >}}

{{< notice warning >}}
51, 93, 526, 694, 547

- 防重技巧: 40, 47, 90, 1079

{{< /notice >}}

---

### Time Complexity

- **x^n**: n 个 node, 每个 node 都可以做 x 次 recursive call

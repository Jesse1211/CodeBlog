+++
authors = ["Jesse"]
title = "BFS"
+++

## Shortcodes O(n \* m)

```python
while (q is not empty) {
	traverse q {
		var cur = q.poll();

		traverse cur.children {
			if cur.child is valid {
				if (cur.child is valid) {
					do something;
					add cur.child to q;
				}
			}
		}
	}
}
```

### Tree: 以 root 为中心

- 横向: 把 tree 转换成 Array 的两种表达式:
  1.  以 root 为中心 root = i, left = i - 1, right = i + 1.
  2.  以 root 为起点, 右下角 leaf 为终点. root = i, left = i _ 2, right = i _ 2 + 1.
      - 从左往右看每一个 level
- 纵向: 通过 Queue / Map 监控每个 node 的 index, 加上当前 Level 便可找出具体 node
  1. Root.index = 1
  2. Root.left.index = Root.index - 1; Root.right.index = Root.index + 1;

{{< notice question >}}
(基础框架 + ...)

- [x] 107 - ⭐️ boolean ifReverse
- [x] 117 - ⭐️⭐️ 特殊处理每层第一个 node
- [x] 199 - ⭐️⭐️ 特殊处理每层最后一个 node
- [x] 261 - ⭐️⭐️⭐️ Queue 配合 Set, 不需要 Topological Sort(已知起点为 0)
- [ ] 297 - ⭐️⭐️⭐️ Tree Serialization
- [x] 314 - ⭐️⭐️⭐️ Map 应用于 column 信息, 额外的 Queue 保存每个 Node 的 Index
- [ ] 449 - ⭐️⭐️⭐️ Tree Serialization
- [ ] 513
- [x] 662 - ⭐️⭐️⭐️⭐️ 314 增强版. 注意 Index (x \* 2 + 1), min & max 计算方式 (min 等于每个 level 的第一个 node.index)
- [ ] 958
- [ ] 987
- [ ] 1530
- [ ] 1609

{{< /notice >}}

---

### Matrix, Graph, 无规则 List: 指定点为中心

1. 难点 - 用 Map 或者 list 来重新梳理一下信息
2. 通过题目的信息来用一下 trick 来防重
   - `int[] minCost = new int[n];`
   - `Set<> visited = new HashSet();`
   - Change value when traversing, change back after
3. 防重可以通过`HashSet`或者`int[]`
   - `HashSet`: 无脑防止第二次 access
   - `int[]`: 根据 cost 或其他数据避免不需要的 access

#### 正推 From center

- 找到中心, 一层一层“向外剥”

低阶
{{< notice question >}}

- [ ] 127 - 双向 BFS
- [ ] 133
- [ ] 200
- [ ] 279
- [ ] 301
- [ ] 322
- [ ] 365
- [ ] 490
- [ ] 690
- [ ] 733
- [ ] 752
- [ ] 787
- [ ] 815
- [ ] 863
- [ ] 1091 - 双向 BFS
- [ ] 1584

{{< /notice >}}

#### 反推 From opposite / leaf

- 从很轻易判定状态的开始 (edge case), 一层一层 “向内剥”
- _Topological_: 如果是从 leaf 开始, 可以通过`int[] degrees`判断是不是 leaf, 然后加到 queue

低阶
{{< notice question >}}

- [ ] 130
- [ ] 207
- [ ] 210
- [ ] 286
- [ ] 310
- [ ] 317
- [ ] 329
- [ ] 339
- [ ] 364
- [ ] 417
- [ ] 542
- [ ] 934
- [ ] 1162

{{< /notice >}}

---

### Recursion 不常用

```java
bfs(TreeNode root, int index, List<List<Integer>>res)
{
	if (root == null) {
		return ;
	}
	if (res.size() == index) { // 需要开一个新的level
		List<Integer> cur = new ArrayList<>();
		cur.add(root.val);
		res.add(cur);
	} else {
		res.get(index).add(root.val);
	}

	bfs(root.left, index+1, res);
	bfs(root.right, index+1, res);
}
```

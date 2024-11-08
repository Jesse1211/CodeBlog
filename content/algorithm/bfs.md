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

- 从 root 开始, 向下蔓延

低阶
{{< notice question >}}
102, 103, 104, 107, 111, 116, 117, 199, **297**, **314**, 429, 513, 515, 559, **958**, **987**, 1609
{{< /notice >}}

高阶
{{< notice warning >}}
**261**, 449, **1530**
{{< /notice >}}

---

### Matrix, Graph, 无规则 List: 指定点为中心

1. 难点 - 用 Map 或者 list 来重新梳理一下信息
2. 通过题目的信息来用一下 trick 来防重
   - `int[] minCost = new int[n];`
   - `Set<> visited = new HashSet();`
   - Change value when traversing, change back after

#### 正推 From center

- 找到中心, 一层一层“向外剥”

低阶
{{< notice question >}}
**127**, **133**, 200, 279, **301**, 322, **365**, 690, 733, **752**, **863**, **1091**
{{< /notice >}}

高阶
{{< notice warning >}}
**490**, 787, 815, 1584
{{< /notice >}}

{{< notice note >}}

- 127, 1091 可以做双向 BFS

{{< /notice >}}

#### 反推 From opposite / leaf

- 从很轻易判定状态的开始 (edge case), 一层一层 “向内剥”
- _Topological_: 如果是从 leaf 开始, 可以通过`int[] degrees`判断是不是 leaf, 然后加到 queue

低阶
{{< notice question >}}
130, 207, 210, 286, 310, 339, **364**, 417, 542, 1162
{{< /notice >}}

高阶
{{< notice warning >}}
**317**, **329**, **934**
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

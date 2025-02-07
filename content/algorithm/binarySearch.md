+++
authors = ["Jesse"]
title = "Binary Search"
+++

因为 x / 2 永远被 floor, 所以永远都要**从右向左**找

## O(log n)

```JAVA
int low = 1; // min boundry
int high = n; // max boundry
while(low <= high){ // depends
	int mid = low + (high-low)/2;
	if(){
		high = mid...
	}
	else {
		low = mid...
	}
}
```

### Inclusive `while (left <= right)` (精确匹配并可能返回索引)

- **适用场景**：当拿到 mid 的时候, **很清楚** mid 是/不是最终结果
  - 查找并且直接返回符合的元素, 找 specific value,

{{< notice question >}}
33, 74, 81, 162, **367**
{{< /notice >}}

{{< notice warning >}}
**275**, **1539**
{{< /notice >}}

---

### Exclusive `while (left < right)` (在区间中查找边界或条件)

- **适用场景**：找边界值，**不清楚** mid 是/不是最终结果
  - 在区间中查找一个 boundary，上界/下界

{{< notice question >}}
**34**, 35, 69, 153, 154, 278, 540, 852, **875**
{{< /notice >}}

{{< notice warning >}}
154, **528**, **1011**,**1300**, **1802**, 1235, **2422**
{{< /notice >}}

### MID = ?

mid 有两种计算方式, 以及如何搭配更新 left & right

#### 偏左 - `int mid = left + (right - left) / 2;`

- `right = mid` 或者 `right = mid - 1` 搭配使用。
- 因为这里的 mid “偏左”，如果你在判断条件满足后让 right = mid，那本次迭代就会把区间 [left, mid] 继续当作候选区间，不会丢失正确解。
- 这样写可以确保每次循环都能将搜索区间减少至少 1。

#### 偏右 - `int mid = left + (right - left) / 2 + 1;`

// 或者更常见的写法: mid = left + (right - left + 1) / 2;

- `left = mid` 或者 `left = mid + 1` 搭配使用。
- 因为这里的 mid “偏右”，如果判断条件满足后让 left = mid，就不会出现死循环；否则如果用“偏左”的 mid 再写 left = mid，可能导致 left 不变，进而死循环。
- 同理，这样可以保证区间同样向右侧或左侧收缩至少 1。

### 找一个 window 的最左侧

如果每个 element 是 unique, 那直接跳到第二部分 - inside the segment

```JAVA
int left = 0;
int right = arr.size() - k;
while (left < right) {
	int mid = left + (right - left) / 2;
	// 1. outside the segment
	if (arr[mid + k] < x) {
		// x = 3
		// [1,1,2],3,4,5
		left = mid + 1;
	} else if (arr[mid] > x) {
		// x = 1
		// 1,2,[3,4,5]
		right = mid;
	} else {
		// 2. inside the segment
		if (Math.abs(x - arr[mid + k]) < Math.abs(x - arr[mid])) {
			// target距离右边近
			left = mid + 1;
		} else {
			right = mid;
		}
	}
}
```

**272**, **658**

### Binary Search Insertion

**300**

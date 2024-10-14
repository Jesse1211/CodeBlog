+++
authors = ["Jesse"]
title = "Binary Search"
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

## O(log n)

#### Inclusive `while (left <= right)` (精确匹配并可能返回索引)

```java
public int firstBadVersion(int n) {
	int low = 1;
	int high = n;
	while(low<=high){
		int mid = low + (high-low)/2;
		if(isBadVersion(mid)){
			high = mid - 1;
		}
		else {
			low = mid + 1;
		}
	}
	return low;
}
```

- **适用场景**：查找并且直接返回符合的元素
- 需要检查`left == right`的时候. 适用于查找唯一 index 场景
  - 如果完全符合, 直接返回
  - 如果最终无功而返, 返回最后 update 的 low - round up. 因为这时 low > high
- **更新方法**： `left = mid + 1; right = mid - 1;`

{{< notice question >}}
33, 34, 35, 69, 74, **81**, 275, 528, **1300**
{{< /notice >}}

---

#### Exclusive `while (left < right)` (在区间中查找边界或条件)

```java
	public int peakIndexInMountainArray(int[] arr) {
		int left = 0;
		int right = arr.length - 1;
			while (left < right) {
				int mid = left + (right - left) / 2;
				if (arr[mid] < arr[mid+1]) {
					left = mid + 1;
				}
				else {
					right = mid;
				}
			}
		return right;
	}
```

- 不检查`left == right`
- 在区间中查找一个 boundary，上界/下界。
- **更新方法**：`left = mid 或者 mid + 1; right = mid 或者 mid - 1`
- **适用场景**：需要找到满足某些条件的边界值，如寻找最左侧或最右侧的满足条件的元素。

{{< notice question >}}
154, 162, 278, 540, 852, **1011**
{{< /notice >}}

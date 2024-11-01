+++
authors = ["Jesse"]
title = "Prefix Sum"
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

# 总结

通过预先累积和存储之前的数值，使得之后使用极大地降低区间查询的时间复杂度

- HashMap / Array: 匹配个数
- Preorder: Tree related (1590)
- Sum 和 traverse 分开: 找不是相连的 Subarray,
- Sum 和 traverse 合一起: 相连的

### Sum 和 find 分开

1. 整个 Array 中搜索某个特定 index
   - 两个方向算 Sum, 然后找关联.
2. 找当前 index 之前的关联
   - 一个方向算 Sum

```JAVA
int n = nums.length;
int[] minFromLeft = new int[n];
int[] minFromRight = new int[n];

minFromLeft[0] = nums[0];
minFromRight[n - 1] = nums[n - 1];

for (int i = 1; i < n; i++) {
    minFromLeft[i] = Math.min(minFromLeft[i - 1], nums[i]);
    minFromRight[n - i - 1] = Math.min(minFromRight[n - i], nums[n - i - 1]);
}

int res = Integer.MAX_VALUE;
for (int i = 1; i < n - 1; i ++) {
    int left = minFromLeft[i - 1];
    int right = minFromRight[i + 1];
    int cur = nums[i];
    // 在这里找关联
}
```

{{< notice question >}}
238, **670**, **724**, **1094**, 1590, **2406**, **2874**, **2909**
{{< /notice >}}

### Sum 和 find 同步

```JAVA
int count = 0, currSum = 0;
HashMap<Integer, Integer> h = new HashMap();

for (int num : nums) {
    currSum += num;

    if (currSum == ???)
        count++;

    count += h.getOrDefault(currSum - k, 0);

    h.put(currSum, h.getOrDefault(currSum, 0) + 1);
}
```

{{< notice question >}}
325, 437, 523, 525, 560, 974, 1004, **1109**,
{{< /notice >}}

## 差分

求和的逆运算

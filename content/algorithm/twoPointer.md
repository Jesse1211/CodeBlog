+++
authors = ["Jesse"]
title = "Two Pointer"
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

## O(nlogn) OR O(nlogn)

##### 两个 list, 分别各有一个指针

低阶
{{< notice question >}}
349, 392, 408, 455, 524
{{< /notice >}}

高阶
{{< notice warning >}}
826, 986, 1570
{{< /notice >}}

---

##### 同向 - 快慢指针

```bash
0 -> i -> j -> n
```

- i (slow) 左边都是 processed
- j (fast) 左边都是 not needed
- n (length) 左边都是 unknown

- fast 检查 element 是否可以放到 slow 的位置 / 用于 reset 慢指针
- slow 代表 next valid element 要放到的位置 / 用于 reset 快指针

低阶
{{< notice question >}}
26, 27, 31, 121, 283, 350, 443, 3163
{{< /notice >}}

高阶
{{< notice warning >}}
80, 88, 457, 532, 541
{{< /notice >}}

---

##### 相夹 - 左右指针

```bash
0 -> i -- j <- n
```

- i (left) 左边都是 processed
- j (right) 右边都是 processed
- n (length)

低阶
{{< notice question >}}
1, 5, 11, 15, 16, 18, 75, 125, 167, 344, 345, 680
{{< /notice >}}

高阶
{{< notice warning >}}
42
{{< /notice >}}

---

##### Sliding Window

```JAVA
int left = 0, right = 0;

while (right < nums.size()) {
    // 增大窗口
    window.addLast(nums[right]);
    right++;

    while (window needs shrink) {
        // 缩小窗口
        window.removeFirst(nums[left]);
        left++;
    }
}
```

- 灵魂拷问
  1、什么时候应该扩大窗口?
  2、什么时候应该缩小窗口?
  3、什么时候应该更新答案?
- 需要 DataStructure 保存当前 window 信息 (有时候是 frequency), 通过判定 fast 对应的 element 来更改 left
- Non-fixed window trick
  - 不需要每次 slide 都要 shrink 找所有情况
  - `res += right - left + 1;`

```bash
fixed window size
while () {
	1. 加入fast, 删除slow
	2. 检查window是否valid
	3. 更新fast, slow指针
}
```

```bash
Non-fixed window size
while () {
	1. 进行一次fast检查
	2. expand: 加入fast之后, 更新window信息
	3. 检查是否需要shrink
	4. 更新fast指针
}
```

低阶
{{< notice question >}}
19, 28, 219, 438, 567, 643, 713, 1248, 1343, 1423, 2090
{{< /notice >}}

高阶
{{< notice warning >}}
**76**, **424**, **904**, **930**, **1004**, 1248, 2090
{{< /notice >}}

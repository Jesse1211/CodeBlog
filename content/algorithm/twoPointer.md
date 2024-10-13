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

- 349, 455, 524, **826**, **1570**

---

##### 同向 - 快慢指针

```bash
0 -> i -> j -> n
```

- i (slow) 左边都是 processed
- j (fast) 左边都是 not needed
- n (length) 左边都是 unknown

<!-- 0 $$\overrightarrow{\rm (processed)}$$ i $$\overrightarrow{\rm \text{(not needed)}}$$ j $$\overrightarrow{\rm (unknown)}$$ n -->

- slow 代表 next valid element 要放到的位置 / 用于 reset 快指针
- fast 检查 element 是否可以放到 slow 的位置
- 26, 27, 28, **80**, **88**, 121, 283, 50, 532, 541

---

##### 相夹 - 左右指针

```bash
0 -> i -- j <- n
```

- i (left) 左边都是 processed
- j (right) 右边都是 processed
- n (length)
<!-- 0 $$\overrightarrow{\rm processed}$$ i $$\overline{\rm \text{unknown}}$$ j $$\overleftarrow{\rm processed}$$ n -->

- 1, 11, 15, 16, 18, **42**, **75**, 125, 167, 344, 345, 680

---

##### Sliding Window

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

- 需要 DataStructure 保存当前 window 信息 (有时候是 frequency), 通过判定 fast 对应的 element 来更改 left
- Fixed window
  - 219, 438, 567, 643, 1343
- Non-fixed window
  - 算次数 trick
    - 不需要每次 slide 都要 shrink 找所有情况
    - `res += right - left + 1;`
  - **424**, **713**, **904**, **930**, **1004**, 1248

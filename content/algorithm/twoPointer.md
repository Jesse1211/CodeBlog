+++
authors = ["Jesse"]
title = "Two Pointer"
+++

## O(nlogn) OR O(nlogn)

### 两个 list, 分别各有一个指针

- Loop 一个 list, 每个 element 和另一个 list 的 2 pointer 合作
- 多刷, 目前没发总结这东西

{{< notice question >}}

408
524
826
986
1570

{{< /notice >}}

---

### 同向 - 快慢指针

```text
0 -> i -> j -> n

- i = slow, [0, i] = processed
- j = fast, [i, j] = not needed
- n = length, [j, n] = unknown

n -> i -> j -> 0 (指针不一定要从 0 出发, 也能从 n-1 出发)
```

```java
slow = ?? // 储存数据
fast = ?? // 阅读数据
while () {
  if (...) {
    fast++; // append
  } else {
    ... // create a new window (不存在shirnk)
    slow++;
    fast++;
  }
}
```

{{< notice question >}}

⭐️ 入门

80
88
121

⭐️⭐️⭐️ 需要找规律

31 - Permutation 找到规律暴力解
443 - 高阶 3163
457 - circular
3163 - 用 sb.append 也类似像是一个 pointer

{{< /notice >}}

---

#### 高阶同向: Sliding Window

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

1. 扩大窗口
2. 缩小窗口
3. 更新答案

- DataStructure 保存 window 信息
  - (有时候是 frequency), 通过判定 fast 对应的 element 来更改 left
- Non-fixed window trick
  - 不需要每次 slide 都要 shrink 找所有情况
  - `res += right - left + 1;`

```bash
fixed window size
while () {
	1. add fast, delete slow
	2. if window is valid
	3. fast = ...; slow = ...;
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

{{< notice question >}}

fixed:

non-fixed:

3
28
76
219
438
424
532
567
713
904
930
1004
1052
1343
1423
1658
2090

另类 sliding window:

621
2365

{{< /notice>}}

---

### 相夹 - 左右指针

```text
0 -> i -- j <- n
- i = left [0, i]: processed
- j = right [j, n]: processed
- n = length, [i, j]: unknown
```

```java
while (... <= right) { // could be i OR left
  if (...) {
    ...
    left++;
  }

  if (...) {
    ...
    right--;
  }

  if (...) {
    ...
  }
}
```

{{< notice question >}}

⭐️ 基础

42
167
680

⭐️⭐️⭐️⭐️ LR 双指针 + index 指针

75
259
611
881
923

{{< /notice >}}

---

+++
authors = ["Jesse"]
title = "Two Pointer"
+++

## O(nlogn) OR O(nlogn)

##### 两个 list, 分别各有一个指针

低阶
{{< notice question >}}
349, 350, 392, 408, 455, 524
{{< /notice >}}

高阶
{{< notice warning >}}
**475**, 826, 986, 1570
{{< /notice >}}

---

##### 同向 - 快慢指针

```bash
0 -> i -> j -> n
```

- i (slow) 左边都是 processed`
- j (fast) 左边都是 not needed
- n (length) 左边都是 unknown

第一步: 判断 slow & fast 他们应该代表什么

第二部: loop:

- fast 什么时候要+1
- 检查 slow 和 fast 的关系

低阶
{{< notice question >}}
26, 27, 31, 88, 121, 283, 443, 3163
{{< /notice >}}

高阶
{{< notice warning >}}
80, **457**, 1004
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
75, 125, 167, 541, 611, 680, **881**
{{< /notice >}}

高阶
{{< notice warning >}}
42, 259, **923**
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
3, 28, **219**, 438, 567, 713, 930, 1343, 1423, 1658
{{< /notice >}}

高阶
{{< notice warning >}}
76, **424**, **532**, 904, **1052**, **2090**
{{< /notice >}}

# Cheats

#### 找 interval intersections

```JAVA
int newStart = Math.max(leftStart, rightStart);
int newEnd = Math.min(leftEnd, rightEnd);
// there is overlapped
if (newStart <= newEnd) {
    list.add(new int[] { newStart, newEnd });
}
```

#### 找 window sum 等于 x

重点: res += 当前 window 所有数值

```JAVA
public int numSubarraysWithSum(int[] nums, int goal) {
    return findAll(nums, goal) - findAll(nums, goal - 1);
}

private int findAll(int[] nums, int goal) {
    int left = 0;
    int right = 0;
    int res = 0;
    int cur = 0;
    while (right < nums.length) {
        cur += nums[right];

        while (cur > goal && left <= right) {
            cur -= nums[left];
            left++;
        }

        int window = right - left + 1; // 加上window里面所有情况
        res += window;
        right++;
    }
    return res;
}
```

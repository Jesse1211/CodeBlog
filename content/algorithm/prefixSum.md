+++
authors = ["Jesse"]
title = "Prefix Sum"
+++

# 总结

通过预先累积和存储之前的数值，使得之后使用极大地降低区间查询的时间复杂度

- HashMap / Array: 匹配个数

{{< notice note >}}
2237: 建立 hashmap 的时候, 要考虑好右边 index 的信息, 因为右边一般是要-1, 但是要 index+1
2021: 考虑好 edge case, prefix 如果不是 Array, 那么 list 该如何 sort 要想全面
{{< /notice >}}

### Sum 和 find 分开 - 找不相连的 Subarray

1. 整个 Array 中搜索某个特定 index
   - 两个方向算 Sum, 然后找关联.
2. 找当前 index 之前的关联
   - 一个方向算 Sum

```java
int[] count = new int[n];

for (int[] light : lights) {
    int left = Math.max(0, light[0] - light[1]);
    int right = Math.min(n - 1, light[0] + light[1]);
    count[left]++;

    if (right < n - 1) {
        // -1是放在最右边能照到的位置+1, prefix经典考点
        count[right + 1]--;
    }
}
```

低阶
{{< notice question >}}
724, 2021, 2237
{{< /notice >}}

高阶
{{< notice warning >}}
1094, 2406, 2874, 2909
{{< /notice >}}

### Sum 和 find 同步 - 找相连的 Subarray

```JAVA
int sum = 0;
HashMap<Integer, Integer> map = new HashMap();

for (int num : nums) {
    sum += num;

    if (map.containsKey(sum)) {
        ...
        // 重点:
        // 1. res + 1
        // 2. res + map.get(sum)
        // 3. res + curIndex - map.get(sum)
    } else {
        ...
    }
}
```

低阶
{{< notice question >}}
325, 523, **525**, 560, 974, 1109
{{< /notice >}}

高阶
{{< notice warning >}}
1590
{{< /notice >}}

### 益智

238, 670

# Cheat

## Intervals

两种方式

1. 找 min & max 做 array
2. treeMap, 它会自动 sort - log n

````JAVA
Map<Integer, Integer> map = new TreeMap<>(); // time : count

for (int[] i : intervals) {
    int left = i[0];
    int right = i[1];
    map.put(left, map.getOrDefault(left, 0) + 1);
    map.put(right + 1, map.getOrDefault(right + 1, 0) - 1);
}

int count = 0;
int res = 0;
for (int i : map.values()) {
    count += i;
    res = Math.max(count, res);
}
```
````

## 差分 - 反向寻找

1590 - 求和的逆运算

找那个不要的部分的 window

**在 map 查找的时候, 找的 window 不是完美 split 的, 要找和 total % p 一样关联的**

```JAVA
// 找最小的window, windowSum mod p = totalSum mod p
int total = 0;
for (int num : nums) {
    total += num;
    total %= p;
}

if (total == 0) {
    return 0;
}

int sum = 0; // the window's sum which to be removed
int res = nums.length;
Map<Integer, Integer> map = new HashMap<>();
map.put(0, -1);

for (int i = 0; i < nums.length; i++) {
    sum = (sum + nums[i]) % p;

    int needed = (sum - total + p) % p; // 这个window的mod和total要符合, 而不是找mod 0的

    if (map.containsKey(needed)) {
        res = Math.min(res, i - map.get(needed));
    }

    map.put(sum, i);
}

return res == nums.length ? -1 : res;

```

## 找出最大的 x y z 组合

拿到左边最大的值 - x
拿到右边最大的值 - y
traverse 每一个 index - z

```JAVA
int n = nums.length;
int[] minFromLeft = new int[n];
int[] minFromRight = new int[n];

minFromLeft[0] = nums[0];
minFromRight[n - 1] = nums[n - 1];

for (int i = 1; i < n; i++) {
    minFromLeft[i] = Math.max(minFromLeft[i - 1], nums[i]);
    minFromRight[n - i - 1] = Math.max(minFromRight[n - i], nums[n - i - 1]);
}

int res = Integer.MAX_VALUE;
for (int i = 1; i < n - 1; i ++) {
    int left = minFromLeft[i - 1];
    int right = minFromRight[i + 1];
    int cur = nums[i];
    // 在这里找关联
}
```

+++
authors = ["Jesse"]
title = "Prefix Sum"
+++

通过预先累积和存储之前的数值，使得之后使用极大地降低区间查询的时间复杂度

### Used Data Structures

- `{value: count}`

#### Array / List

```java
n = right - left + 1;

int[] sum = new int[n]; // inclusive count
int[] sum = new int[n + 1]; // exclusive count, 比如路灯问题

```

```java
// a - b: increase
// b - a: decrease
Collections.sort(new ArrayList<>(), (a, b) -> a[0] != b[0] ? a[0] - b[0] : a[1] - b[1]);

Arrays.sort(new int[], (a, b) -> a - b);
```

- Value

```java
int[] sums = new int[n];

// 额外解决index 0
sums[0] = ...

// loop for the rests from 1
for (int i = 1; i < n; i++) {
    sums[i] = sums[i-1] + nums[i];
}
```

#### Hash Map

注意 base case, 比如 `map.put(0, 某个值)`

### Sum 和 find 分开 - 找不相连的 Subarray

1. 整个 Array 中搜索某个特定 index
   - 两个方向算 Sum, 然后找关联.
2. 找当前 index 之前的关联
   - 一个方向算 Sum

```java
int[] count = new int[n];

for (int[] light : lights) {
    int left = ...;
    int right = ...;
    count[left]++;
    count[right]--;
}

int cur = 0;
int res = 0;

for (int c : count) {
    cur += c;
    res = Math.max(res, cur);
}

return res;
```

{{< notice note >}}

⭐️ 基础

724 - 2 list
1094 - map
2021 - sort array list
2237 - list

⭐️⭐️ Groups - res = 最多 count 的 prefix

2406

⭐️⭐️⭐️ Triplets - 需要 2 lists (2 个 int) + 一次 traverse (1 个 int)

2874
2909 - 和 2874 一样

{{< /notice >}}

### Sum 和 find 同步 - 找相连的 Subarray

```JAVA
int sum = 0;
HashMap<Integer, Integer> map = new HashMap();
map.put(0, -1);

for (int num : nums) {
    sum += num;
    mapKey = sum...;

    // 检查subarray是否存在
    if (map.containsKey(mapKey)) {
        // res...
        // ...
    }

    // 是否更新map
    if (!map.containsKey(sum)) {
        // map.put...
    }
}
```

{{< notice question >}}

⭐️ 入门 - map, res = Math.max(...)

325
523
1109 - list

⭐️⭐️⭐️ ❤️ sum 和 value 关系不直接

525 - 特定某个 value 对 sum 是加/减
1590 - 通过 sum 求出 map.key

⭐️⭐️⭐️ count 所有组合 - res += ...

560 - map
974 - map

⭐️⭐️⭐️⭐️ 益智 but 常考

238
670
{{< /notice >}}

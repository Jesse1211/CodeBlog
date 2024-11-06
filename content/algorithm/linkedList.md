+++
authors = ["Jesse"]
title = "Linked List"
+++

# Linked List:

**707**

{{< notice warning >}}
**143**, **147**, **287**, **148**, **430**
{{< /notice >}}

## 反转

```JAVA
public ListNode reverseList(ListNode cur) {
  ListNode prev = null;
  while (cur != null) {
      // step1: save cur.next node & set cur.next as prev
      ListNode after = cur.next;
      cur.next = prev;
      // step2: update prev as cur & update cur to saved node
      prev = cur;
      cur = after;
  }
  return prev;
}
public ListNode reverseList(ListNode head) {
    if (head == null || head.next == null) {
        return head;
    }
    ListNode p = reverseList(head.next);
    head.next.next = head;
    head.next = null;
    return p;
}
```

## 操作一个链表

### 借助其他 data structure 存储信息

{{< notice question >}}
138
{{< /notice >}}

### 反转系列

{{< notice question >}}
**92**, **206**, **234**
{{< /notice >}}

### Sliding Window

{{< notice question >}}
19, 61,
{{< /notice >}}

### 双指针

{{< notice question >}}
82, 86, 141, 142, 328, **2807**
{{< /notice >}}

## 操作两个链表

{{< notice question >}}
**2**, 21, **23**, 160
{{< /notice >}}

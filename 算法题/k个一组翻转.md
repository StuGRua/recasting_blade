- 思路就是从头前面一个开始寻找第k个元素，一个一个往他屁股后面插，插k-1次即可继续迭代。
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseKGroup(self, head: ListNode, k: int) -> ListNode:

        top = ListNode(next=head)
        left = right = top

        while True:
            for _ in range(k):
                right = right.next
                if not right:
                    return top.next
            next_left = left.next
            for _ in range(k-1):
                left.next, right.next, right.next.next = left.next.next, left.next, right.next
            left = right = next_left

```

```python
# 基本的链表滚动赋值，通过设置pre和cur和临时tmp三个指针，进行指针交替滚动，完成翻转
class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        cur,pre = head,None
        while cur:
            tmp = cur.next
            cur.next = pre
            pre = cur
            cur = tmp
        return pre

```
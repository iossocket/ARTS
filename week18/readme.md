### ARTS

#### Algorithm
##### Remove Duplicates from Sorted List II

Given a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list.

Return the linked list sorted as well.

**Example 1:**
```
Input: 1->2->3->3->4->4->5
Output: 1->2->5
```
**Example 2:**
```
Input: 1->1->1->2->3
Output: 2->3
```

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        ListNode dummy = new ListNode(-1);
        dummy.next = head;

        ListNode current = head;
        ListNode prev = dummy;

        while (current != null && current.next != null) {
            if (current.val == current.next.val) {
                int val = current.val;
                while (current != null && current.val == val) {
                    current = current.next;
                }
                prev.next = current;
            } else {
                prev = current;
                current = current.next;
            }
        }

        return dummy.next;
    }
}
```

#### Review
原文链接：[Secret Management on iOS](https://nshipster.com/secrets/)

Matt大神总结了一些常见的存储credentials的反模式，例如，直接写在code里，使用Configuration file或Info.plist。
代码混淆，可以认为是一种较为有效的防护手段，但同时也强调任何存储在client端的credentials都是不安全的，应该尽可能的将重要数据移至后端。

#### Tips

[React Native 拆包实践 番外篇 - 更改index.js路径](https://www.jianshu.com/p/6501c491b1ef)
[React Native 拆包实践5 - 按需加载js module](https://www.jianshu.com/p/832d7c01b101)

#### Sharing

[Nginx 学习总结](https://www.jianshu.com/p/0b0bd2982a79)
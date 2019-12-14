### ARTS

#### Algorithm

Given a linked list, remove the n-th node from the end of list and return its head.

Example:
```
Given linked list: 1->2->3->4->5, and n = 2.
```
After removing the second node from the end, the linked list becomes 1->2->3->5.
Note:

Given n will always be valid.

Follow up:

Could you do this in one pass?


```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode sentry = new ListNode(0);
        ListNode preHead = sentry;
        preHead.next = head;

        ListNode fast = head;
        ListNode slow = head;
        ListNode preSlow = preHead;

        while (n > 0) {
            fast = fast.next;
            n--;
        }
        while (fast != null) {
            fast = fast.next;
            slow = slow.next;
            preSlow = preSlow.next;
        }

        preSlow.next = slow.next;
        slow.next = null;

        return sentry.next;
    }
}
```

#### Review

***SwiftUI by Tutorials*** raywenderlich 发布的一本英文电子书，学习一下SwiftUI的子视图布局：
[SwiftUI - Stack布局详解（1）](https://www.jianshu.com/p/c3346a5cc8b1)

#### Tips



#### Sharing

开始重新学backend，开始写一个系列文章：


### ARTS

#### Algorithm

Given a linked list, determine if it has a cycle in it.

To represent a cycle in the given linked list, we use an integer pos which represents the position (0-indexed) in the linked list where tail connects to. If pos is -1, then there is no cycle in the linked list.

Example:
```
Input: head = [3,2,0,-4], pos = 1
Output: true
Explanation: There is a cycle in the linked list, where tail connects to the second node.
```

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
public class Solution {
    // 使用Set
    public boolean hasCycle(ListNode head) {
        HashSet<ListNode> set = new HashSet<ListNode>();
        ListNode current = head;
        while (current != null) {
            if (set.contains(current)) {
                return true;
            }
            set.add(current);
            current = current.next;
        }
        return false;
    }
    // 使用快慢指针
    public boolean hasCycle(ListNode head) {
        ListNode fast = head;
        ListNode slow = head;

        while (fast != null && fast.next != null && fast.next.next != null) {
            slow = slow.next;
            fast = fast.next.next;
            if (slow == fast) {
                return true;
            }
        }
        return false;
    }
}
```

#### Review

***SwiftUI by Tutorials*** raywenderlich 发布的一本英文电子书
继续上一周的内容，这周看了本书Chapter 7: State & Data Flow, 对State多理解了一些，更新了之前的一篇文章:[link](https://www.jianshu.com/p/a2a69fb070b0)

#### Tips


#### Sharing

开始重新学backend，开始写一个系列文章：

1. 第四篇[cookie](https://www.jianshu.com/p/740b29bbb0ca)
2. 第五篇[log](https://www.jianshu.com/p/b0c983fa96b8)

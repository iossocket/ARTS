### ARTS

#### Algorithm

Reverse a singly linked list.

Follow up:
A linked list can be reversed either iteratively or recursively. Could you implement both?

Example:
```
Input: 1->2->3->4->5->NULL
Output: 5->4->3->2->1->NULL
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
    public ListNode reverseList(ListNode head) {
        ListNode pre = null;
        ListNode cur = head;

        while (cur != null) {
            ListNode tmp = cur.next;
            cur.next = pre;
            pre = cur;
            cur = tmp;
        }

        return pre;
    }
}
```

#### Review

***SwiftUI by Tutorials*** raywenderlich 发布的一本英文电子书
继续上一周的内容，这次来介绍如何SwiftUI写一个Watch App的页面，并且和iOS复用:[link](https://www.jianshu.com/p/9c42a2423997)

#### Tips

mybatis-genenerator的使用

[link](https://www.jianshu.com/p/4208c7f390ce)

#### Sharing

开始重新学backend，开始写一个系列文章：

1. 第二篇[配置数据库](https://www.jianshu.com/p/05f50442cbb6)
2. 第三篇[运行SpringBoot](https://www.jianshu.com/p/42a22bc09723)

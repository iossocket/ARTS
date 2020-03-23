### ARTS

#### Algorithm
##### Remove Duplicates from Sorted List

Given a sorted linked list, delete all duplicates such that each element appear only once.

**Example 1:**
```
Input: 1->1->2
Output: 1->2
```
**Example 2:**
```
Input: 1->1->2->3->3
Output: 1->2->3
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
        if (head == null) {
            return null;
        }
        ListNode cur = head;
        ListNode next = head.next;

        while (next != null) {
            if (cur.val != next.val) {
                cur.next = next;
                cur = cur.next;
            }
            next = next.next;
        }

        cur.next = null;

        return head;
    }
}
```

#### Review
由于Keycloak的API都是通过RestEasy来实现的，所以有了这些。网上的相关资料真的是太少了。

原文链接：[resteasy-tutorial](https://www.baeldung.com/resteasy-tutorial)

结合自己的理解总结：[RestEasy Get Started](https://www.jianshu.com/p/4a4ff98bef0e)

#### Tips

[React Native 拆包实践4 - createModuleIdFactory](https://www.jianshu.com/p/717f4cb7e682)

#### Sharing

开始重新学backend，开始写一个系列文章：

Keycloak的第十篇 [配置Postgres数据库](https://www.jianshu.com/p/2c3406e0a301)
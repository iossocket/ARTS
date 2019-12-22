### ARTS

#### Algorithm

Middle of the Linked List
Given a non-empty, singly linked list with head node head, return a middle node of linked list.

If there are two middle nodes, return the second middle node.

Example 1:
```
Input: [1,2,3,4,5]
Output: Node 3 from this list (Serialization: [3,4,5])
The returned node has value 3.  (The judge's serialization of this node is [3,4,5]).
Note that we returned a ListNode object ans, such that:
ans.val = 3, ans.next.val = 4, ans.next.next.val = 5, and ans.next.next.next = NULL.
```

Example 2:
```
Input: [1,2,3,4,5,6]
Output: Node 4 from this list (Serialization: [4,5,6])
Since the list has two middle nodes with values 3 and 4, we return the second one.
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
class Solution {
    public ListNode middleNode(ListNode head) {
        ListNode fast = head;
        ListNode slow = head;

        while (fast!= null && fast.next != null) {
            fast = fast.next.next;
            slow = slow.next;
        }
        return slow;
    }
}
```

#### Review

***SwiftUI by Tutorials*** raywenderlich 发布的一本英文电子书，学习一下SwiftUI的子视图布局：
[SwiftUI - Stack布局详解（2）](https://www.jianshu.com/p/14c35a3592f6)

#### Tips

1. 在react native的native module下开启一个Timer
若没有指定当前native moduel的运行线程，默认使用的是facebook开启的线程，这时创建timer是无法执行的，即使将这个timer添加到当前runloop中也无法执行。解决方式有两种：

a. 指定当前的native module运行在主线程

```
- (dispatch_queue_t)methodQueue {
  return dispatch_get_main_queue();
}
```

b. 启动timer时，将构造函数的执行切换到主线程

2. [BUCK - 使用BUCK编译iOS项目(2)](https://www.jianshu.com/p/3425866e9847)

3. [x-www-form-urlencoded & form-data](https://www.jianshu.com/p/51f954e077b3)

#### Sharing

开始重新学backend，开始写一个系列文章：

[通过postman从keycloak server获取token](https://www.jianshu.com/p/e12e3cf6d35b)
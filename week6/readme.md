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

#### mongo 开发环境配置

```
下载mongo镜像
docker pull mongo

运行mongo
run --name mongo -p 27017:27017 -v ~/docker-data/mongo:/data/db -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=admin -d mongo
-e: 设置环境变量
-d: 后台运行
-p: 端口映射
-v: 挂载存储空间
--name: 指定运行后container的名字
最后的mongo指的是image的名字


登录docker的bash
docker exec -it mongo bash

通过shell连接mongo
mongo -u admin -p admin

创建库
use springbucks

创建用户
db.createUser(
    {
      user: "springbucks",
      pwd: "springbucks",
      roles: [
         { role: "readWrite", db: "springbucks" }
      ]
})

查看所有集合
show collections

db.coffee.find()
db.coffee.remove({"name": "espresso"})
```
#### redis 开发环境配置
```
docker pull redis
docker run --name redis -d -p 6379:6379 redis

docker exec -it redis bash
redis-cli
HGETALL "springbucks-menu"
```

#### Sharing

开始重新学backend，开始写一个系列文章：

1. 第四篇[cookie](https://www.jianshu.com/p/740b29bbb0ca)
2. 第五篇[log](https://www.jianshu.com/p/b0c983fa96b8)

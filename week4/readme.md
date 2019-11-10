### ARTS

#### Algorithm

Design and implement a data structure for Least Recently Used (LRU) cache. It should support the following operations: get and put.

get(key) - Get the value (will always be positive) of the key if the key exists in the cache, otherwise return -1.
put(key, value) - Set or insert the value if the key is not already present. When the cache reached its capacity, it should invalidate the least recently used item before inserting a new item.

The cache is initialized with a positive capacity.

Follow up:
Could you do both operations in O(1) time complexity?

Example:
```
LRUCache cache = new LRUCache( 2 /* capacity */ );

cache.put(1, 1);
cache.put(2, 2);
cache.get(1);       // returns 1
cache.put(3, 3);    // evicts key 2
cache.get(2);       // returns -1 (not found)
cache.put(4, 4);    // evicts key 1
cache.get(1);       // returns -1 (not found)
cache.get(3);       // returns 3
cache.get(4);       // returns 4
```

> 解题思路：使用一个双向链表来存储顺序，一个字典来检查是否存在该元素。使用双向链表是因为可以加快删除指定元素的速度，不需要再遍历链表。
> 题目中有一点没有说清楚，当put一个存在的key时，应该更新value值，同时改变它在链表中的位置。

```swift
class Node {
    private let key: Int
    private var value: Int
    var nextNode: Node?
    var preNode: Node?
    
    init(key: Int, value: Int) {
        self.key = key
        self.value = value
    }
    
    func getValue() -> Int {
        return value
    }
    
    func setValue(_ value: Int) {
        self.value = value
    }
    
    func getKey() -> Int {
        return key
    }
}

class LinkedList {

    private var head: Node?
    private var tail: Node?
    
    init() {}
    
    func addAtHead(_ node: Node) {
        guard let head = self.head else {
            self.head = node
            self.tail = node
            return
        }
        node.nextNode = head
        head.preNode = node
        self.head = node
    }
    
    func deleteTail() -> Node? {
        guard let tail = tail else {
            return nil
        }
        
        self.tail = tail.preNode
        self.tail?.nextNode = nil
        return tail
    }
    
    func deleteNode(_ node: Node) {
        guard let head = self.head, let tail = self.tail else {
            return
        }
        
        if node.getKey() == head.getKey() {
            self.head = self.head?.nextNode
            self.head?.preNode = nil
            return
        }
        
        if node.getKey() == tail.getKey() {
            self.tail = self.tail?.preNode
            self.tail?.nextNode = nil
            return
        }
        
        node.preNode?.nextNode = node.nextNode
        node.nextNode?.preNode = node.preNode
        node.preNode = nil
        node.nextNode = nil
    }
}

class LRUCache {

    private let capacity: Int
    private let list: LinkedList
    private var dict: [Int: Node]
    
    init(_ capacity: Int) {
        self.capacity = capacity
        self.list = LinkedList()
        self.dict = [Int: Node]()
    }
    
    func get(_ key: Int) -> Int {
        guard let node = dict[key] else {
            return -1
        }
        list.deleteNode(node)
        list.addAtHead(node)
        return node.getValue()
    }
    
    func put(_ key: Int, _ value: Int) {
        if let node = dict[key] {
            node.setValue(value)
            list.deleteNode(node)
            list.addAtHead(node)
            return
        }
        
        let node = Node(key: key, value: value)
        dict[key] = node
        list.addAtHead(node)
        if dict.keys.count <= capacity {
            return
        }
        if let tail = list.deleteTail() {
            dict.removeValue(forKey: tail.getKey())
        }
    }
}
```

#### Review

***SwiftUI by Tutorials*** raywenderlich 发布的一本英文电子书
继续上一周的内容，这次来介绍如何将SwiftUI集成到已有项目中:[link](https://www.jianshu.com/p/fbc920c11b0d)

#### Tips

数据库相关的两个工具 Navicat 和 PDMan

[link](https://www.jianshu.com/p/5a85e1a26250)

#### Sharing

开始重新学backend，开始写一个系列文章，第一篇[工程构建](https://www.jianshu.com/p/f1d19982912d)

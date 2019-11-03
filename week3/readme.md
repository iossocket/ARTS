### ARTS

#### Algorithm

这次用双向列表实现一个
Design Linked List
Design your implementation of the linked list. You can choose to use the singly linked list or the doubly linked list. A node in a singly linked list should have two attributes: val and next. val is the value of the current node, and next is a pointer/reference to the next node. If you want to use the doubly linked list, you will need one more attribute prev to indicate the previous node in the linked list. Assume all nodes in the linked list are 0-indexed.

Implement these functions in your linked list class:

1. get(index) : Get the value of the index-th node in the linked list. If the index is invalid, return -1.
2. addAtHead(val) : Add a node of value val before the first element of the linked list. After the insertion, the new node will be the first node of the linked list.
3. addAtTail(val) : Append a node of value val to the last element of the linked list.
4. addAtIndex(index, val) : Add a node of value val before the index-th node in the linked list. If index equals to the length of linked list, the node will be appended to the end of linked list. If index is greater than the length, the node will not be inserted. If index is negative, the node will be inserted at the head of the list.
5. deleteAtIndex(index) : Delete the index-th node in the linked list, if the index is valid.

```swift
class Node {
    private let value: Int
    var nextNode: Node?
    var preNode: Node?
    
    init(value: Int) {
        self.value = value
    }
    
    func getValue() -> Int {
        return value
    }
}

class MyLinkedList {

    var count: Int = 0
    private var head: Node?
    private var tail: Node?
    
    /** Initialize your data structure here. */
    init() {}
    
    /** Get the value of the index-th node in the linked list. If the index is invalid, return -1. */
    func get(_ index: Int) -> Int {
        if count == 0 || index >= count || index < 0 {
            return -1
        }
        guard let head = self.head else {
            return -1
        }
        
        var currentIndex = 0
        var currentNode: Node? = head
        while index != currentIndex {
            currentIndex += 1
            currentNode = currentNode?.nextNode
        }
        return currentNode == nil ? -1 : currentNode!.getValue()
    }
    
    /** Add a node of value val before the first element of the linked list. After the insertion, the new node will be the first node of the linked list. */
    func addAtHead(_ val: Int) {
        count += 1
        let newHead = Node(value: val)
        guard let head = self.head else {
            self.head = newHead
            self.tail = newHead
            return
        }
        newHead.nextNode = head
        head.preNode = newHead
        self.head = newHead
    }
    
    /** Append a node of value val to the last element of the linked list. */
    func addAtTail(_ val: Int) {
        count += 1
        let newTail = Node(value: val)
        guard let tail = self.tail else {
            self.head = newTail
            self.tail = newTail
            return
        }
        tail.nextNode = newTail
        newTail.preNode = tail
        self.tail = newTail
    }
    
    /** Add a node of value val before the index-th node in the linked list. If index equals to the length of linked list, the node will be appended to the end of linked list. If index is greater than the length, the node will not be inserted. */
    func addAtIndex(_ index: Int, _ val: Int) {
        if index > count {
            return
        }
        
        if index <= 0 {
            addAtHead(val)
            return
        }
        
        if index == count {
            addAtTail(val)
            return
        }
        
        var currentNode = head
        var currentIndex = 0
        while currentIndex != index - 1 {
            currentNode = currentNode?.nextNode
            currentIndex += 1
        }
        
        count += 1
        let newNode = Node(value: val)
        
        newNode.nextNode = currentNode?.nextNode
        newNode.preNode = currentNode
        currentNode?.nextNode?.preNode = newNode
        currentNode?.nextNode = newNode
        
    }
    
    /** Delete the index-th node in the linked list, if the index is valid. */
    func deleteAtIndex(_ index: Int) {
        if index < 0 || index > count - 1 {
            return
        }
        
        if index == 0 {
            count -= 1
            head = head?.nextNode
            head?.preNode?.nextNode = nil
            head?.preNode = nil
            return
        }
        
        if index == count - 1 {
            count -= 1
            tail = tail?.preNode
            tail?.nextNode?.preNode = nil
            tail?.nextNode = nil
            return
        }
        
        count -= 1
        var currentNode = head
        var currentIndex = 0
        while currentIndex != index {
            currentIndex += 1
            currentNode = currentNode?.nextNode
        }
        
        currentNode?.preNode?.nextNode = currentNode?.nextNode
        currentNode?.nextNode?.preNode = currentNode?.preNode
        currentNode?.preNode = nil
        currentNode?.nextNode = nil
    }
    
    func printList() -> String {
        if count == 0 {
            return ""
        }
        
        var currentIndex = 0
        var currentNode = head
        var result = ""
        while currentNode?.nextNode != nil {
            result += "\(currentNode!.getValue()) -> "
            currentNode = currentNode?.nextNode
            currentIndex += 1
        }
        result += "\(currentNode!.getValue())"
        return result
    }
    
    func getCount() -> Int {
        return count
    }
}
```

#### Review

***SwiftUI by Tutorials*** raywenderlich 发布的一本英文电子书
继续上一周的内容，这次来聊聊数据的绑定

[链接](https://www.jianshu.com/p/a2a69fb070b0)

#### Tips

将RN作为Framework引入需要的Scripts

[链接]()

#### Sharing

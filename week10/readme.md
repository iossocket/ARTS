### ARTS

#### Algorithm

##### Min Stack

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

* push(x) -- Push element x onto stack.
* pop() -- Removes the element on top of the stack.
* top() -- Get the top element.
* getMin() -- Retrieve the minimum element in the stack.

Example:
```
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> Returns -3.
minStack.pop();
minStack.top();      --> Returns 0.
minStack.getMin();   --> Returns -2.
```

```java
import java.util.EmptyStackException;
import java.util.Stack;

class MinStack {
    private Stack<Integer> miniStack;
    private Stack<Integer> realStack;

    public MinStack() {
        miniStack = new Stack<>();
        realStack = new Stack<>();
    }

    public void push(int x) {
        realStack.push(x);
        try {
            Integer miniValue = miniStack.peek();
            if (miniValue <= x) {
                miniStack.push(miniValue);
            } else {
                miniStack.push(x);
            }
        } catch (EmptyStackException e) {
            miniStack.push(x);
        }
    }

    public void pop() {
        try {
            realStack.pop();
            miniStack.pop();
        } catch (EmptyStackException e) { }
    }

    public int top() {
        return realStack.peek();
    }

    public int getMin() {
        return miniStack.peek();
    }
}
```

#### Review

***SwiftUI by Tutorials*** raywenderlich 发布的一本英文电子书

[SwiftUI - Navigation & List](https://www.jianshu.com/p/643ce6cd8345)

#### Tips

本节中我们将使用BUCK来编译一个自定义的library，在此library中使用了Objective-C和C++；之后添加一个二进制的Framework，这里集成的是腾讯的mars日志框架。
[BUCK - 使用BUCK编译iOS项目(3)](https://www.jianshu.com/p/fa2d94283da3)


#### Sharing

开始重新学backend，开始写一个系列文章：

[]()
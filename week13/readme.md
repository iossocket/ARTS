### ARTS

#### Algorithm
##### Sort an Array (Bubble Sort)
Given an array of integers nums, sort the array in ascending order.

Example 1:
```
Input: nums = [5,2,3,1]
Output: [1,2,3,5]
```
Example 2:
```
Input: nums = [5,1,1,2,0,0]
Output: [0,0,1,1,2,5]
```

```java
public class SortArray {
    public List<Integer> sortArray(int[] nums) {
        for (int i = 0; i < nums.length; i++) {
            boolean flag = false;
            for (int j = 0; j < nums.length - i - 1; j++) {
                if (nums[j] > nums[j+1]) {
                    int temp = nums[j];
                    nums[j] = nums[j+1];
                    nums[j+1] = temp;
                    flag = true;
                }
            }
            if (!flag) break;
        }
        List<Integer> list = new ArrayList<>();
        for (int item : nums) {
            list.add(item);
        }
        return list;
    }
}
```

#### Review

***SwiftUI by Tutorials*** raywenderlich 发布的一本英文电子书

[SwiftUI - 图形绘制](https://www.jianshu.com/p/7b4573121e60)

#### Tips

项目中有大量的蓝牙操作，由于蓝牙外设的不稳定性，经常出现无法连接，或指令超时的现象，所以自定义了一个超时方法，方便复用：
```swift
class Timeout {
    private var timer: Timer?
    private var callback: (() -> Void)?
    
    init(_ delaySeconds: Double, _ callback: @escaping () -> Void) {
        self.callback = callback
        self.timer = Timer.scheduledTimer(timeInterval: delaySeconds, target: self, selector: #selector(invoke), userInfo: nil, repeats: false)
    }
    
    @objc private func invoke() {
        DispatchQueue.main.async {
            self.callback?()
            self.callback = nil
            self.timer = nil
        }
    }
    
    func cancel() {
        DispatchQueue.main.async {
            self.timer?.invalidate()
            self.timer = nil
        }
    }
}
```

#### Sharing

开始重新学backend，开始写一个系列文章：

Keycloak的第五篇，[配置OTP](https://www.jianshu.com/p/a4e3b2923b83)
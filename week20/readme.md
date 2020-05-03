### ARTS

#### Algorithm
##### Binary Search

Given a sorted (in ascending order) integer array nums of n elements and a target value, write a function to search target in nums. If target exists, then return its index, otherwise return -1.

**Example:**

```
Input: nums = [-1,0,3,5,9,12], target = 9
Output: 4
Explanation: 9 exists in nums and its index is 4
```

```java
class Solution {
    public int search(int[] nums, int target) {
        int start = 0;
        int end = nums.length - 1;

        while (start <= end) {
            int mid = start + (end - start) / 2;
            if (nums[mid] == target) {
                return mid;
            } else if (nums[mid] > target) {
                end = mid - 1;
            } else {
                start = mid + 1;
            }
        }
        return -1;
    }
}
```

#### Review
原文链接：[Date​Components](https://nshipster.com/datecomponents/)

当使用HealthKit时常常需要计算日期，比如计算本周的开始时间和结束时间，某天的起始时间等等，正确的使用`Date​Components`可以简化我们的计算过程。这篇Matt大神给出了很好的解释。不要再使用：`date.addingTimeInterval(60 * 60 * 24)`这种计算方式了。
引用其中的一句话来说明`Date​Components`都做了什么：

> It’s a relatively recent addition to Foundation for representing a date or duration of time.

1. 当作为date使用时：
```swift
let calendar = Calendar.current
let now = Date()

let dateComponents = DateComponents(calendar: calendar,year: 2020, month: 10, day: 10)
let date = calendar.date(from: dateComponents)!
// 2020-10-10


// 可以获得今天的年月日等一系列数据
calendar.dateComponents([.year, .month, .day, .timeZone, .weekday, .weekdayOrdinal], from: now)

// 获取当月的第一天
var beginningOfMonth: Date?
beginningOfMonth = calendar.dateInterval(of: .month, for: now)!.start

var tomorrow: Date?
tomorrow = calendar.date(byAdding: .day, value: 1, to: now) // equals add 24 hours

// 获取明天的起始时刻
let startOfTmr = calendar.dateComponents([.year, .month, .day], from: tomorrow!)
calendar.date(from: xx)
```

2. 当作为duration使用时
```swift
let calendar = Calendar.current
let now = Date()

// 一个月加一天
let duration = DateComponents(calendar: calendar, year: 0, month: 1, day: 1)
let date = calendar.date(byAdding: duration, to: date)!


// this is a range: 2020-04-30 16:00:00 +0000 to 2020-05-31 16:00:00 +0000
let monthInterval = calendar.dateInterval(of: .month, for: now)!

// 获取本月一个用多少个小时
calendar.dateComponents([.hour], from: monthInterval.start, to: monthInterval.end)
```

#### Tips

pp助手下线后，如何获取ipa文件 => iMazing
https://www.jianshu.com/p/33dceeadf8a1


#### Sharing

[React Native 拆包实践6 - Android 启动流程](https://www.jianshu.com/p/89757051ffe5)
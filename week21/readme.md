### ARTS

#### Algorithm
##### Binary Search

Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You may assume no duplicates in the array.

**Example:**

```
Input: [1,3,5,6], 5
Output: 2
```

```java
class Solution {
    public int searchInsert(int[] nums, int target) {
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
        return start;
    }
}
```

#### Review
原文链接：[Locale](https://nshipster.com/locale/)

有很多方法会涉及到国际化，通常这些方法都有一个optional的参数，可以根据需要传入，如果不传或是传入nil时，它的行为将基于当前用户手机的设置而决定，下面给出了一个例子。类似这样的情况还有很多比如最常见的一周的起始是周一还是周日。

```
import Foundation

let units = ["meter", "smoot", "agate", "ångström"]

units.sorted { (lhs, rhs) in
    lhs.compare(rhs, locale: .current) == .orderedAscending
}
```

再给出一个有用的tips，在HTTP的header中的Accept-Language，通常是被我们忽略掉的，如果有一天我们要支持国际化，再加上这个header就有点晚了，那是就需要强制用户升级才能支持这个特性。
```
import Foundation

let url = URL(string: "https://nshipster.com")!
var request = URLRequest(url: url)

let acceptLanguage = Locale.preferredLanguages.joined(separator: ", ")
request.setValue(acceptLanguage, forHTTPHeaderField: "Accept-Language")
```


#### Tips

这周在RN项目中集成了Charts，这个library可以说是图表界的老大了。集成过程过程中遇到了一个有意思的点，我们的x轴的文字是两行的，`BarChartView`的布局初始化如果放在`init(frame: CGReact)`中，无论使用frame，autoResizing或是autoLayout都只能显示一行，但把chart在x轴的两个尽头处拖动一下，瞬间换为两行。分析之后得知这是Charts布局的问题，它是通过CGContext画出来的。

解决方式：在`init(frame: CGReact)`中仅执行addSubview的操作，而把布局的代码放在`layoutSubviews()`中执行


#### Sharing

分享的第七篇
[React Native 拆包实践7 - Android 按需加载jsbundle](https://www.jianshu.com/p/ce80c2924292)
### ARTS

#### Algorithm
##### Add Two Numbers

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example:**

```
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode result = new ListNode(0);
        ListNode curNode = result;
        int temp = 0;
        while (l1 != null && l2 != null) {
            int cur = l1.val + l2.val + temp;
            temp = cur > 9 ? 1 : 0;
            curNode.next = new ListNode(cur > 9 ? cur - 10 : cur);
            curNode = curNode.next;
            l1 = l1.next;
            l2 = l2.next;
        }

        while (l1 != null) {
            int cur = l1.val + temp;
            temp = cur > 9 ? 1 : 0;
            curNode.next = new ListNode(cur > 9 ? cur - 10 : cur);
            curNode = curNode.next;
            l1 = l1.next;
        }

        while (l2 != null) {
            int cur = l2.val + temp;
            temp = cur > 9 ? 1 : 0;
            curNode.next = new ListNode(cur > 9 ? cur - 10 : cur);
            curNode = curNode.next;
            l2 = l2.next;
        }

        if (temp != 0) {
            curNode.next = new ListNode(1);
        }

        return result.next;
    }
}
```

#### Review
原文链接：[Apple Push Notification Device Tokens](https://nshipster.com/apns-device-tokens/)

当获取到device token后，AppDelegate将触发`didRegisterForRemoteNotificationsWithDeviceToken`方法，传入的参数是一个`Data`类型，而我们需要的是一个string，Swift在解析Data上比较简单：
```
let deviceTokenString = deviceToken.map { String(format: "%02x", $0) }.joined()
```
对Data类型进行map操作，其中每一个element是一个`UInt8`，`%02x`则将这个`UInt8`转换为十六进制输出，`02`是在指明输出两位，若不够两位则前面补零，简单直接。

在Objective-C中要如何操作呢？查阅了一下资料后，最佳方案为：
```
const char *data = [deviceToken bytes];
NSMutableString *tokenStr = [NSMutableString string];
for (int i = 0; i < [deviceToken length]; i++) {
  [tokenStr appendFormat:@"%02.2hhx", data[i]];
}
```
NSData的bytes将得到一个char数组，而我们需要将char进行格式化输出后append到一个NSString里，不容易理解的就是这个格式化输出符`%02.2hhx`。其中`02`和swift相同，`hhx`指明data[i]是一个unsigned char类型（`hx` - unsigned short），`hhx`前面的2指明两位，和`%02`用意上略有相同。可以参考[https://www.yawintutor.com/format-specifiers-in-c/](https://www.yawintutor.com/format-specifiers-in-c/)这篇博客了解`.`的用意。这里给出这篇博客中的一个例子：

```
#include <stdio.h>

int main(int argc, char** argv) {
	char s[] = "YawinTutor"; 
	printf("value actual                : [%s]\n", s); 
	printf("value with number           : [%15s]\n", s); 
	printf("value with minus+number     : [%-15s]\n", s); 
	printf("value with number+dot       : [%15.5s]\n", s); 
	printf("value with minus+number+dot : [%-15.5s]\n", s); 

	printf("value with dot              : [%.5s]\n", s); 
	printf("value with minus            : [%-s]\n", s); 
	printf("value with minus+dot        : [%-.5s]\n", s); 
	return 0;
}
```

Output
```
value actual                : [YawinTutor]
value with number           : [     YawinTutor]
value with minus+number     : [YawinTutor     ]
value with number+dot       : [          Yawin]
value with minus+number+dot : [Yawin          ]
value with dot              : [Yawin]
value with minus            : [YawinTutor]
value with minus+dot        : [Yawin]
```

#### Tips

Android启动页的透明状态栏
启动页想要避免黑屏或白屏，最佳的实践方式是使用theme：
```
        <activity
            android:name=".SplashActivity"
            android:configChanges="keyboard|keyboardHidden|orientation|screenSize"
            android:theme="@style/AppTheme.Splash"
            android:screenOrientation="portrait">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
```
theme的定义如下所示，其中`android:windowContentOverlay`和`windowBackground`的设置可以避免状态栏启动时背景颜色的跳动：
```
<resources>
    <style name="AppTheme" parent="Theme.AppCompat.Light.NoActionBar">
        <item name="colorPrimary">@color/colorPrimary</item>
        <item name="colorPrimaryDark">@color/colorPrimaryDark</item>
        <item name="colorAccent">@color/colorAccent</item>
        <item name="android:windowContentOverlay">@null</item>
        <item name="android:windowBackground">@android:color/white</item>
    </style>

    <style name="AppTheme.Splash" parent ="AppTheme">
        <item name="android:background">@drawable/drawable_splash</item>
        <item name="android:windowFullscreen">true</item>
    </style>
</resources>
```

#### Sharing

[Hybrid项目中集成Firebase推送](https://www.jianshu.com/p/0ce5bcf041a6)
### ARTS

#### Algorithm
##### Climbing Stairs
You are climbing a stair case. It takes n steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

Note: Given n will be a positive integer.

Example 1:
```
Input: 2
Output: 2
Explanation: There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps
```
Example 2:
```
Input: 3
Output: 3
Explanation: There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
```

```java
class Solution {
    private HashMap<Integer, Integer> hashMap = new HashMap<>();

    public int climbStairs(int n) {
        if (n == 1 || n == 2) return n;

        if (hashMap.containsKey(n)) {
            return hashMap.get(n);
        }

        int ret = climbStairs(n - 1) + climbStairs(n - 2);
        hashMap.put(n, ret);
        return ret;
    }
}
```

#### Review

***SwiftUI by Tutorials*** raywenderlich 发布的一本英文电子书

[SwiftUI - Gesture](https://www.jianshu.com/p/a30113706dca)

#### Tips

将React Native引入一个由BUCK构建的iOS项目中，这个应该是BUCK构建iOS项目的最后一篇了，也是就费劲的一篇，想把BUCK引入到当前的项目中，需要把所有潜在的坑的踩一下。

[BUCK - 使用BUCK编译iOS项目(4)](https://www.jianshu.com/p/dba8af43dc9e)

#### Sharing

开始重新学backend，开始写一个系列文章：

Keycloak的第五篇，[通过rest api创建用户](https://www.jianshu.com/p/938f2cc75270)
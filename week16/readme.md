### ARTS

#### Algorithm
##### Sort an Array (Quick Sort)
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
class Solution {
    public List<Integer> sortArray(int[] arr) {
        quickSort(arr, 0, arr.length - 1);
        return convertArrayToList(arr);
    }

    private void quickSort(int[] arr, int start, int end) {
        if (start >= end) {
            return;
        }

        int startIndex = start;
        int endIndex = end;
        int anchor = startIndex;
        while (startIndex < endIndex) {
            if (arr[endIndex] > arr[anchor]) {
                endIndex--;
                continue;
            }
            if (arr[startIndex] <= arr[anchor]) {
                startIndex++;
                continue;
            }
            swap(arr, startIndex, endIndex);
        }
        swap(arr, anchor, startIndex);
        quickSort(arr, start, startIndex - 1);
        quickSort(arr, startIndex + 1, end);
    }

    private void swap(int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
    
    private List<Integer> convertArrayToList(int[] nums) {
        List<Integer> list = new ArrayList<>();
        for (int item : nums) {
            list.add(item);
        }
        return list;
    }
}
```

#### Review

原文链接：[Matt大神关于xcconfig的一篇博客](https://nshipster.com/xcconfig/)

结合自己的理解总结：[Xcode Configuration Settings File](https://www.jianshu.com/p/dc58d26038c8)

#### Tips

[React Native 拆包实践3 - react-native bundle](https://www.jianshu.com/p/359721b85f12)

#### Sharing

开始重新学backend，开始写一个系列文章：

Keycloak的第九篇 [Authentication SPI](https://www.jianshu.com/p/d18daee88e92)
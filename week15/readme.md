### ARTS

#### Algorithm
##### Sort an Array (Merge Sort)
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
    public int[] mergeSort(int[] arr) {
        return mergeSort(arr, 0, arr.length - 1);
    }

    private int[] mergeSort(int[] arr, int start, int end) {
        if (start == end) {
            return arr;
        }
        int mid = start + (end - start) / 2;
        mergeSort(arr, start, mid);
        mergeSort(arr, mid + 1, end);
        mergeSortedArray(arr, start, mid, end);
        return arr;
    }

    private void mergeSortedArray(int[] arr, int start, int mid, int end) {
        int[] result = new int[end - start + 1];
        int leftIndex = start;
        int rightIndex = mid + 1;
        int resultIndex = 0;

        while (leftIndex <= mid && rightIndex <= end) {
            if (arr[leftIndex] <= arr[rightIndex]) {
                result[resultIndex] = arr[leftIndex];
                leftIndex++;
            } else {
                result[resultIndex] = arr[rightIndex];
                rightIndex++;
            }
            resultIndex++;
        }

        while (leftIndex <= mid) {
            result[resultIndex] = arr[leftIndex];
            resultIndex++;
            leftIndex++;
        }

        while (rightIndex <= end) {
            result[resultIndex] = arr[rightIndex];
            resultIndex++;
            rightIndex++;
        }

        for (int i = 0; i < result.length; i++) {
            arr[i + start] = result[i];
        }
    }
}
```

#### Review

继续SwiftUI的Animation

原文链接：[Getting Started with SwiftUI Animations](https://www.raywenderlich.com/5815412-getting-started-with-swiftui-animations)

[SwiftUI - Animation](https://www.jianshu.com/p/d200e7295cfc)

#### Tips

[React Native 拆包实践1 - bundle server的启动过程](https://www.jianshu.com/p/d1d77c709053)

[React Native 拆包实践2 - react-native start](https://www.jianshu.com/p/473dddd751c8)

#### Sharing

开始重新学backend，开始写一个系列文章：

Keycloak的第八篇 [User Federation](https://www.jianshu.com/p/d057cc8cc383)
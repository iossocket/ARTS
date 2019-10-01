### ARTS

#### Algorithm

从一个最简单的题开始吧，TwoSum，

Given an array of integers, return indices of the two numbers such that they add up to a specific target.
You may assume that each input would have exactly one solution, and you may not use the same element twice.

*Example*

```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

*Solution*

```java
public int[] twoSum(int[] nums, int target) {
	Map<Integer, Integer> store = new HashMap<>();
	for (int i = 0; i < nums.length; i++) {
		store.put(nums[i], i);
	}
	for (int i = 0; i < nums.length; i++) {
		int required = target - nums[i];
		Integer index = store.get(required);
		if (index != null && index != i) {
			return new int[]{i, index};
		}
	}
	return new int[]{};
}
```

#### Review

#### Tips

#### Sharing


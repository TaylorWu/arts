# Algorithm
**Question: Two Sum**

Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

**Example:**

```
 Given nums = [2, 7, 11, 15], target = 9,
 
 Because nums[0] + nums[1] = 2 + 7 = 9,
 return [0, 1].
 ```
 
 ## 第一次尝试，暴力破解
 ```java
 class Solution {
      public int[] twoSum(int[] nums, int target) {
          int[] result = new int[2];
          for(int i = 0; i < nums.length - 1; i++) {
              for (int j = i + 1; j < nums.length; j++) {
                  if (nums[i] + nums[j] == target) {
                      result[0] = i;
                      result[1] = j;
                      return result;
                  }
              }
          }
          return result;
      }
  }
  ```
  使用下下标遍历数组，算法复杂度为O(n^2)
  
## 第二次，参照答案
```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int[] result = new int[2];
        Map<Integer,Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            if (map.containsKey(target - nums[i])) {
                return new int[]{map.get(target - nums[i]), i};
            }
            map.put(nums[i], i);
        }
        return result;
    }
}
```
使用map，key为数值，value为数组下标。用HashMap高效的搜索，将复杂度下降为O(n)
# Review
# Tip
# share

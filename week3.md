# Algorithm
**Question: Longest Substring Without Repeating Characters**

Given a string, find the length of the **longest substring** without repeating characters.

**Example:**
```
Given "abcabcbb", the answer is "abc", which the length is 3.

Given "bbbbb", the answer is "b", with the length of 1.

Given "pwwkew", the answer is "wke", with the length of 3. Note that the answer must be a substring, "pwke" is a subsequence and not a substring.
```
**Solution**
- 第一次尝试，暴力破解
```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int result = 0;
        if (s.length() == 1) {
            result = 1;
        }
        for (int i = 0; i < s.length() - 1; i++) {
            String sub = String.valueOf(s.charAt(i));
            for (int j = i + 1; j < s.length(); j++) {
                String charAt = String.valueOf(s.charAt(j));
                if (sub.contains(charAt)) {
                    break;
                }
                sub = s.substring(i, j + 1);
            }
            int subLength = sub.length();
            if (subLength > result) {
                result = subLength;
            }
        }
        return result;
    }
}
```
# Review
[97 Things Every Programmer Should Know](https://legacy.gitbook.com/book/97-things-every-x-should-know/97-things-every-programmer-should-know/details)
# Tip
# share
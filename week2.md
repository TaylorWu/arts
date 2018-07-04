# Algorithm
**Question: Add Two Numbers**

You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order** and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example:**
```
 Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
 Output: 7 -> 0 -> 8
 Explanation: 342 + 465 = 807.
```
**Solution**
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
     int sum = l1.val + l2.val;
     int carry = 0;
     if (sum > 9) {
         carry = 1;
         sum = sum - 10;
     }
     ListNode result = new ListNode(sum);
     ListNode l1next = l1.next;
     ListNode l2next = l2.next;
     ListNode current = result;
     ListNode next = null;
     while(l1next != null || l2next != null) {
         int v1 = 0;
         int v2 = 0;
         if (l1next != null) {
             v1 = l1next.val;
         }
         if (l2next != null) {
             v2 = l2next.val;
         }
         sum = v1 + v2 + carry;
         if (sum > 9) {
             carry = 1;
             sum = sum - 10;
         } else {
             carry = 0;
         }
         next = new ListNode(sum);
         current.next = next;
         current = next;
         if (l1next != null) {
             l1next = l1next.next;
         }
         if (l2next != null) {
             l2next = l2next.next;
         }
     }
     if (carry > 0) {
         current.next = new ListNode(1);
     }
     return result;
 }
}
```

# Review
# Tip
本周学习了Thymeleaf的基本用法
### 五种表达式
- Variable Expressions: ${...}，与velocity相同，展示变量
- Selection Variable Expressions: *{...}，在一个标签的范围内起效，可以转化为$表达式
- Message Expressions: #{...}，国际化使用，在springboot的resource中需要有message.properties文件
- Link URL Expressions: @{...}，css，js等可以用这种方式引入
- Fragment Expressions: ~{...}，写一个碎片，在别的文件中引用。类似java中一个类中调用另一个类的方法
### 基础对象
- \#request
- \#session等<br>
### 工具对象
- \#dates
- \#strings等
# share

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
花了两个中午看了耗子书推荐的一篇文章[5-hour-rule](https://medium.com/the-mission/the-5-hour-rule-if-youre-not-spending-5-hours-per-week-learning-you-re-being-irresponsible-791c3f18f5e6)，30%单词不认识，能猜个大概。<br>
开篇就说世界上最忙的人（奥巴马、盖茨、巴菲特）都有时间每天花1小时学习，你还有什么借口不学习。后面阐述了学习和金钱的关系，预计今后高技能的职位越来越多，而低技能的职位会被人工智能取代。不学习将会被淘汰。最后分享了学习的步骤，每天抽出一小时，坚持在这固定的时间内学习，实践学习成果。

# Tip
本周在公司做了一个数据对接项目，需要定期同步oracle，mysql，sqlserver数据源的数据。我第一次使用了JdbcTemplate，书上看过，但没用过。对于数据对接来讲，还是比较方便的。我将代码发布在[我的github](https://github.com/TaylorWu/jdbc-template-with-two-data-sources)上了。<br>
这里只提一句，JdbcTemplate查询数据，如果数据为空会抛EmptyResultDataAccessException异常。

# share
## 分享本周解决的一个maven打包问题
dependency的scope是system的，依赖不会传递。例如本地项目的common包pom.xml中有如下配置：
```xml
<dependency>
    <groupId>comet4j-tomcat7</groupId>
    <artifactId>comet4j-tomcat7</artifactId>
    <version>1.0</version>
    <scope>system</scope>
    <systemPath>${basedir}/src/main/resources/lib/comet4j-tomcat7.jar</systemPath>
</dependency>
```
另外一个项目引入common的依赖，但是不会自动引入comet4j-tomcat7.jar这个jar包的。  
## 解决方案
将第三方jar包上传至nexus，去掉原项目中dependency的scope。
## jar包上传至nexus
用mvn **deploy:deploy-file**命令将jar包传至nexus的repositories/releases目录下，但是maven打包是从/groups/public/目录下取文件。jar包deploy成功后nexus的Public仓库并没有刚才上传成功的jar包，原因还未找到。后来在nexus的管理界面将jar包上传至3rd party中，问题解决。

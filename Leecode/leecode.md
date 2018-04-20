# Leecode

###从排序数组中删除重复项

给定一个排序数组，你需要在原地([原地算法](https://baike.baidu.com/item/原地算法))删除重复出现的元素，使得每个元素只出现一次，返回移除后数组的新长度。不要使用额外的数组空间，你必须在原地修改输入数组并在使用 O(1) 额外空间的条件下完成。

**示例**

```java
给定数组 nums = [1,1,2], 
函数应该返回新的长度 2, 并且原数组 nums 的前两个元素被修改为 1, 2。 
你不需要考虑数组中超出新长度后面的元素。
```

**说明**

```java
// nums 是以“引用”方式传递的。也就是说，不对实参做任何拷贝
int len = removeDuplicates(nums);
// 在函数里修改输入数组对于调用者是可见的。
// 根据你的函数返回的长度, 它会打印出数组中该长度范围内的所有元素。
for (int i = 0; i < len; i++) {
    print(nums[i]);
}
```

**思路**

```java
1.遍历数组
2.用(快慢)两个角标记录，当元素重复时，跳过重复的位置，当不重复的时候，把元素放到正确的位置上去
```

**代码**

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums == null || nums.length == 0) return 0;
        int a = 0;
        for (int i = 1; i < nums.length; i++) {
            if (nums[a] != nums[i]) nums[++a] = nums[i];
        }
        return a + 1;
    }
}
```

### 买卖股票的最佳时机 II

给定一个数组，它的第 *i* 个元素是一支给定股票第 *i* 天的价格。

设计一个算法来计算你所能获取的最大利润。你可以尽可能地完成更多的交易（多次买卖一支股票）。

**ps**: 你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。

**示例**

```java
输入: [7,1,5,3,6,4]
输出: 7
解释: 在第 2 天（股票价格 = 1）的时候买入，在第 3 天（股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。随后，在第 4 天（股票价格 = 3）的时候买入，在第 5 天（股票价格 = 6）的时候卖出, 这笔交易所能获得利润 = 6-3 = 3 。
```

**思路**

```java
贪心法 允许多次买卖股票获取最大收益，只要今天比昨天的价格高了我就卖
```

**代码**

```java
class Solution {
    public int maxProfit(int[] prices) {
        //贪心法 允许多次买卖股票获取最大收益，只要今天比昨天的价格高了我就卖
        int m = 0;
        for (int i = 1; i < prices.length; i++) {
            if (prices[i] > prices[i - 1]) m += prices[i] - prices[i - 1];
        }
        return m;
    }
}
```

### 旋转数组

将包含 *n* 个元素的数组向右旋转 *k* 步。

如果  *n* = 7 ,  *k* = 3，给定数组  `[1,2,3,4,5,6,7]`  ，向右旋转后的结果为 `[5,6,7,1,2,3,4]`。

**ps**:注意要求空间复杂度为 O(1)

**思路**

```java
循环K次遍历数组，倒叙遍历将每个位置的数字角标抬高一位，并将最后一位赋值到第1位
```

**代码**

```java
class Solution {
    public void rotate(int[] nums, int k) {
       int len = nums.length;
        while (k > 0) {
            int cache = nums[len - 1];//缓存数组最后一位数
            for (int x = len - 2; x >= 0; x--) {
                nums[x + 1] = nums[x];//倒叙遍历将每个位置的数字角标抬高一位
            }
            nums[0] = cache;
            --k;//完成一个循环
        }
    }
}
```

### 存在重复

给定一个整数数组，判断是否存在重复元素。

如果任何值在数组中出现至少两次，函数应该返回 true。如果每个元素都不相同，则返回 false。

**示例**

```java
[5,3,1,2,4,2,6,10] 这个数组存在2并且至少出现了2次 应该返回true
```

**思路**

```java
//先排序 再判断相邻元素是否相同
```

**代码**

```java
class Solution {
    public boolean containsDuplicate(int[] nums) {
        //先排序 再判断相邻元素是否相同
        Arrays.sort(nums);
        for (int x = 1; x < nums.length; x++) {
            if (nums[x] == nums[x-1]) return true;
        }
        return false;
    }
}
```

### 只出现一次的数字

给定一个整数数组，除了某个元素只出现一次以外，其余每个元素均出现两次。找出那个只出现了一次的元素。**ps**:你的算法应该具有线性时间复杂度。 你可以不使用额外空间来实现吗？

**思路**

```java
//异或运算的可交换性 
// a ^ b = b ^ a
// a ^ b ^ c = a ^ (b ^ c) = (a ^ b) ^ c;
```

**代码**

```java
class Solution {
    public int singleNumber(int[] nums) {
        int len = nums.length;
        if (len == 1) return nums[0];
        int result = nums[0];
        for (int i = 1; i < len; i++) {
            result ^= nums[i];//异或运算的可交换性 
           // a ^ b = b ^ a
           // a ^ b ^ c = a ^ (b ^ c) = (a ^ b) ^ c;
        }
        return result;
    }
}
```


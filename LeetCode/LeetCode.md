# LeetCode算法练习-数组篇

### 从排序数组中删除重复项

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

### 两个数组的交集 II

给定两个数组，写一个方法来计算它们的交集。

**例如**:
给定 *nums1* = `[1, 2, 2, 1]`, *nums2* = `[2, 2]`, 返回 `[2, 2]`.

**注意**

```java
1.输出结果中每个元素出现的次数，应与元素在两个数组中出现的次数一致。
2.我们可以不考虑输出结果的顺序。
3.如果给定的数组已经排好序呢？你将如何优化你的算法？
4.如果 nums1 的大小比 nums2 小很多，哪种方法更优？
5.如果nums2的元素存储在磁盘上，内存是有限的，你不能一次加载所有的元素到内存中，你该怎么办？
```

**思路**

```java
哈希表来解决问题，将数组nums1哈希到哈希表中，然后继续将数组nums2哈希到哈希表中，如果发生哈希碰撞则统计加1，最后可以得出数组的交集。时间复杂度也就是哈希所有元素的复杂度O(n)。这里我使用HashMap来处理
```

**代码**

```java
class Solution {
    public int[] intersect(int[] nums1, int[] nums2) {
        ArrayList<Integer> temp = new ArrayList<>();
        HashMap<Integer, Integer> hashMap = new HashMap<>();
        for (int i = 0; i < nums1.length; i++) {
            Integer value = hashMap.get(nums1[i]);
            hashMap.put(nums1[i], (value == null ? 0 : value) + 1);
        }

        for (int i = 0; i < nums2.length; i++) {
            if (hashMap.containsKey(nums2[i]) && hashMap.get(nums2[i]) != 0) {
                temp.add(nums2[i]);
                hashMap.put(nums2[i], hashMap.get(nums2[i]) - 1);
            }
        }
        int[] result = new int[temp.size()];
        for (int i = 0; i < temp.size(); i++) {
            result[i] = temp.get(i);
        }
        return result;
    }
}
```

### 加一

给定一个**非负整数**组成的**非空**数组，在该数的基础上加一，返回一个新的数组。

最高位数字存放在数组的首位， 数组中每个元素只存储一个数字。

你可以假设除了整数 0 之外，这个整数不会以零开头。

**示例**

```java
输入: [1,2,3]
输出: [1,2,4]
解释: 输入数组表示数字 123。

输入: [4,3,2,1]
输出: [4,3,2,2]
解释: 输入数组表示数字 4321。
```

**思路**

```java
解法的关键在于弄明白什么情况下会产生进位

想让个位+1进位，那么个位必须为9

想让十位+1进位，那么十位必须为9，想要产生进位carry，那么必须由个位进位而来。想让个位进位，个位必须为9.

想让百位+1进位，那么百位必须为9，想要产生进位carry，那么必须由十位进位而来，想让十位进位，那么十位必须为9，想要产生进位，个位必须为9。

根据以上可以推论得出两种情况：
1.最高位进位
2.最高位不进位

最高位进位 
//若最高位进位，那么比他低的位数字都为9，且加1后都为0，需要初始化一个长度为(lenght+1)的新数组，0位置为1代表进位

最高位不进位 
//若最高位不进位，那么不需要产生新数组，后续数字由更低位计算而来
```

**代码**

```java
class Solution {
    public int[] plusOne(int[] digits) {
       int carry = 1;
        for (int i = digits.length - 1; i >= 0; i--) {
            if (carry == 0) {
                return digits;
            }
            int tmp = digits[i] + carry;
            carry = tmp / 10;
            digits[i] = tmp % 10;
        }
        if (carry != 0) {
            int[] result = new int[digits.length + 1];
            result[0] = 1;
            return result;
        }
        return digits;
    }
}
```

### 移动零

给定一个数组 `nums`, 编写一个函数将所有 `0` 移动到它的末尾，同时保持非零元素的相对顺序。

例如， 定义 `nums = [0, 1, 0, 3, 12]`，调用函数之后， `nums` 应为 `[1, 3, 12, 0, 0]`。

**注意事项**

1. 必须在原数组上操作，不要为一个新数组分配额外空间。
2. 尽量减少操作总数。

**思路**

```java
1.遍历数组，使用慢指针去记录非零整数的个数，同时并移动位置
2.得到0的个数 倒序遍历数组 补位0 知道个数满足记录下的0的个数
```

**代码**

```java
class Solution {
    public void moveZeroes(int[] nums) {
        int unZeroCount = 0;//慢指针去记录非0整数的个数，同时并移动位置
        int len = nums.length;
        for (int i = 0; i < len; i++) {
            if (nums[i] != 0) {
                nums[unZeroCount] = nums[i];
                ++unZeroCount;
            }
        }
        //数组末尾有这么多个0  去补位
        int zeroCount = len - unZeroCount;
        for (int i = len - 1; i > 0; i--) {
            if (zeroCount == 0) return;
            nums[i] = 0;
            --zeroCount;
        }
    }
}
```

### 两数之和

给定一个整数数组和一个目标值，找出数组中和为目标值的两个数。

你可以假设每个输入只对应一种答案，且同样的元素不能被重复利用。

**示例**

```java
给定 nums = [2, 7, 11, 15], target = 9
因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]
```

**思路**

```java
我希望通过O(n)的时间复杂度完成要求。第一遍O(n)的算法将每个数据a对应的target-a建立查询的数据结构，例如Hash表；第二遍遍历时，查询每个数是否在Hash表中，每次查询时间复杂度为O(1)，总的时间复杂度是O(n)。
```

**代码**

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) map.put(nums[i], i);
        for (int i = 0; i < nums.length; i++) {
            int value = target - nums[i];
            //差值存在哈希表中且角标不是当前被减数自己 防止 6-3=3这种的清空的出现
            if (map.containsKey(value) && map.get(value) != i) {
                int index = map.get(value);
                if (i < index) return new int[]{i, index};
                return new int[]{index, i};
            }
        }
        return new int[0];
    }
}
```

### 旋转图像

给定一个 *n* × *n* 的二维矩阵表示一个图像。

将图像顺时针旋转 90 度。

**说明**

```java
//你必须在原地旋转图像，这意味着你需要直接修改输入的二维矩阵。请不要使用另一个矩阵来旋转图像。
```

**示例**

```java
给定 matrix = 
[
  [1,2,3],
  [4,5,6],
  [7,8,9]
],

原地旋转输入矩阵，使其变为:
[
  [7,4,1],
  [8,5,2],
  [9,6,3]
]

给定 matrix =
[
  [ 5, 1, 9,11],
  [ 2, 4, 8,10],
  [13, 3, 6, 7],
  [15,14,12,16]
], 

原地旋转输入矩阵，使其变为:
[
  [15,13, 2, 5],
  [14, 3, 4, 1],
  [12, 6, 8, 9],
  [16, 7,10,11]
]

```

**思路**

```java
坐标旋转(顺时针)
90°（相当于逆时针270°）：a[i][j]=b[j][n-i-1];
//转置矩阵  行变列
创建一个新的矩阵：b[i][j] = a[j][i];
对原矩阵进行求转置矩阵，转置矩阵每一行进行反转即可得到旋转90°后的矩阵
```



**代码**

```java
class Solution {
    public void rotate(int[][] matrix) {
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) return;
        int length = matrix.length;
        for (int i = 0; i < length / 2; i++) {
            for (int j = 0; j < (length + 1) / 2; j++) {
                int tmp = matrix[i][j];
                matrix[i][j] = matrix[length - j - 1][i];
                matrix[length - j - 1][i] = matrix[length - i - 1][length - j - 1];
                matrix[length - i - 1][length - j - 1] = matrix[j][length - i - 1];
                matrix[j][length - i - 1] = tmp;
            }
        }
    }
}
```


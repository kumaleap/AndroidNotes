# LeeCode算法练习-字符串篇

### 反转字符串

请编写一个函数，其功能是将输入的字符串反转过来。

**示例**

```java
输入：s = "hello"
返回："olleh"
```

**思路**

```java
1、string 转char[]数组 然后依序遍历
2、位运算 a^=b 交换位置 ab交换位置 我示例代码给这个思路的 效率会高一些
```

**代码**

```java
class Solution {
        public String reverseString(String s) {
            if (null == s || s.length() == 0) return s;
            char[] ch = s.toCharArray();//字符串转换成字符数组
            int len = s.length();
            for (int i = 0; i < len / 2; i++) {
                ch[i] ^= ch[len - 1 - i];//位运算交换位置
                ch[len - 1 - i] ^= ch[i];
                ch[i] ^= ch[len - 1 - i];
            }
            return new String(ch);
        }
    }
```

### 反转整数

给定一个 32 位有符号整数，将整数中的数字进行反转。

**示例**

```java
输入: 123
输出: 321

输入: -123
输出: -321

输入: 120
输出: 21

//假设我们的环境只能存储 32 位有符号整数，其数值范围是 [−231,  231 − 1]。
//根据这个假设，如果反转后的整数溢出，则返回 0。
```

**思路**

```java
1、判断符号
2、反转数字
3、去0 并转成数字
4、如果抛异常就返回0
```

**代码**

```java
class Solution {
        public int reverse(int x) {
            boolean isF = x < 0;
            String value = String.valueOf(Math.abs(x));
            char[] chars = value.toCharArray();
            int len = chars.length;
            for (int i = 0; i < len / 2; i++) {
                chars[i] ^= chars[len - 1 - i];//位运算交换位置
                chars[len - 1 - i] ^= chars[i];
                chars[i] ^= chars[len - 1 - i];
            }
            value = new String(chars);
            if (chars[0] == 0) value = value.substring(1);
            try {
                if (isF) return -1 * Integer.parseInt(value);
                return Integer.parseInt(value);
            } catch (Exception e) {
                return 0;
            }
        }
    }
```

### 字符串中的第一个唯一字符

给定一个字符串，找到它的第一个不重复的字符，并返回它的索引。如果不存在，则返回 -1。

**示例**

```java
s = "leetcode"
返回 0.

s = "loveleetcode",
返回 2.
 
//您可以假定该字符串只包含小写字母。
```

**思路**

```java
//建立Hash表 排除重复选项 再遍历hash表 判断是否有唯一字符
```

**代码**

```java
class Solution {
        public int firstUniqChar(String s) {
            int index = -1;
            if (s == null) return index;
            Map<Character, Integer> chMap = new LinkedHashMap<>();
            for (char c : s.toCharArray()) {
                if (!chMap.containsKey(c)) {
                    chMap.put(c, 1);
                } else {
                    chMap.put(c, chMap.get(c) + 1);
                }
            }
            for (Character key : chMap.keySet()) {
                if (chMap.get(key) == 1) return s.indexOf(String.valueOf(key));
            }
            return index;
        }
    }
```


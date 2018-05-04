# LeetCode算法练习-字符串篇

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

### 有效的字母异位词

给定两个字符串 *s* 和 *t* ，编写一个函数来判断 *t* 是否是 *s* 的一个字母异位词。

**示例**

```java
s = "anagram"，t = "nagaram"，返回 true
s = "rat"，t = "car"，返回 false
注意：假定字符串只包含小写字母。
提升难度:
输入的字符串包含 unicode 字符怎么办？你能能否调整你的解法来适应这种情况？
```

**思路**

```jav
1.将两个字符串转换为字符串数组
2.排序数组
3.判断两个数组的元素是否相同(用系统自带的方法了，你也可以遍历，其实系统方法内部实现原理也不一样是遍历)
```

**代码**

```java
class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) return false;
        // if (s.length() == 1 && t.length() == 1) return s.equals(t);
        char[] sch = s.toCharArray();
        char[] tch = t.toCharArray();
        Arrays.sort(sch);
        Arrays.sort(tch);
        return Arrays.equals(sch, tch);
    }
}
```

### 验证回文字符串

给定一个字符串，验证它是否是回文串，只考虑字母和数字字符，可以忽略字母的大小写。

**说明：**本题中，我们将空字符串定义为有效的回文串。

**示例**

```java
输入: "A man, a plan, a canal: Panama"
输出: true
    
输入: "race a car"
输出: false
```

**思路**

```java
1.替换字符串中的所有空格 如果替换完的字符串为空 则返回true 空格为有效的回文串
2.提出除英文字符和数字以外所有的特殊字符并将大写转换为小写
3.翻转字符串
4.判断翻转后的字符串与翻转前的字符串是否相等
```

**代码**

```java
class Solution {
    public boolean isPalindrome(String s) {
        if (s.length() == 1) return true;
        String p = s.replace(" ", "");
        if (p.equals("")) return true;
        s = p.replaceAll("[^a-z0-9A-Z]", "").toLowerCase();
        char[] ch = s.toCharArray();
        int len = s.length();
        for (int i = 0; i < len / 2; i++) {
            ch[i] ^= ch[len - 1 - i];//位运算交换位置
            ch[len - 1 - i] ^= ch[i];
            ch[i] ^= ch[len - 1 - i];
        }
        return s.equals(new String(ch));
    }
}

//另外一种写法

class Solution {
    public boolean isPalindrome(String s) {
        if (s.length() == 1) return true;
        if (s.replace(" ", "").equals("")) return true;
        s = s.replaceAll("[^a-z0-9A-Z]", "");
        return s.equalsIgnoreCase(new StringBuffer(s).reverse().toString());
    }
}

```

### 字符串转整数（atoi）

实现 `atoi`，将字符串转为整数。

在找到第一个非空字符之前，需要移除掉字符串中的空格字符。如果第一个非空字符是正号或负号，选取该符号，并将其与后面尽可能多的连续的数字组合起来，这部分字符即为整数的值。如果第一个非空字符是数字，则直接将其与之后连续的数字字符组合起来，形成整数。

字符串可以在形成整数的字符后面包括多余的字符，这些字符可以被忽略，它们对于函数没有影响。

当字符串中的第一个非空字符序列不是个有效的整数；或字符串为空；或字符串仅包含空白字符时，则不进行转换。

若函数不能执行有效的转换，返回 0。

**说明：**

假设我们的环境只能存储 32 位有符号整数，其数值范围是 [−231,  231 − 1]。如果数值超过可表示的范围，则返回  INT_MAX (231 − 1) 或 INT_MIN (−231) 。

**示例**

```java
输入: "42"
输出: 42

输入: "   -42"
输出: -42
解释: 第一个非空白字符为 '-', 它是一个负号。
     我们尽可能将负号与后面所有连续出现的数字组合起来，最后得到 -42 。


输入: "4193 with words"
输出: 4193
解释: 转换截止于数字 '3' ，因为它的下一个字符不为数字。

输入: "words and 987"
输出: 0
解释: 第一个非空字符是 'w', 但它不是数字或正、负号。
     因此无法执行有效的转换。
     

输入: "-91283472332"
输出: -2147483648
解释: 数字 "-91283472332" 超过 32 位有符号整数范围。 
     因此返回 INT_MIN (−231) 。
```

**思路**

```java
去除字符串两端空字符
拦截输入字符只是+或者-的字符
拦截首字符是非数字字符直接返回0
遍历判断是否为数字字符遇到非数字即跳出循环
```

**代码**

```java
class Solution {
    public int myAtoi(String str) {
        str = str.trim();
        if (str.length() == 0) return 0;
        if (str.equals("+") || str.equals("-")) return 0;
        String first = String.valueOf(str.charAt(0));
        if (!first.equals("+") 
            && !first.equals("-") && !Character.isDigit(str.charAt(0))) return 0;
        boolean isF = first.equals("-");
        if (first.equals("+") || isF) str = str.substring(1);
        char[] ch = str.toCharArray();
        String s = "";
        p:
        for (char c : ch) {
            if (Character.isDigit(c)) s += c;
            else break p;
        }
        if (s.length() == 0) return 0;
        try {
            if (isF) return -1 * Integer.parseInt(s);
            return Integer.parseInt(s);
        } catch (Exception e) {
            if (isF) return Integer.MIN_VALUE;
            return Integer.MAX_VALUE;
        }
    }
}
```


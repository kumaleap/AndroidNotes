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

### 实现strStr()

实现 [strStr()](https://baike.baidu.com/item/strstr/811469) 函数。给定一个 haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 (从0开始)。如果不存在，则返回  **-1**。

**示例**

```java
输入: haystack = "hello", needle = "ll"
输出: 2

输入: haystack = "aaaaa", needle = "bba"
输出: -1
```

**注意**:当`needle`是空字符串时，应当返回`0`

**思路**

```java
这道算法其实是让我们明白 string类内 indexOf() 方法的原理
当然你使用 indexOf() 方法可以快速完成，但是最好还是知道下原理最好
原理解释：首先会查找子字符串的头字符在此字符串中第一次出现的位置，再以此位置的下一个位置开始，然后将子字符串的字符依次和此字符串中字符进行比较，如果全部相等，则返回这个头字符在此字符串中的位置；如果有不相等的，则继续在剩下的字符串中查找，继续进行上面的过程，直到查找到子字符串或没有找到返回-1为止。
```

**代码**

```java
class Solution {
        public int strStr(String haystack, String needle) {
            if (needle == null || needle.length() == 0) return 0;
            return haystack.indexOf(needle);
        }
    }
```

### 数数并说

报数序列是指一个整数序列，按照其中的整数的顺序进行报数，得到下一个数。其前五项如下：

```
1.     1
2.     11
3.     21
4.     1211
5.     111221
```

**示例**

```JAVA
输入: 1
输出: "1"
    
输入: 4
输出: "1211"
```

**思路**

```java
"数数并说，搞清楚什么时候合并数字什么时候不合并数字就可以了。"
1.并说：超过1个相同的数字连在一起时，并说，也就是"几个几"
2.不并说：前后数字不同时，不并说，需要单说，也就是"1个几"
```

**代码**

```java
class Solution {
        public String countAndSay(int n) {
            if (n <= 0) return "-1";
            String result = "1";
            for (int i = 1; i < n; i++) {
                StringBuilder builder = new StringBuilder();
                int index = 0;
                while (index < result.length()) {
                    // 记录值
                    char val = result.charAt(index);
                    // 记录连续位数
                    int count = 0;
                    // 查找连续位数，碰到不相同的数字时停止。
                    while (index < result.length() && result.charAt(index) == val) {
                        index++;
                        count++;
                    }
                    // 追加连续位数到结果中
                    builder.append(String.valueOf(count));
                    // 追加连续位数的值到结果中
                    builder.append(val);
                }
                result = builder.toString();
            }
            return result;
        }
    }
```

### 最长公共前缀

编写一个函数来查找字符串数组中的最长公共前缀。

如果不存在公共前缀，返回空字符串 `""`。

**示例**

```java
输入: ["flower","flow","flight"]
输出: "fl"
    
    
输入: ["dog","racecar","car"]
输出: ""
解释: 输入不存在公共前缀。

//说明：所有输入只包含小写字母 a-z 。
```

**思路**

```java
1.获取字符串数组中字符串最小的串
2.使用最小串遍历定位字符串数组中相同串的长度
```

**代码**

```java
class Solution {
        public String longestCommonPrefix(String[] strs) {
            if (strs.length == 0) return "";
            int minLen = Integer.MAX_VALUE;
            for (String str : strs) {
                minLen = Math.min(minLen, str.length());
            }
            int low = 0;
            int high = minLen;
            while (low <= high) {///注意是 <=
                int middle = (low + high) / 2;
                if (isCommonPrefix(strs, middle))
                    low = middle + 1;
                else
                    high = middle - 1;
            }
            return strs[0].substring(0, (low + high) / 2);
        }

        private boolean isCommonPrefix(String[] strs, int len) {
            String str1 = strs[0].substring(0, len);
            for (int i = 0; i < strs.length; i++) {
                if (!strs[i].startsWith(str1))
                    return false;
            }
            return true;
        }
    }
```


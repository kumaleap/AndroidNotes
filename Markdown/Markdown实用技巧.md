# Markdown实用技巧－语法教程

### 标题

Markdown支持多种标题格式

1、使用 `=`（等号定义一级标题） 和 `-`（减号定义二级标题），任意数量的加号和减号都是相同的效果；

2、通过在行首插入 1 到 6 个 # ，来定义对应的 1 到 6 阶 标题，个人推荐使用这种；

| Markdown        | 预览     |
| --------------- | -------- |
| # 一级标题      | 一级标题 |
| ## 二级标题     | 二级标题 |
| ### 三级标题    | 三级标题 |
| #### 四级标题   | 四级标题 |
| ##### 五级标题  | 五级标题 |
| ###### 六级标题 | 六级标题 |

### 特殊效果

| Markdown                                          | 预览     |
| ------------------------------------------------- | -------- |
| \*倾斜\*                                          | *倾斜*   |
| \*\*粗体\*\*                                      | **粗体** |
| \~\~删除线\~\~                                    | 删除线   |
| \>引用                                            | >引用    |
| 下划线使用3个`* 星号`或者 `- 减号`或者 `_ 下划线` | ---      |
| 反斜杠`\`来还原一些特殊语法的字符                 | \*Hi\*   |

### 段落和换行

Markdown支持段内换行，如果你想进行段落内换行可以在上一行结尾插入两个以上的空格后再回车;

如果相邻的两行文字之间存在`空行` `空格` `TAB` `回车` 等都会被视为不同段落;

### 代码

程序员使用的比较多一些的就是贴示例代码；

1、使用\`行内代码\` 展示出来的效果就是 `行内代码`；

2、多行代码

多行代码使用 3 个反引号来标记(反引号一般位于键盘左上角，要用英文) ，在第一个 `｀｀｀` 后面可以跟语言类型，没有语言类型可以省略不写；

```
​``` java
// 我是注释
int x = 100;
​```
```

**预览:**

```java
// 我是注释
int x = 100;
```

### 表格

Markdown 标准(原生)语法中没有表格支持，但现在多数平台已经支持了该语法，如 GitHub，CSDN，简书 等均支持；

**Markdown：**

```markdown
| 默认  |   靠右 |  居中  | 靠左   |
| ---- |  ---: | :--:  | :---  |
| 内容  |   内容 |  内容  | 内容   |
| 内容  |   内容 |  条目  | 内容   |
```

**预览：**

| 默认 | 靠右 | 居中 | 靠左 |
| ---- | ---- | ---- | ---- |
| 内容 | 内容 | 内容 | 内容 |
| 内容 | 内容 | 条目 | 内容 |

### 无序表格

无序列表前面可以用 `*` `+` `-` 等，结果是相同的。
有序列表的数字即便不按照顺序排列，结果仍是有序的。

```
* 内容
* 内容
* 内容
  * 子内容
  * 子内容
* 内容
```

**预览**：

* 内容
* 内容
* 内容
  * 子内容
  * 子内容
* 内容

### 图片及链接

1、行内式链接

```
github地址：[github](http://www.github.com/wulijie)
github地址：[github](htttp://www.github.com/wulijie "这里写的内容会在你鼠标停在链接上时显示")
```

**预览**：

github地址：[github](http://www.github.com/wulijie)

github地址：[github](htttp://www.github.com/wulijie "这里写的内容会在你鼠标停在链接上时显示")

2、自动链接

```
<http://www.github.com/wulijie>
```

**预览**：

<http://www.github.com/wulijie>

3、相对链接

```python
//如果你的内容发布在github或者个人网站上，此时可以用相对链接
![头像](/assets/wulijie/head.jpg)
//多平台发布时切忌不要使用相对链接
//某些本地编辑器不支持读取相对链接
```

4、图片链接

```
//图片链接其实就是把图片和链接嵌套在一起
[![](https://ws3.sinaimg.cn/large/006tNbRwly1fpzi4y1ftsj305r05rq2q.jpg)](http://www.github.com/wulijie)
```

**预览**：

[![](https://ws3.sinaimg.cn/large/006tNbRwly1fpzi4y1ftsj305r05rq2q.jpg)](http://www.github.com/wulijie)

5、参考式链接

```java
//在写文章的时候很可能会出现在同一个地方多次引用同一个链接地址
//使用方式
[wulijie的github][1]
[AndroidNotes][2]
//链接声明
[1]: http://www.github.com/wulijie
[2]: https://github.com/wulijie/AndroidNotes "一个神奇的网站"
[文章]:https://github.com/wulijie/AndroidNotes
```

**预览**：

如果你喜欢我的文章，请访问[wulijie的github][1]并关注我，另外[AndroidNotes][2]也是个很不错的[文章][]

[1]: http://www.github.com/wulijie
[2]: https://github.com/wulijie/AndroidNotes "一个神奇的网站"
[文章]:https://github.com/wulijie/AndroidNotes

6、拓展语法（可能在某些平台或者编辑器无法使用，请自测后在使用）

**在新标签页打开**（在后面添加上 `{:target="_blank"}` 或者使用 HTML 语法）

```
<http://www.github.com/wulijie>{:target="_blank"}

<a href="http://www.github.com/wulijie" target="_blank">wulijie的github</a>
```

**预览**：

<a href="http://www.github.com/wulijie" target="_blank">wulijie的github</a>

**控制图片的大小**（使用 `{:width="300" height="100"}` 或者 HTML 格式可以控制图片显示大小）

```
![](https://ws3.sinaimg.cn/large/006tNbRwly1fpzi4y1ftsj305r05rq2q.jpg){:width="50"}

<img src="https://ws3.sinaimg.cn/large/006tNbRwly1fpzi4y1ftsj305r05rq2q.jpg" width="50"/>
```

**预览**：

<img src="https://ws3.sinaimg.cn/large/006tNbRwly1fpzi4y1ftsj305r05rq2q.jpg" width="50"/>


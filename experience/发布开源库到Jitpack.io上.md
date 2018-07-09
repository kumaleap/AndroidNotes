# 发布开源库到Jitpack.io上

### 配置gradle

project的`gradle`下的配置：

```groovy
buildscript {
    
    repositories {
        google()
        jcenter()
        //jitpack need
        mavenCentral()
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:3.1.2'
        //jitpack need
        classpath 'com.github.dcendents:android-maven-gradle-plugin:1.5'
    }
}
```

lib的`gradle`下的配置：

```groovy
apply plugin: 'com.android.library'
//这个跟Jcenter一样的插件
apply plugin: 'com.github.dcendents.android-maven'
//你的Github用户名替换一下
group='com.github.your-github-name'
```

### 操作github

你开源库怎么上传到github上就不用细说了，下面重点说下，github和`jitpack`

如何搭配起来的。

打开你在github上的开源库页面 => 点击`release`:

![](https://ws3.sinaimg.cn/large/006tNc79ly1frz8steltmj30h50arjrf.jpg)

点击`create a new release`

![](https://ws3.sinaimg.cn/large/006tNc79ly1frz8r6cfuoj30gz07lt8o.jpg)

填写版本信息、点发布：

![](https://ws2.sinaimg.cn/large/006tNc79ly1frz8u9bcljj30jk0lzglx.jpg)

切记：项目的gradle文件夹下的文件一定要传上去，否则`jitpack`是无法编译通过的。
![](https://ws3.sinaimg.cn/large/006tNc79ly1frz8uzaz3cj30990dmq2y.jpg)

[jitpack.io](https://jitpack.io) 打开官网 => 使用你的github进行登录，然后你就会看到在左侧有一排你的库

点击：你的库

![](https://ws2.sinaimg.cn/large/006tNc79ly1frz8xsf1wsj306q0etdfs.jpg)

此时`jitpack`其实已经在加载中了，耐心等待你的库编译通过就好了。

绿色的log 代表你ok了，点击log文件 ，打开可以查看运行配置的信息，也可以看你的库的引用地址，比如：

![](https://ws3.sinaimg.cn/large/006tNc79ly1frz8zuus4kj30is0ctaaf.jpg)

ok，到此结束了，快去试试吧。比Jcenter好用几百倍。
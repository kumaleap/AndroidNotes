# TensorFlow入门 - Android机器学习应用

### TensorFlow-Android 介绍

Google开源项目[TensorFlow-Android Example](https://github.com/tensorflow/tensorflow/tree/master/tensorflow/examples/android) 中实现了Android 应用中使用`TF模型` 进行机器学习的功能。

阅读 [TensorFlow-Android REDDME](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/contrib/android/README.md) 自己尝试基于TensorFlow示例中已有的模型来构建Android的应用。

### 获取已有的数据模型

可以在我的项目示例的 [asstes](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/java/README.md) 中复制，也可以去下载 Google 提供的一个数据模型 [inception5h.zip](https://link.jianshu.com/?t=https%3A%2F%2Fstorage.googleapis.com%2Fdownload.tensorflow.org%2Fmodels%2Finception5h.zip)；其中 `.pb` 后缀的文件是已经训练好的模型，而 `.txt` 对应的是训练数据包含的所有标签。

这个模型可对 1008 种物品识别分类，具体有哪些类可以查看标签信息，至于每个类别到底训练了多少张图片就不得而知了。

### 在Android项目中引入TensorFlow

如果你使用的是`AndroidStudio`，那么恭喜你可以像集成其他第三方库一样，通过`Jcenter`就可以完成库的依赖；

```groovy
allprojects {
    repositories {
        jcenter()
    }
}

dependencies {
    //使用+号 可以保持最新的版本
    compile 'org.tensorflow:tensorflow-android:+'
}
```

**如果有兴趣可以阅读TensorFlow的JavaAPI**  [TensorFlow Java API](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/java/README.md)

> 这里我们直接使用了 Google 为我们编译好的 TensorFlow 现成库了，如果你想自行对 TensorFlow 进行 NDK 交叉编译得到库文件也可以。具体交叉编译，看教程 [TensorFlow-Android REDDME](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/contrib/android/README.md)

### 图片识别功能的实现

将获取到的数据模型，复制到项目的`assets` 文件下；

```java
--- asstes
	--- model
		--- imagenet_comp_graph_label_strings.txt //  对应的是训练数据包含的所有标签
		--- tensorflow_inception_graph.pb //已经训练好的模型
		--- LICENSE //开源协议
```






### 相关介绍

Google开源项目[TensorFlow-Android Example](https://github.com/tensorflow/tensorflow/tree/master/tensorflow/examples/android) 中实现了Android 应用中使用`TF模型` 进行机器学习的功能。

阅读 [TensorFlow-Android REDDME](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/contrib/android/README.md) 自己尝试基于TensorFlow示例中已有的模型来构建Android的应用。

### 获取已有的数据模型

可以在我的项目示例的 [asstes](https://github.com/wulijie/MyTensorFlow/tree/master/app/src/main/assets) 中复制，也可以去下载 Google 提供的一个数据模型 [inception5h.zip](https://storage.googleapis.com/download.tensorflow.org/models/inception5h.zip)；

其中 `.pb` 后缀的文件是已经训练好的模型，而 `.txt` 对应的是训练数据包含的所有标签。

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
    implementation 'org.tensorflow:tensorflow-android:+'
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

**代码构建**

```java
    //权限是必须的
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
    <uses-permission android:name="android.permission.CAMERA"/>
```

直接使用 Google demo 项目中提供的 [Classifier.java](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/examples/android/src/org/tensorflow/demo/Classifier.java) 和 [TensorFlowImageClassifier.java](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/examples/android/src/org/tensorflow/demo/TensorFlowImageClassifier.java) 这两个类来实现；

其中重点的注意的方法是如下两个：

**TensorFlowImageClassifier**的静态`create`方法；

```java
/**
     * Initializes a native TensorFlow session for classifying images.
     *
     * @param assetManager The asset manager to be used to load assets.
     * @param modelFilename The filepath of the model GraphDef protocol buffer.
     * @param labelFilename The filepath of label file for classes.
     * @param inputSize The input size. A square image of inputSize x inputSize is assumed.
     * @param imageMean The assumed mean of the image values.
     * @param imageStd The assumed std of the image values.
     * @param inputName The label of the image input node.
     * @param outputName The label of the output node.
     * @throws IOException
     */
public static Classifier create(AssetManager assetManager, String modelFilename, String labelFilename,int inputSize, int imageMean, float imageStd, String inputName, String outputName)
```

该方法需要传入模型相关的参数进行初始化，完成后返回一个 `Classifier` 实例。

通过 `Classifier` 对象，我们可以调用其 `recognizeImage` 方法来识别我们传入的 `bitmap` 图像数据，该方法会返回图像类别后对物品类别进行推断的标签结果：

```java
/**
 * 进行图片识别
 */
 public List<Recognition> recognizeImage(final Bitmap bitmap)
```

代码下载[地址](https://github.com/wulijie/MyTensorFlow)

**效果**

![](https://github.com/wulijie/MyTensorFlow/blob/master/app/src/main/assets/Screenshot.png)


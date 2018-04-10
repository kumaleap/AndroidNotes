# Android使用Infura、Web3j、Http等方式接入以太坊区块链

### 接入以太坊区块链的方式

1、自己搭建节点，终端去访问搭建好的节点获取数据

2、使用免费的[Infura](https://infura.io/signup)，省去创建节点的烦恼

### Infura

[Infura](https://infura.io/signup) 提供免费公开的Ethereum(以太坊)主网和测试网络节点；申请只要输入一点基本资料和Email就可以在你输入的Email邮箱里收到[Infura](https://infura.io/signup)发给你的邮件，邮件内容主要是你可以使用的主网节点及测试网络节点的地址。

ps：[Infura](https://infura.io/signup) 需要翻墙才能注册过去，有个验证码需要你翻墙才能显示出来，可以用免费的[蓝灯](https://github.com/getlantern/forum)翻墙。

**邮件内容截图如下**

![](https://ws2.sinaimg.cn/large/006tNc79ly1fq6iv5z53gj30b40afdg4.jpg)

###  [web3j](https://github.com/web3j/web3j) 接入方式

1、 [web3j](https://github.com/web3j/web3j)**介绍**

 [web3j](https://github.com/web3j/web3j)是一个轻量级，Reactive(响应式)，类型安全的Java库，用于与Ethereum网络上的客户端（节点）集       成，这允许您使用Ethereum块链，而不需要为平台编写自己的集成代码的额外开销。

2、 [web3j](https://github.com/web3j/web3j)**的提供的功能**

* 通过HTTP和IPC 完成Ethereum的JSON-RPC客户端API的实现
* Ethereum钱包支持
* 使用过滤器的函数式编程功能的API
* 自动生成Java智能合约包装器，以创建、部署、处理和调用来自本地Java代码的智能合约
* 支持Parity的 个人和Geth的 个人客户端API
* 支持[Infura](https://infura.io/signup)，所以您不必自己运行一个Ethereum客户端
* 一套综合化、一体的测试示范和可运行的脚步
* 支持命令行工具
* 兼容Android
* 支持JP Morgan’s Quorum via [web3j-quorum](https://github.com/web3j/quorum)

3、 [web3j](https://github.com/web3j/web3j)的集成

最新的集成方式可以参考[web3j的说明文档](https://docs.web3j.io/getting_started.html#gradle)

```groovy
implementation 'org.web3j:core:3.3.1'//切记需要java8 
implementation 'org.web3j:core:3.3.1-android'
```

4、[web3j](https://github.com/web3j/web3j)的使用

web3j的api说明文档挺简陋的，看着头晕，建议配合[web3的文档](https://github.com/ethereum/wiki/wiki/JavaScript-API)对照着看，应该会提高效率；

另外我还找到了他人翻译的[web3的中文文档](http://web3.tryblockchain.org/Web3.js-api-refrence.html)，当做参考。

```java
//获取节点运行geth客户端的版本号
String url = "https://mainnet.infura.io/your api-key";
Web3j web3 = Web3j.build(new HttpService(url));
Web3ClientVersion web3ClientVersion = web3.web3ClientVersion().sendAsync().get();
String clientVersion = web3ClientVersion.getWeb3ClientVersion();

//只读属性，返回当前节点持有的帐户列表 这个方法说明就是我从web3的中文文档里找到的
String url = "https://mainnet.infura.io/your api-key";
Web3j web3 = Web3j.build(new HttpService(url));
//点进ethAccounts()方法的源码就可以知道返回的是什么对象了
EthAccounts ethAccounts = web3.ethAccounts().sendAsync().get();
List<String> accountList = ethAccounts.getAccounts();//返回当前节点持有的账户列表
```

这样简单的接入就完成了。

### JSON-RPC API 的接入方式

因为Ethereum（以太坊）提供了[JSON-RPC API](https://github.com/ethereum/wiki/wiki/JSON-RPC#web3_clientversion) 可以访问。

**JSON-RPC support**

| cpp-ethereum   | go-ethereum | py-ethereum | parity |      |
| -------------- | ----------- | ----------- | ------ | ---- |
| JSON-RPC 1.0   | ✓           |             |        |      |
| JSON-RPC 2.0   | ✓           | ✓           | ✓      | ✓    |
| Batch requests | ✓           | ✓           | ✓      | ✓    |
| HTTP           | ✓           | ✓           | ✓      | ✓    |
| IPC            | ✓           | ✓           |        | ✓    |
| WS             |             |             |        |      |

1、**Http**

Http是以太坊各种客户端都支持的方式之一，也是终端开发最熟悉的。

```java
//查阅API 发现需要POST的形式 参数以json的形式 请求
//这里我测试使用的是xutils3 以请求版本号为例
String json = "{\"jsonrpc\":\"2.0\",\"method\":\"web3_clientVersion\",\"params\":[],\"id\":67}";
RequestParams params = new RequestParams("https://mainnet.infura.io/your api-key");
params.setAsJsonContent(true);
params.setBodyContent(json);
x.http().post(params, new Callback.CommonCallback<String>() {
            @Override
            public void onSuccess(String result) {
                Log.e("wlj", "result" + result);
            }

            @Override
            public void onError(Throwable ex, boolean isOnCallback) {
                Log.e("wlj", ex.toString());
            }

            @Override
            public void onCancelled(CancelledException cex) {

            }

            @Override
            public void onFinished() {

            }
        });

```

2、**JSONRPC 2.0的方式**

下载 [jar包](http://www.java2s.com/Code/Jar/a/Downloadandroidjsonrpc034jar.htm) ，导入AndroidStudio的libs下，引入依赖。

```java
// 获取节点运行geth客户端的版本号 
final String url = "https://mainnet.infura.io/your api-key";

//对着 JSON-RPC API 的参数说明拼接参数
final Map<String, Object> map = new HashMap();
List paramsList = new ArrayList();
map.put("json-rpc", "2.0");
map.put("method", "web3_clientVersion");
map.put("params", paramsList);
map.put("id", "67");

//需要异步处理 当然你可以配合handler来更新页面
new Thread(new Runnable() {
            @Override
            public void run() {
			 JSONRPCHttpClient client = new JSONRPCHttpClient(url);
			String clientVersion = client.callString("web3_clientVersion", map);
            }
}).start();
```

这两种传参方式繁琐复杂，没有web3j封装的好，但是好在灵活自由。


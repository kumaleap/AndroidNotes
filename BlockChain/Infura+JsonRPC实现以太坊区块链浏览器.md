# Infura

Infura 提供公开的 Ethereum 主网和测试网路节点。到 [Infura 官网申请](https://infura.io/signup)，只要输入一点基本资料和 Email，就可以在邮件中收到 带有`API-key的链接地址。
**如下**

![邮件截图](https://ws4.sinaimg.cn/large/006tNc79ly1fq6fzvilscj30j50hyt98.jpg)



示例代码

```java
String url = "https://mainnet.infura.io/your api-key";
JSONRPCHttpClient client = new JSONRPCHttpClient(url);
Map<String, Object> map = new HashMap();
List paramsList = new ArrayList();
map.put("json-rpc", "2.0");
map.put("method", "web3_clientVersion");
map.put("params", paramsList);
map.put("id", "67");
String st = client.callString("web3_clientVersion", map);
```



Web3j库的示例(需要 Java8)

```java
Web3j web3 = Web3j.build(new HttpService("https://mainnet.infura.io/your api-key"));
Web3ClientVersion web3ClientVersion = web3.web3ClientVersion().sendAsync().get();
String clientVersion = web3ClientVersion.getWeb3ClientVersion();
```


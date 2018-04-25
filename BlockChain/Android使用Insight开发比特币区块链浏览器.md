# Android使用Insight开发比特币区块链浏览器

如果喜欢这篇文章，欢迎来star下我的[安卓笔记](https://github.com/wulijie/AndroidNotes)哦。

### 接入BTC、BCH区块链的方式

1、自己搭建节点，终端去访问搭建好的节点获取数据；

2、使用第三方免费的节点[Insight-api](https://github.com/bitpay/insight-api)，省去创建节点的烦恼；

### Insight

[Insight](https://github.com/bitpay/insight)是一款开源的web端区块链浏览器，支持BTC、BCH等区块链浏览器；并且对外公开了访问区块链的API

如果不想自己搭建节点，使用android开发一款区块链浏览器的话，使用这个官网提供的api就能实现简单的浏览器功能；

### 如何接入

**BTC（比特币）**               接入地址：[https://insight.bitpay.com/api](https://insight.bitpay.com/api)
**BCH（比特币现金)**         接入地址：[https://bch-insight.bitpay.com/api](https://bch-insight.bitpay.com/api)

查看[Insight-api](https://github.com/bitpay/insight-api)的Readme内提供的接口说明文档，调用相应功能接口；

**代码示例**        

下面均以BTC为例，因为两个区块链本来就是一样的

根据交易Hash获取某一个交易详情

请求方式Get

https://insight.bitpay.com/api/tx/0a37339bfe54474095e96b83ded45aa1f745beee4faf55039f25087858d5c2cf



```json
//使用GET请求 调用地址  https://insight.bitpay.com/api/tx/交易hash
//返回结果

{
	"txid": "0a37339bfe54474095e96b83ded45aa1f745beee4faf55039f25087858d5c2cf",
	"version": 2,
	"locktime": 518049,
	"vin": [{
		"txid": "c9f0b642b566dc2076efe5dc685c3f7655eab05986f9cb6b992e984415489544",
		"vout": 113,
		"sequence": 4294967294,
		"n": 0,
		"scriptSig": {
			"hex": "483045022100ad25609e2a845542f4e47351ef9e9a7256bc40d0d20b617ce2ae083dcfc4a4cd0220238a871042376df11008dc5b5b7a45c09f0a6d29e4faa59e33f1efdb3238af450121038d588053a29779e3c2b10d9be59b9695c091d62268ed05cf5329a58f89373c2b",
			"asm": "3045022100ad25609e2a845542f4e47351ef9e9a7256bc40d0d20b617ce2ae083dcfc4a4cd0220238a871042376df11008dc5b5b7a45c09f0a6d29e4faa59e33f1efdb3238af45[ALL] 038d588053a29779e3c2b10d9be59b9695c091d62268ed05cf5329a58f89373c2b"
		},
		"addr": "1EruNcryxv71TTMvBJC2w7kYm8NPZ8Sapv",
		"valueSat": 5578915,
		"value": 0.05578915,
		"doubleSpentTxID": null
	}, {
		"txid": "ff9f16e26879a71ce1e3ec0c95805db56f30ca120bdfff55dbf9fb6172d26ee1",
		"vout": 1,
		"sequence": 4294967294,
		"n": 1,
		"scriptSig": {
			"hex": "483045022100d195a21eddeb747ae1ca573790b0fe7935f8a229d54dff32781816be63e0af8a0220528548bbea30cb84ceb613d85b8834c910a2aa4c14d2e9adddad055b4ebb9b0b01210338b140b65ac68df0f29dd730b1d50748465651784f3d43b60a740d53ef0ce3f8",
			"asm": "3045022100d195a21eddeb747ae1ca573790b0fe7935f8a229d54dff32781816be63e0af8a0220528548bbea30cb84ceb613d85b8834c910a2aa4c14d2e9adddad055b4ebb9b0b[ALL] 0338b140b65ac68df0f29dd730b1d50748465651784f3d43b60a740d53ef0ce3f8"
		},
		"addr": "1NpmsWtQArECreydtxgZn8n6eseT67PNyn",
		"valueSat": 5000000,
		"value": 0.05,
		"doubleSpentTxID": null
	}],
	"vout": [{
		"value": "0.03946339",
		"n": 0,
		"scriptPubKey": {
			"hex": "76a914bea093f139989dccf7725fb2794efe048ce14f7f88ac",
			"asm": "OP_DUP OP_HASH160 bea093f139989dccf7725fb2794efe048ce14f7f OP_EQUALVERIFY OP_CHECKSIG",
			"addresses": ["1JNwkbZQEtcVcoyeMMk9i9ZtxGk5yWHq2A"],
			"type": "pubkeyhash"
		},
		"spentTxId": "69e08bc96290b00b04d45e77c36912f981bdc3097084e0b5f49c1131ebd05e16",
		"spentIndex": 0,
		"spentHeight": 518051
	}, {
		"value": "0.06353576",
		"n": 1,
		"scriptPubKey": {
			"hex": "a914c56cbaf35f6723ffab76f0a7fc4f3f55beed07ce87",
			"asm": "OP_HASH160 c56cbaf35f6723ffab76f0a7fc4f3f55beed07ce OP_EQUAL",
			"addresses": ["3KguJ3eFC1z8gyiC6kEmDJrsC36BmEPfEm"],
			"type": "scripthash"
		},
		"spentTxId": null,
		"spentIndex": null,
		"spentHeight": null
	}],
	"blockhash": "0000000000000000003492ab1123c56fa769c8fe15005496b402a7d3360f6c0d",
	"blockheight": 518050,
	"confirmations": 1797,
	"time": 1523643926,
	"blocktime": 1523643926,
	"valueOut": 0.10299915,
	"size": 372,
	"valueIn": 0.10578915,
	"fees": 0.00279
}

//返回结果说明：
//txId其实就是交易Hash
//fees是旷工费
//valueIn和valueOut代表的这笔交易的输入总量或者输出总量
//vin数组和vout数组代表的是这些笔交易内的一些参与地址 从xxx转账到xxx

//其实比对数据有个很简单的小技巧，
//就是你可以找市面上已经做好的区块链浏览器，
//因为同一个hash返回的数据跟他们做的应该是一模一样的，
//因为使用的都是区块链内的数据；
```

**我做的区块链软件示例** 还在接入其他区块链比如莱特币、以太坊经典币ETC等，后续开源项目方便大家学习

![](https://ws3.sinaimg.cn/large/006tNc79ly1fqoz1e9kkdj30u02b6mz3.jpg)![](https://ws1.sinaimg.cn/large/006tNc79ly1fqoz1r093yj30u01pk0ue.jpg)
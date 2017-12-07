# 【区块链】利用IPFS构建自己的去中心化分布式Wiki系统

@(小枫Blog)

>IPFS全称InterPlanetary File System，中文名：星际文件系统，是一个旨在创建持久且分布式存储和共享文件的网络传输协议。
>它是一种内容可寻址的对等超媒体分发协议。在IPFS网络中的节点将构成一个分布式文件系统。它是一个开放源代码项目，自2014年开始由Protocol Labs （协议实验室）在开源社区的帮助下发展。其最初由Juan Benet设计。
>IPFS是点对点的超媒体协议，可以让网络更快、更安全、更开放。它是一个面向全球的、点对点的分布式版本文件系统，试图将所有具有相同文件系统的计算设备连接在一起。
>官网：https://ipfs.io/

[TOC]

![](http://daijiale-cn.oss-cn-hangzhou.aliyuncs.com/djl-blog-pic/ipfs/ipfs_io.png)

## 一、IPFS 简介

IPFS—又称“星际文件系统”。简单点说，它是一个点对点的分布式文件系统（和比特币技术一样），通过底层协议，可以让存储在IPFS系统上的文件，在全世界任何一个地方快速获取，且不受防火墙的影响（无需网络代理）。

我们现在所使用的互联网协议被称作——超文本协议HTTP。这种协议具有超中心化特性。

也就是说，你从互联网上下载文件或者是浏览网页，一次只能从一个数据中心获取你所需要的资料。如果这个数据中心出现故障，或者被限制或是攻击，就会出现文件丢失或者网页无法打开的问题。比如你存在某云盘的资料突然无法下载，或者你想浏览的网页因为某些政策原因无法打开。

而IPFS的目的就是解决这些问题。在某些方面，IPFS类似Web，你一样可以基于IPFS进行互联网地址的链接。但IPFS是去中心化的，它不存在Web的主网故障问题。所以，**IPFS完全取代掉HTTP也并非天方夜谭**。


### 1.1 IPFS与HTTP的区别

#### HTTP的四大痛点
![](http://daijiale-cn.oss-cn-hangzhou.aliyuncs.com/djl-blog-pic/ipfs/IPFS%20is%20the%20Distributed%20Web.png)

>HTTP效率低下，服务器成本昂贵

使用HTTP协议从一台计算机服务器上一次只能下载一个文件，而不是同时从多台计算机中获取文件。通过P2P方式的视频传输可以节省带宽成本的60％。

>历史文件被删除

网页的平均使用寿命为100天，大量的网站文件不能得以长期保存。有些重要的文件因操作不当，也有可能永远在互联网消失。

>中心化的网络限制了机会

互联网一直是人类进步的催化器，但中心化的网络容易被控制，是对互联网良性发展的的威胁。

>网络应用太依赖骨干网

为保证数据的可靠性，我们开发的应用程序太依赖大型的中心服务器，并通过大量的备份来保证数据的安全。


HTTP协议已经用了20年的历史，从HTTP 1.0 到现在的HTTP5，网页的展示越来越美观丰富，**但它背后的Browser/Server 模式是从来没变的**。


#### IPFS区别于HTTP痛点的特质

>互联网信息永久存储

IPFS像是一个分布式存储网络（类似于SIA），任何存储在系统里的资源，包括文字、图片、声音、视频，以及网站代码，通过IPFS进行哈希运算后，都会生成唯一的地址。今后，你只要通过这个地址就可以打开它们。并且这个地址是可以被分享的。

而由于加密算法的保护，该地址具备了不可篡改和删除的特性（在某种意义上，如果破解密码还是有可能被篡改或删除，但概率极低）。所以，一旦数据存储在IPFS中，它就会是永久性的。比如我们经常会遇到的某个资源删除无法访问的问题。


这种情况，在IPFS上就不会发生。即便是把该站点撤销，只要存储该站点信息的网络依然存在，该网页就可以被正常访问。存储站点的分布式网络越多，它的可靠性也就越强。

与SIA不同的是，IPFS存储的一般是公共信息，普通大众都可以获得的。有一种说法认为，**如果IPFS完全取代HTTP，那么此后，人类历史将会被永久保存，且不会被篡改**。

这也就意味着，人类所做的每一件事情都会被记录，不管是正确的、抑或是错误的。


>解决过度冗余问题，实现共享经济

如果你喜欢某部电影，又担心电影资源丢失，通常的做法是，你会把这部电影下载在自己的电脑上。比如电影《阿凡达》，在2016年一年的下载次数就达到了1658万次，总下载数量更是惊人。那么一个无法避免的问题是：同样的一部电影被反复储存，造成了内存资源极大浪费。这就是HTTP协议的弊端。同样的资源备份的次数过多，就会造成过度冗余的问题。

而IPFS的出现可以很好的解决这个问题。IPFS会把存储文件，做一次哈希计算，只字不差的两个文件哈希值相同。所以，用户只需要使用相同的哈希值，就可以访问那个文件，这个哈希值就是文件的地址。只要获取这个地址，就可以共享资源了。

基于上面的永久存储特性，你再也不用担心某个电影找不到了，也不用备份，**因为全球电脑上只要有那么几个人存储着，你就能拿到它。而不是重复存储几十万份**。



>同时基于内容寻址，而非基于域名寻址。

IPFS的网络上运行着一条区块链，即用来存储互联网文件的哈希值表，每次有网络访问，即要在链上查询该内容（文件）的地址。

文件（内容）具有存在的唯一性，一个文件加入了IPFS的网络，将基于计算对内容赋予一个唯一加密的哈希值。这将改变我们使用域名访问网络的习惯。

提供文件的历史版本控制器（类似Git），并且让多节点使用保存不同版本的文件。


>节点存储激励，代币分成

通过使用代币（FileCoin）的激励作用，让各节点有动力去存储数据。 Filecoin 是一个由加密货币驱动的存储网络**。矿工通过为网络提供开放的硬盘空间获得Filecoin，而用户则用 Filecoin 来支付在去中心化网络中储存加密文件的费用**。



### 1.2 IPFS工作原理

![](http://daijiale-cn.oss-cn-hangzhou.aliyuncs.com/djl-blog-pic/ipfs/ipfswork.jpg)

- 每个文件及其中的所有块都被赋予一个称为加密散列的唯一指纹。

- IPFS通过网络删除重复具有相同哈希值的文件，通过计算是可以判断哪些文件是冗余重复的。并跟踪每个文件的版本历史记录。

- 每个网络节点只存储它感兴趣的内容，以及一些索引信息，有助于弄清楚谁在存储什么。

- 查找文件时，你通过文件的哈希值就可以在网络查找到储存改文件的节点，找到想要的文件。

- 使用称为IPNS（去中心化命名系统），每个文件都可以被协作命名为易读的名字。通过搜索，就能很容易地找到想要查看的文件。

- 从IPFS的介绍可以看出， IPFS设想的是让所有的网络终端节点不仅仅只充当 Browser或Client的角色，其实人人都可以作为这个网络的运营者，人人都可以是服务器。


## 二、IPFS 配置

### 2.1 IPFS 下载

下载地址：https://dist.ipfs.io/#go-ipfs

本篇博客下载并使用的版本是：**go-ipfs Version v0.4.13 for OS X 64bit**


### 2.2 IPFS 安装

![](http://daijiale-cn.oss-cn-hangzhou.aliyuncs.com/djl-blog-pic/ipfs/ipfs_install1.png)

```
ipfs --help  //打开命令行，输入，出现Log信息时，表示安装成功
```

### 2.3 IPFS本地部署


#### 2.3.1 创建节点

在本地全局目录下新建仓库：


![](http://daijiale-cn.oss-cn-hangzhou.aliyuncs.com/djl-blog-pic/ipfs/ipfs_init.png)


#### 2.3.2 节点配置



```
cd ~/.ipfs
export EDITOR=/usr/bin/vim
ipfs config edit
```

执行完`ipfs config edit`后会打开一个ipfs节点配置文件，可以如下修改配置参数

```json
{
	"Identity":{
		"PeerID":"QmXXXXXXXXXXXXXXX",
		"PrivKey":"XXXXXXXXXXXX"
	},
	"Datastore":{
		"StorageMax":"10GB",
		"StorageGCWatermark":90,
		"GCPeriod":"1h",
		"Spec":{
			"mounts":[
				{
					"child":{
						"path":"blocks",
						"shardFunc":"/repo/flatfs/shard/v1/next-to-last/2",
						"sync":true,
						"type":"flatfs"
					},
					"mountpoint":"/blocks",
					"prefix":"flatfs.datastore",
					"type":"measure"
				},
				{
					"child":{
						"compression":"none",
						"path":"datastore",
						"type":"levelds"
					},
					"mountpoint":"/",
					"prefix":"leveldb.datastore",
					"type":"measure"
				}
			],
			"type":"mount"
		},
		"HashOnRead":false,
		"BloomFilterSize":0
	},
	"Addresses":{
		"Swarm":[
			"/ip4/0.0.0.0/tcp/4001",
			"/ip6/::/tcp/4001"
		],
		"Announce":[

		],
		"NoAnnounce":[

		],
		"API":"/ip4/127.0.0.1/tcp/5001",
		"Gateway":"/ip4/127.0.0.1/tcp/8080"
	},
	"Mounts":{
		"IPFS":"/ipfs",
		"IPNS":"/ipns",
		"FuseAllowOther":false
	},
	"Discovery":{
		"MDNS":{
			"Enabled":true,
			"Interval":10
		}
	},
	"Ipns":{
		"RepublishPeriod":"",
		"RecordLifetime":"",
		"ResolveCacheSize":128
	},
	"Bootstrap":[
		"/dnsaddr/bootstrap.libp2p.io/ipfs/QmNnooDu7bfjPFoTZYxMNLWUQJyrVwtbZg5gBMjTezGAJN",
		"/dnsaddr/bootstrap.libp2p.io/ipfs/QmQCU2EcMqAqQPR2i9bChDtGNJchTbq5TbXJJ16u19uLTa",
		"/dnsaddr/bootstrap.libp2p.io/ipfs/QmbLHAnMoJPWSCR5Zhtx6BHJX9KiKNN6tpvbUcqanj75Nb",
		"/dnsaddr/bootstrap.libp2p.io/ipfs/QmcZf59bWwK5XFi76CZX8cbJ4BhTzzA3gU1ZjYZcYW3dwt",
		"/ip4/104.131.131.82/tcp/4001/ipfs/QmaCpDMGvV2BGHeYERUEnRQAwe3N8SzbUtfsmvsqQLuvuJ",
		"/ip4/104.236.179.241/tcp/4001/ipfs/QmSoLPppuBtQSGwKDZT2M73ULpjvfd3aZ6ha4oFGL1KrGM",
		"/ip4/128.199.219.111/tcp/4001/ipfs/QmSoLSafTMBsPKadTEgaXctDQVcqN88CNLHXMkTNwMKPnu",
		"/ip4/104.236.76.40/tcp/4001/ipfs/QmSoLV4Bbm51jM9C4gDYZQ9Cy3U6aXMJDAbzgu2fzaDs64",
		"/ip4/178.62.158.247/tcp/4001/ipfs/QmSoLer265NRgSp2LA3dPaeykiS1J6DifTC88f5uVQKNAd",
		"/ip6/2604:a880:1:20::203:d001/tcp/4001/ipfs/QmSoLPppuBtQSGwKDZT2M73ULpjvfd3aZ6ha4oFGL1KrGM",
		"/ip6/2400:6180:0:d0::151:6001/tcp/4001/ipfs/QmSoLSafTMBsPKadTEgaXctDQVcqN88CNLHXMkTNwMKPnu",
		"/ip6/2604:a880:800:10::4a:5001/tcp/4001/ipfs/QmSoLV4Bbm51jM9C4gDYZQ9Cy3U6aXMJDAbzgu2fzaDs64",
		"/ip6/2a03:b0c0:0:1010::23:1001/tcp/4001/ipfs/QmSoLer265NRgSp2LA3dPaeykiS1J6DifTC88f5uVQKNAd"
	],
	"Gateway":{
		"HTTPHeaders":{
			"Access-Control-Allow-Headers":[
				"X-Requested-With",
				"Range"
			],
			"Access-Control-Allow-Methods":[
				"GET"
			],
			"Access-Control-Allow-Origin":[
				"*"
			]
		},
		"RootRedirect":"",
		"Writable":false,
		"PathPrefixes":[

		]
	},
	"API":{
		"HTTPHeaders":null
	},
	"Swarm":{
		"AddrFilters":null,
		"DisableBandwidthMetrics":false,
		"DisableNatPortMap":false,
		"DisableRelay":false,
		"EnableRelayHop":false,
		"ConnMgr":{
			"Type":"basic",
			"LowWater":600,
			"HighWater":900,
			"GracePeriod":"20s"
		}
	},
	"Reprovider":{
		"Interval":"12h",
		"Strategy":"all"
	},
	"Experimental":{
		"FilestoreEnabled":false,
		"ShardingEnabled":false,
		"Libp2pStreamMounting":false
	}
}
```

#### 2.3.3 节点ID

每个节点都会存在一个唯一标识，查看节点ID方式如下：

```

ipfs id 

```

#### 2.3.4 启动节点服务器

```
ipfs daemon
```

![](http://daijiale-cn.oss-cn-hangzhou.aliyuncs.com/djl-blog-pic/ipfs/ipfs-daemon-error.png)


出现了5001端口被占用的情况，这边可以通过对**节点配置文件的修改**来解决，如下所示：


- 找到所有配置5001端口的地方
- 替换成5002端口

![](http://daijiale-cn.oss-cn-hangzhou.aliyuncs.com/djl-blog-pic/ipfs/ipfs-config-edit.png)



再次启动节点，服务成功启动如下所示：

![](http://daijiale-cn.oss-cn-hangzhou.aliyuncs.com/djl-blog-pic/ipfs/ipfs-run-successful.png)



#### 2.3.5 配置CORS跨域资源共享

为了方便后续前端的开发和数据访问，提前对跨域资源共享`CORS`进行配置，`ctrl-c` 退出` ipfs`，然后按照下面的步骤进行跨域配置：

```
ipfs config --json API.HTTPHeaders.Access-Control-Allow-Methods '["PUT", "GET", "POST", "OPTIONS"]'

ipfs config --json API.HTTPHeaders.Access-Control-Allow-Origin '["*"]'
```

#### 2.3.6 验证

浏览器打开 http://localhost:5002/webui ，出现Web Console 图形化控制台

![](http://daijiale-cn.oss-cn-hangzhou.aliyuncs.com/djl-blog-pic/ipfs/webui-connection.png)

这里可以看到所有run在主网上的节点信息，和本地节点相关的配置数据。


## 三、IPFS 项目实践

>**利用 IPFS 构建一个去中心化、不可篡改的分布式Wiki系统**


### 3.1 新建workplace

考虑到方便后期开源和推广，这边我是托管在github上，**大家可以选择自己熟悉的代码托管服务，也可以克隆我的工程 -> [ipfs-wiki-system](https://github.com/daijiale/ipfs-wiki-system)，在其基础上进行你的二次开发，有任何问题，欢迎提交issue给我**

```
mkdir workplace
cd workplace
git clone git@github.com:daijiale/ipfs-wiki-system.git
```

### 3.2 wiki系统搭建

```
cd workplace/ipfs-wiki-system/wiki-release
ll
```
可以看到如下文件：

- **wiki-release**
	- **index.html**     //markdown模板渲染
	- **navigation.md**       //导航markdown
	- **index.md**      //首页markdown

大家可以参考`ipfs-wiki` Demo，根据自己的需求，通过[markdown](https://baike.baidu.com/item/markdown/3245829?fr=aladdin)自定义不同的wiki内容和目录。

### 3.3 挂载本地节点


![](http://daijiale-cn.oss-cn-hangzhou.aliyuncs.com/djl-blog-pic/ipfs/publish-to-block.png)

记住文件根目录的Hash值：QmV5ZVQxXURKPDcVDW8WjpLCiQYvNzg173XcB6rYFevoXm


### 3.4 发布到主网

```
ipfs daemon
```

https://ipfs.io/ipfs/QmV5ZVQxXURKPDcVDW8WjpLCiQYvNzg173XcB6rYFevoXm/#!index.md

### 3.5 发布到IPNS

由于ipfs的hash对应着一个不可变的内容，每次更新网站之后，website的hash都会变，旧的link不能访问到新的内容。

ipfs提供了`ipns`来解决更新的问题。

ipfs允许用户使用一个私有密钥来对哈希附加一个引用，使用一个公共密钥哈希（简称pubkeyhash）表示你的网站的最新版本。

具体操作是:


![](http://daijiale-cn.oss-cn-hangzhou.aliyuncs.com/djl-blog-pic/ipfs/ipns.png)

通过上述方式，就完成了website和一个固定的link的绑定：
`QmPS5NRXPCeAUtofKbW7c58Qm4PpM8mPEVJvaooE13LF78`

### 3.6 绑定验证

```
ipfs name resolve QmPS5NRXPCeAUtofKbW7c58Qm4PpM8mPEVJvaooE13LF78

/ipfs/QmV5ZVQxXURKPDcVDW8WjpLCiQYvNzg173XcB6rYFevoXm
```

**IPNS访问固定节点Hash：**

https://ipfs.io/ipns/QmPS5NRXPCeAUtofKbW7c58Qm4PpM8mPEVJvaooE13LF78

验证成功，出现如下效果：

![](http://daijiale-cn.oss-cn-hangzhou.aliyuncs.com/djl-blog-pic/ipfs/ipfs-wiki-demo.png)



### 3.7 去中心化验证

以之前发布到主网的节点为第一节点，我们本地再新建一个节点，用以模拟第二节点的身份，打开Web Console：

![](http://daijiale-cn.oss-cn-hangzhou.aliyuncs.com/djl-blog-pic/ipfs/ipfs-web-consolve.png)

在第二节点上，我们依然可以通过`IPFS HASH`查询到第一节点主网上的 `ipfs-wiki-system`目录文件数据


同时，我们也能看到：控制台显示记录了我们发布至主网数据的区块节点数已经扩散至275个。

![](http://daijiale-cn.oss-cn-hangzhou.aliyuncs.com/djl-blog-pic/ipfs/ipfs-peer-id.png)

也就是说，来自另外全球其他274地方的个体，在自己的''记账本''中记下了你之前发布的数据，**哪怕其中个别服务器宕机（天灾人祸，挖断电缆，世界末日等等），只要有一个节点安好，你的数据都不会丢失**，真正意义实现了**去中心化的服务机制**。


## 四、项目体验

![](http://daijiale-cn.oss-cn-hangzhou.aliyuncs.com/djl-blog-pic/ipfs/ipfs-wiki-demo.png)

[-> 传送门](https://ipfs.io/ipfs/QmV5ZVQxXURKPDcVDW8WjpLCiQYvNzg173XcB6rYFevoXm/#!index.md)



## 参考文献

>本文部分内容参考如下文献，特别鸣谢

- [如何使用星际文件传输网络（IPFS）搭建区块链服务-黎跃春](http://liyuechun.org/2017/09/18/ipfs-blockchain/)
- [Youtube实验室](https://www.youtube.com/watch?v=iUVLuXjPAfg)
- [protocol协议实验室](https://protocol.ai/)
- [Filecoin早期旷工计划](https://filecoin.io/)
- [IPFS开发英文官方文档](https://ipfs.io/docs/)
- [IPFS——它能取代HTTP协议？](http://www.jianshu.com/p/ddccae89a49a)
- [IPFS—http的终极杀手](http://mp.weixin.qq.com/s/0nHPzty51knpYOZZaBIA8g)



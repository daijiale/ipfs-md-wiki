# [IPFS 维基百科]

[![jaywcjlove/sb](https://jaywcjlove.github.io/sb/lang/chinese.svg)](README-zh.md)

 本项目期望利用 IPFS 和Markdown 构建一个去中心化、不可篡改的分布式Wiki系统。

欢迎免费 **star** and **fork**，和一些建设性的PR.

## Explanation

[English](README.md) | [中文](README-zh.md)

## 使用引导

### 新建workplace

考虑到方便后期开源和推广，这边我是托管在github上，**大家可以选择自己熟悉的代码托管服务，也可以克隆我的工程 -> [ipfs-wiki-system](https://github.com/daijiale/ipfs-wiki-system)，在其基础上进行你的二次开发，有任何问题，欢迎提交issue给我**

```
mkdir workplace
cd workplace
git clone git@github.com:daijiale/ipfs-wiki-system.git
```

### wiki系统搭建

```
cd workplace/ipfs-wiki-system/wiki-release
ll
```

可以看到如下文件：

- **wiki-release**

  - **index.html** //markdown模板渲染
  - **navigation.md** //导航markdown
  - **index.md** //首页markdown

大家可以参考`ipfs-wiki` Demo，根据自己的需求，通过[markdown](https://baike.baidu.com/item/markdown/3245829?fr=aladdin)自定义不同的wiki内容和目录。

### 挂载本地节点

![](http://daijiale-cn.oss-cn-hangzhou.aliyuncs.com/djl-blog-pic/ipfs/publish-to-block.png)

记住文件根目录的Hash值：QmV5ZVQxXURKPDcVDW8WjpLCiQYvNzg173XcB6rYFevoXm

### 发布到主网

```
ipfs daemon
```

<https://ipfs.io/ipfs/QmV5ZVQxXURKPDcVDW8WjpLCiQYvNzg173XcB6rYFevoXm/#!index.md>

### 发布到IPNS

由于ipfs的hash对应着一个不可变的内容，每次更新网站之后，website的hash都会变，旧的link不能访问到新的内容。

ipfs提供了`ipns`来解决更新的问题。

ipfs允许用户使用一个私有密钥来对哈希附加一个引用，使用一个公共密钥哈希（简称pubkeyhash）表示你的网站的最新版本。

具体操作是:

![](http://daijiale-cn.oss-cn-hangzhou.aliyuncs.com/djl-blog-pic/ipfs/ipns.png)

通过上述方式，就完成了website和一个固定的link的绑定： `QmPS5NRXPCeAUtofKbW7c58Qm4PpM8mPEVJvaooE13LF78`

### 绑定验证

```
ipfs name resolve QmPS5NRXPCeAUtofKbW7c58Qm4PpM8mPEVJvaooE13LF78

/ipfs/QmV5ZVQxXURKPDcVDW8WjpLCiQYvNzg173XcB6rYFevoXm
```

**IPNS访问固定节点Hash：**

<https://ipfs.io/ipns/QmPS5NRXPCeAUtofKbW7c58Qm4PpM8mPEVJvaooE13LF78>

验证成功，出现如下效果：

![](http://daijiale-cn.oss-cn-hangzhou.aliyuncs.com/djl-blog-pic/ipfs/ipfs-wiki-demo.png)

### 去中心化验证

以之前发布到主网的节点为第一节点，我们本地再新建一个节点，用以模拟第二节点的身份，打开Web Console：

![](http://daijiale-cn.oss-cn-hangzhou.aliyuncs.com/djl-blog-pic/ipfs/ipfs-web-consolve.png)

在第二节点上，我们依然可以通过`IPFS HASH`查询到第一节点主网上的 `ipfs-wiki-system`目录文件数据

同时，我们也能看到：控制台显示记录了我们发布至主网数据的区块节点数已经扩散至275个。

![](http://daijiale-cn.oss-cn-hangzhou.aliyuncs.com/djl-blog-pic/ipfs/ipfs-peer-id.png)

也就是说，来自另外全球其他274地方的个体，在自己的''记账本''中记下了你之前发布的数据，**哪怕其中个别服务器宕机（天灾人祸，挖断电缆，世界末日等等），只要有一个节点安好，你的数据都不会丢失**，真正意义实现了**去中心化的服务机制**。

## 项目体验

![](http://daijiale-cn.oss-cn-hangzhou.aliyuncs.com/djl-blog-pic/ipfs/ipfs-wiki-demo.png)

[-> 传送门](https://ipfs.io/ipfs/QmV5ZVQxXURKPDcVDW8WjpLCiQYvNzg173XcB6rYFevoXm/#!index.md)

## 参考文献

> 本文部分内容参考如下文献，特别鸣谢

- [如何使用星际文件传输网络（IPFS）搭建区块链服务-黎跃春](http://liyuechun.org/2017/09/18/ipfs-blockchain/)
- [Youtube实验室](https://www.youtube.com/watch?v=iUVLuXjPAfg)
- [protocol协议实验室](https://protocol.ai/)
- [Filecoin早期旷工计划](https://filecoin.io/)
- [IPFS开发英文官方文档](https://ipfs.io/docs/)
- [IPFS----它能取代HTTP协议？](http://www.jianshu.com/p/ddccae89a49a)
- [IPFS--http的终极杀手](http://mp.weixin.qq.com/s/0nHPzty51knpYOZZaBIA8g)

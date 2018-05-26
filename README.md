# [ipfs-wiki-system] build your wiki system base on ipfs and markdown

[![jaywcjlove/sb](https://jaywcjlove.github.io/sb/lang/chinese.svg)](README-zh.md)

 The goal of the project is to build a wiki system on ipfs. The wiki data is **decentration** and **not modifiable**.

If anyone interest this project, they can direct clone this repo to yourself.

Welcome to commit any question or issue to me.

Feel free to **star** and **fork**.

## Explanation

[English](README.md) | [中文](README-zh.md)

## How to use

### Create Workplace

```
mkdir workplace
cd workplace
git clone git@github.com:daijiale/ipfs-wiki-system.git
```

### Build Wiki System

Exec these command:

```
cd workplace/ipfs-wiki-system/wiki-release
ll
```

The output:

- **wiki-release**

  - **index.html** //markdown模板渲染
  - **navigation.md** //导航markdown
  - **index.md** //首页markdown

Everyone can refer this repo to make yourself wiki content by `markdown` format.

### Mount Location Node

![](http://daijiale-cn.oss-cn-hangzhou.aliyuncs.com/djl-blog-pic/ipfs/publish-to-block.png)

Remember the hash of the files root directory: QmV5ZVQxXURKPDcVDW8WjpLCiQYvNzg173XcB6rYFevoXm

### Public To Master Net

Just execute `ipfs daemon`, the wiki file would to send to the ipfs net.

The example is [this](https://ipfs.io/ipfs/QmV5ZVQxXURKPDcVDW8WjpLCiQYvNzg173XcB6rYFevoXm/#!index.md)

### Public To IPNS

Since one hash corresponding one not modifable content, if update a website, the website hash would be changed, and other old links can't find this new website.

For resolve this problem, `ipfs` support a basic component names `IPNS`.

ipfs allow user to create an additional message with a file hash and a private key, and use a pubkeyhash to indicate your lastest website version.

The operation command is blow:

![](http://daijiale-cn.oss-cn-hangzhou.aliyuncs.com/djl-blog-pic/ipfs/ipns.png)

Finish it now, we have a fixed link to bundle a website: `QmPS5NRXPCeAUtofKbW7c58Qm4PpM8mPEVJvaooE13LF78`

### Bundling Validation

```
ipfs name resolve QmPS5NRXPCeAUtofKbW7c58Qm4PpM8mPEVJvaooE13LF78

/ipfs/QmV5ZVQxXURKPDcVDW8WjpLCiQYvNzg173XcB6rYFevoXm
```

**Use IPNS To Access Fixed Node Hash:**

<https://ipfs.io/ipns/QmPS5NRXPCeAUtofKbW7c58Qm4PpM8mPEVJvaooE13LF78>

When verification successful, we will see this result:

![](http://daijiale-cn.oss-cn-hangzhou.aliyuncs.com/djl-blog-pic/ipfs/ipfs-wiki-demo.png)

### Decentration Validation

Now we assume the node that recived our data is first node. Then we create another node in location to simulate the second node.

Open web console:

![](http://daijiale-cn.oss-cn-hangzhou.aliyuncs.com/djl-blog-pic/ipfs/ipfs-web-consolve.png)

In the second node, we also can use `IPFS HASH` to find the `ipfs-wiki-system` content of first node.

And we can see our data has spreaded to 275 nodes in the ipfs console. In other words, there are 274 nodes have recorded our data in there own 'book'. So we don't warry about any disaster. If one node is well, our data would not lost.

![](http://daijiale-cn.oss-cn-hangzhou.aliyuncs.com/djl-blog-pic/ipfs/ipfs-peer-id.png)

### Project Demo

![](http://daijiale-cn.oss-cn-hangzhou.aliyuncs.com/djl-blog-pic/ipfs/ipfs-wiki-demo.png)

[-> demo](https://ipfs.io/ipfs/QmV5ZVQxXURKPDcVDW8WjpLCiQYvNzg173XcB6rYFevoXm/#!index.md)

## Reference

- [How To Build A BlockChain Service On IPFS - YuanChunLi](http://liyuechun.org/2017/09/18/ipfs-blockchain/)
- [Youtube Lab](https://www.youtube.com/watch?v=iUVLuXjPAfg)
- [protocol lab](https://protocol.ai/)
- [Filecoin Miner Early Plan](https://filecoin.io/)
- [IPFS Development Doc](https://ipfs.io/docs/)
- [IPFS----Replace HTTP Protocol?](http://www.jianshu.com/p/ddccae89a49a)
- [IPFS--Killer To HTTP](http://mp.weixin.qq.com/s/0nHPzty51knpYOZZaBIA8g)

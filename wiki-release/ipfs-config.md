# IPFS配置

## IPFS 下载

下载地址：<https://dist.ipfs.io/#go-ipfs>

本篇博客下载并使用的版本是：**go-ipfs Version v0.4.13 for OS X 64bit**

## IPFS 安装

![](http://daijiale-cn.oss-cn-hangzhou.aliyuncs.com/djl-blog-pic/ipfs/ipfs_install1.png)

```
ipfs --help  //打开命令行，输入，出现Log信息时，表示安装成功
```
## IPFS本地部署

### 创建节点

在本地全局目录下新建仓库：

![](http://daijiale-cn.oss-cn-hangzhou.aliyuncs.com/djl-blog-pic/ipfs/ipfs_init.png)

### 节点配置

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

### 节点ID

每个节点都会存在一个唯一标识，查看节点ID方式如下：

```

ipfs id
```

### 启动节点服务器

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

### 配置CORS跨域资源共享

为了方便后续前端的开发和数据访问，提前对跨域资源共享`CORS`进行配置，`ctrl-c` 退出`ipfs`，然后按照下面的步骤进行跨域配置：

```
ipfs config --json API.HTTPHeaders.Access-Control-Allow-Methods '["PUT", "GET", "POST", "OPTIONS"]'

ipfs config --json API.HTTPHeaders.Access-Control-Allow-Origin '["*"]'
```

### 验证

浏览器打开 <http://localhost:5002/webui> ，出现Web Console 图形化控制台

![](http://daijiale-cn.oss-cn-hangzhou.aliyuncs.com/djl-blog-pic/ipfs/webui-connection.png)

这里可以看到所有run在主网上的节点信息，和本地节点相关的配置数据。


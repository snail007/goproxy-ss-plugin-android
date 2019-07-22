# ss goproxy安卓插件
 
### 数据流
为了方便理解插件怎么工作的，下面对使用插件前后流量走向做个对比

#### 使用插件前

```text
本地VPN -》本地SS-》----互联网------》SS服务器
```

#### 使用插件后

```text
本地VPN -》本地SS-》本地goproxy-》----互联网------》goproxy服务器
```

对比可以发现，使用了goproxy插件之后，实际上设备出去对流量都是goproxy控制的，也就是说可以使用goproxy的各种传输协议和服务了。

#### 使用说明  
1.安装官方ss客户端。  
2.安装ss goproxy插件。  
3.在官方客户端里面新建一个服务端，填写规范如下：  
3.1 服务器IP、端口、加密方法、密码正常填写，需要注意的是加密方法要填写goproxy的sps支持的加密方法。  
3.2 最下面`插件`选择`ShadowsocksGoProxyPlugin`。  
3.3 配置参数：填写goproxy的sps启动参数即可。  
3.4 需要注意的是，填写goproxy的sps启动参数里面的-p和-P是不需要填写的，如果-T是ws或者wss依赖域名可以加上-P参数，另外必须用-h和-j指定上面填写的加密方法和密码。  

#### 示例

假设上级(IP为1.1.1.1)执行的命令是：`proxy socks -t ws -p :8800`  
ss客户端新建里面填写：  
服务器IP：1.1.1.1  
端口：8800  
加密方法：aes-256-cfb  
密码：123  
插件配置参数：`-S socks -T ws -h aes-256-cfb -j 123`  

<img src="/doc/1.png" widht="300px" >

<img src="/doc/2.png" widht="300px" >


#### 使用了WS和CDN示例

假设上级执行的命令是：`proxy socks -t ws -p :8800`  
CDN域名是：test.com  
ss客户端新建里面填写：  
服务器IP：test.com  
端口：8800  
加密方法：aes-256-cfb  
密码：123  
插件配置参数：`-S socks -T ws -h aes-256-cfb -j 123 -P test.com:80`   

<img src="(/doc/3.png" widht="300px" >

<img src="(/doc/4.png" widht="300px" >


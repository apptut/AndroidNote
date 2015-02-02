## 手机抓包工具

这里推荐两款比较经典的手机抓包工具（当然不光是手机开发使用，Web开发也适用）：

1. `Fiddler` windows平台下强大的抓包工具（其实也有其他平台，但是很挫），Mac不好用
2. `Charles` Mac下可以使用这个，缺点是它是个收费的软件。

##### 1. 使用`Fiddler`抓取手机数据包

使用这个软件如何抓取手机上数据包，网上资料一堆，百度谷歌一下即可，推荐一个介绍比较详细的文章：<http://www.trinea.cn/android/android-network-sniffer/>

需要说明的是，使用这个工具抓取手机数据包，你需要做一些额外设置（默认是不支持手机抓包的），勾选以下内容，然后重启`Fiddler`即可

```
Connections -> Allow remote computers to connect
```

具体使用说明，请参考参考上述链接地址，如果链接有损坏，请及时联系我。

官网网址：<http://www.telerik.com/fiddler>

##### 2. 使用`Charles`抓取手机数据包

和`Fiddler`用法类似，这个软件默认开启了远程网络请求功能，因此软件本身不需要做任何设置，直接设置手机代理即可。

具体使用方法，可参考这篇文章：<http://blog.devtang.com/blog/2013/12/11/network-tool-charles-intr/>

还是那句老话，如果链接能使用，你能看到具体这个软件使用方法，虽然作者文章中是针对`IOS`开发的，但是也适用于`Android`开发，如果链接无法打开，请及时联系我。

官方网址：<http://www.charlesproxy.com/>


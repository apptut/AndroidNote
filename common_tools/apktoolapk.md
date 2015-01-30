## apktool反编译apk包

其实去反编译别家的apk不是很道德，但是有时候我们可能需要反编译自家的apk，查看里面的一些信息，`apktool`可以用来反编译apk查看其中的资源文件：

1. 官网下载安装，<http://code.google.com/p/android-apktool/>和`apktool mac`命令包`apktool-install-macosx-r05-ibot.tar.bz2`
解压，拷贝 两包下所有文件到 /usr/local/bin/ 目录。

2. 反编译命令：

```js
apktool d [demo.apk]  // 参数是 d 而不是 -d。
```

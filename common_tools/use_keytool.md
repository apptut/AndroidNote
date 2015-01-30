## 使用 keytool 查看签名

对于一个完整的Apk包，可能我们最常用的需要查看当前Apk的签名信息，或者`md5`密钥，最方便的是使用`keytool`工具：

```sh
keytool -list -keystore ~/tools/app.keystore

// 然后根据提示输入keystore密钥即可
```

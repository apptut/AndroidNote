## 获取url参数


```java
String url = "http://apptut.com/?param=123";
Uri srcUri = Uri.parse(url);

// 获取param的值
String value = srcUri.getQueryParameter("param");
```

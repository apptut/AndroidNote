## 时间字符串格式化

一般来说服务端会把格式化的字符串输出给客户端，一般不需要客户端自己来处理，但是总有特殊的时候，所以整理了一些常用的时间格式化场景：

使用`SimpleDateFormat`格式化时间:

#### 1. 场景一

```java
// 解析 2015-01-18T09:47:26.000+0000 字符串

Date date = new SimpleDateFormat("yyyy-MM-dd'T'HH:mm:ss.SSSZ").parse(jsonObject.optString("createDate"));
// 重新输出新格式
String time = new SimpleDateFormat("yyyy-MM-dd HH:mm E").format(date);

//解析后为: 2015-01-18 09:47 周日
```

#### 2. 格式化毫秒值

```java
public String getTimeStr(long timestamp){
    return new SimpleDateFormat("yyyy-MM-dd").format(new Date(timestamp));
}
```

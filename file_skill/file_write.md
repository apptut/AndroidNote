## 文件写入


### 写入字符串数据到文件

```java
try {
	// 包中创建一个私有缓存文件
	File file = new File(cacheDir, fileName);
	// 创建写入流，如果文件不存在自动创建
	FileOutputStream fileOutputStream = new FileOutputStream(file);

    // 获取字符串utf-8字节，防止乱码问题
	fileOutputStream.write(sortCache.getBytes("UTF-8"));
	fileOutputStream.close(); // 关闭流数据

	}catch (IOException e) {

}
```

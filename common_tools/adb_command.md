## 常用adb命令

了解一些常用的adb命令，会给开发带来便利，我经常会使用下面的命令：

#### 1. adb push 命令使用

推送电脑文件到手机目录

     格式：adb push <电脑目录> <手机目录>

     例如：adb push  ~/Desktop/000.jpg  /sdcard/

**注意**：

手机目录必须以 / 结尾，并且关闭手机和电脑的 USB存储设备 连接选项。如果拷贝电脑上整个目录下的文件，到手机某个目录，那么电脑文件夹不需要加/。

例如：adb push ~/Desktop/test /sdcard/test    拷贝test目录下所有内容到 手机test目录

#### 2. adb 删除手机文件

与其说是adb命令，还不说删除其实是shell命令，android手机其实就是linux码：

  1. adb shell   使用shell命令
  2. su 获取root权限
  3. cd /sdcard/
  4. rm -r XXX.file 文件

#### 3. 安装与卸载

安装apk

     adb install [文件名称.apk]

     重新安装该软件
     adb install -r apk文件名称.apk

卸载apk软件

     adb uninstall apk包名.apk


**安装卸载注意**

可能直接使用adb install不会成功，或许需要你使用sudo方式：

```
sudo adb install [文件.apk]
```

甚至需要root你的手机，如何root手机将会在下一节介绍。

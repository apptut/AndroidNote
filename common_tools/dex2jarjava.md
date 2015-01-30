## dex2jar反编译java

`apktool`只能反编译apk包中的资源文件，其中的`java`文件不能被反解为汇编语言，所以如果要看包里的java文件，需要用这个软件：

首先需要下载`dex2jar`脚本，百度即可

     a) 更改需要反编译的 demo.apk 为 demo.zip，然后unzip demo.zip包
     b) 然后执行 sh dex2jar.sh class.dex。
     c) 使用 js-GUI 工具查看 class.dex解压过的jar包文件即可。


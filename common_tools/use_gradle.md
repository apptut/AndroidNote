## 使用Gradle插件

![gradle logo](../images/gradle-logo.gif)

从`Eclipse`转到`Android Studio`后，免不了与`Gradle`打交道，掌握一些常用的`Gradle`使用方法，是自动化打包（apk包）变得很方便。

需要说明的是，`Android Studio`集成的是`Gradle`专为`Android`开发的插件，使用这个插件，只需要我们添加一些默认的配置，或者一些自动化任务，我们就能完成类似于自动生成多渠道包、签名、添加版本号等。

`Gradle`本身能干很多事情（不光是android自动化构建），但是作为`Android`开发人员来说，我们只需要了解于如何在`Android`开发中做一些自动化部署的知识即可，如果你需要掌握更多关于`Gradle`的知识，请移步于官网：<https://gradle.org/>

#### 1. Gradle常用的情景

现在我们关注`Gradle`经常用到的情景，当前使用`Gradle`插件版本为：

```sh
gradle-version: 2.2.21
```

**1.1 基本配置字段**

```sh
android {
    compileSdkVersion 19
    buildToolsVersion '19.1.0'

    defaultConfig {
        applicationId "com.example.app"
        minSdkVersion 8
        targetSdkVersion 19
        manifestPlaceholders = [channelValue: "6"]
        versionCode 1
        versionName "1.0"
    }
    # ...
}
```
`compileSdkVersion` 表示当前参与编译的sdk版本，以及参与编译工具（`buildToolsVersion`）所对应的版本。

`defaultConfig`字段用来配置设置一些常用配置字段，如果设置此模块下相应字段，那么在打包的时候，会自动替换调`AndroidManifest.xml`中的相应字段。(需要注意)

这个模块下有一个字段需要特别说明：`manifestPlaceholders`，此字段用来动态替换`AndroidManifest.xml`所设置的占位符内容，对于构建多渠道包非常有好处，例如,我们现在需要把不同渠道id在打包时自动生成到`AndroidManifest.xml`中，那么可以这样：：

```xml
<!-- AndroidManifest.xml 占位符-->
<meta-data
    android:name="com.example.app"
    android:value="${channelValue}" />
```
然后再`build.gradle`中替换掉：

```sh
manifestPlaceholders = [channelValue: "6"] #可以多个参数，参数名自定
```
至于当前模块下其他参数内容很明了，无需详说，需要再次强调的这些字段会最终替换调`AndroidManifest.xml`的字段（切记，切记！！！）

**1.2 签名字段**

该模块下用来设置设置签名密钥相关字段，但是这里唯一觉得不足的是暴露了密钥文件以及密码，但是也没办法，自动化就得知道这些。

```sh
release {
    storeFile file("keystore/android.keystore")     #签名文件位置
    storePassword "A7HbvETmGSj8WEKJZC"              #存储密码
    keyAlias "android.keystore"                     #别名
    keyPassword "A7HbvETmGSj8WEKJZC"                #签名密码
}
```

**1.3 buildTypes**

`buildTypes`用来指定最终编译字段配置。

```
release {
        minifyEnabled true                      #是否压缩
        proguardFiles 'proguard.cfg'            #是否混淆
        signingConfig signingConfigs.release    #签名

        // 定制不同渠道修改此处即可 覆盖defaultConfig 渠道字段后的release包
        // manifestPlaceholders = [channelValue: "6"]
}
```

**1.4 sourceSets资源配置**

该字段下主要配置一些项目资源路径。

**1.5 productFlavors渠道包字段**

该字段用来打不同的渠道包，如果不同的渠道包下有不同的文件需要合并，那么只需要在`src/`目录下建立以渠道名作为根目录的根目录即可：

```sh
#自定义两个渠道，渠道名为Channel123，Official渠道
"Channel123"{
    manifestPlaceholders = [channelValue: "1"]
}
// 官方渠道
"Official" {
    manifestPlaceholders = [channelValue: "6"]
}

```
如上述描述两个渠道，如果说两个渠道的某些项目文件不一样，那么可以以各自的渠道名作为根目录建立各自不同的项目文件路径即可：

```sh
src/
    main/
        #全局的代码
        images/     #假设有一个图片文件下有俩文件
            a.png
            b.png
    Channel123/
        #此频道下自己不同的文件（任何文件），覆盖main下文件即可,相同的文件路径
        images/
            a.png   #如果a.png不一样，那么直接覆盖即可

    Offcial/
        #类比Channel123
```


**2. gradle示例模板：**

```sh
// 添加打包生成apk的时间
import java.text.DateFormat
import java.text.SimpleDateFormat

def getDateTime() {
    DateFormat df = new SimpleDateFormat("YYYY_MM_dd_HH_mm",Locale.US);
    return df.format(new Date());
}

android {
    compileSdkVersion 19
    buildToolsVersion '19.1.0'

    defaultConfig {
        applicationId "com.example.app"
        minSdkVersion 8
        targetSdkVersion 19
        manifestPlaceholders = [channelValue: "6"]
        versionCode 1
        versionName "1.0"
    }

    # 设置包签名字段
    signingConfigs {
        release {
            storeFile file("keystore/android.keystore")
            storePassword "A7HbvETmGSj8WEKJZC"
            keyAlias "android.keystore"
            keyPassword "A7HbvETmGSj8WEKJZC"
        }

        # 此处可以做其他自定义任务
    }

    buildTypes {
        release {
            minifyEnabled true
            proguardFiles 'proguard.cfg'
            signingConfig signingConfigs.release

            // 定制不同渠道修改此处即可 覆盖defaultConfig 渠道字段后的release包
            // manifestPlaceholders = [channelValue: "6"]
        }

        debugDaily {
            debuggable true
            minifyEnabled false
            signingConfig signingConfigs.dailybuild
            applicationVariants.all { variant ->
                variant.outputs.each { output ->
                    def file = output.outputFile
                    output.outputFile = new File(file.parent, file.name.replace(".apk", "-" + defaultConfig.versionName + "-" + getDateTime() + ".apk"))
                }
            }
        }
    }

    sourceSets {
        main {
            jniLibs.srcDirs = ['libs'] //ndk编译目录，默认是main/jniLibs/
        }
    }

    //渠道包打包例子
    productFlavors {
        #自定义渠道，渠道名为Channel123
        "Channel123"{
            manifestPlaceholders = [channelValue: "1"]
        }
        // 官方渠道
        "Official" {
            manifestPlaceholders = [channelValue: "6"]
        }
    }

}

# 第三方依赖
dependencies {
    compile 'com.android.support:support-v4:19.1.0'
    compile 'com.nineoldandroids:library:2.4.0'
    compile 'com.loopj.android:android-async-http:1.4.6'
}

```



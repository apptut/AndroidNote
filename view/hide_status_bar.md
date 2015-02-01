## 隐藏状态栏

网上有很多关于如何隐藏状态栏的代码，但大部分都是需要重新启动当前的Activity,这样做有时候让人很郁闷，然而使用下面的代码可以避免重启，经测试`Android 2.3+` 都能奏效：

**隐藏状态栏:**

```java
WindowManager.LayoutParams lp = getWindow().getAttributes();
lp.flags |= WindowManager.LayoutParams.FLAG_FULLSCREEN;
getWindow().setAttributes(lp);
getWindow().addFlags(WindowManager.LayoutParams.FLAG_LAYOUT_NO_LIMITS);
setRequestedOrientation(ActivityInfo.SCREEN_ORIENTATION_LANDSCAPE);
```

**显示状态栏:**

```java
WindowManager.LayoutParams attr = getWindow().getAttributes();
attr.flags &= (~WindowManager.LayoutParams.FLAG_FULLSCREEN);
getWindow().setAttributes(attr);
getWindow().clearFlags(WindowManager.LayoutParams.FLAG_LAYOUT_NO_LIMITS);
```

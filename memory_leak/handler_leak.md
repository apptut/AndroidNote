# handler潜在问题

使用handler时建议使用软引用和静态类，避免内存溢出，这是Google官方的建议，IDE自动提示也会发出相关内存溢出警告：

```java
// 改进前的代码
private Handler myHandler = new Handler(){
    @Override
    public void handleMessage(Message msg) {
        // some code
    }
};

```
上述代码可能会造成内存溢出，因此建议采用下面的方式：

```java
// 改进后的代码
private Handler myHandler = new MyHandler(this);
private static class MyHandler extends Handler{
    private WeakReference<AboutActivity> owner;

    private MyHandler(AboutActivity aboutActivity) {
        this.owner = new WeakReference<AboutActivity>(aboutActivity);
    }

    @Override
    public void handleMessage(Message msg) {
        AboutActivity aboutActivity = owner.get();

        if(aboutActivity == null) return;

        // 调用当前类对象的一些方法
        aboutActivity.onDestroy();
    }
}
```

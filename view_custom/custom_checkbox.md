## 自定义checkbox

###1.1 自定义checkbox 选中图片

自定义checkbox使用的时`android:background`而不是`android:button`，原因在于使用`button`时自定义图片过大超出边缘部分会截断，而使用`background`时会自由拉伸。

####1.1.1 自定义button图片

```xml
<?xml version="1.0" encoding="utf-8" ?>
<selector xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:drawable="@drawable/usercenter_delete_havor" android:state_checked="true" />
    <item android:drawable="@drawable/usercenter_delete_default" android:state_checked="false" />
    <item android:drawable="@drawable/usercenter_delete_default" />
</selector>
```
####1.1.1 自定义checkbox样式

```xml
<style name="VideoDownloadCheckbox" parent="@android:style/Widget.CompoundButton.CheckBox">
    <item name="android:button">@null</item>
    <item name="android:background">@drawable/usercenter_delete_selector</item>
</style>
```
####1.1.3 使用

```xml
<CheckBox
    android:layout_width="25dp"
    android:layout_height="25dp"
    style="@style/VideoDownloadCheckbox" />
```

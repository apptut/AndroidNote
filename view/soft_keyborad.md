## 软键盘操作

软件盘常用操作方法。

#### 1.1 隐藏软件盘

```java
EditText editText = findViewById(R.id.editView);
InputMethodManager inputManager = (InputMethodManager) editText.getContext().getSystemService(Context.INPUT_METHOD_SERVICE);
inputManager.hideSoftInputFromWindow(editText.getWindowToken(), 0);
```
#### 1.1 显示软件盘

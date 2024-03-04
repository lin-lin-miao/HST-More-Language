# 计算器插件

可使用JavaScript拓展应用程序

## 自定义Prompt() Confirm() Alert()

使用字段码    js/:title=自定义标题/:msg=自定义消息

调用字段为    js/:  分隔符为 /:

除    js/:    外其它字段可乱序

不使用则为默认标题

## api调用

未完全实现，未来可能会发生变化，有其它需求可在Issues提出或与作者联系

### 使用反射机制

默认无返回值

反射类名为: App

调用示例

```javascript
App.Toast(strs);
```

|函数名|结果|
|--|--|
|Toast(String msg)|与应用Toast一致|
|permission(String msg, String value)|对插件的设置，msg为设置函数名，value为设置值|

permission 可设置的函数

- setAppCacheEnabled
- setAppCachePath
- setDatabaseEnabled
- setJavaScriptCanOpenWindowsAutomatically

### 使用Prompt()函数

有返回值

调用示例

```javascript
prompt("js/:api=i18n/:mes=计算器")
```

api值为需要调用的函数名，

若无api值则为自定义输入框

调用值可乱序

若执行失败返回 defaultValue

|函数名|所需参数|返回|结果|
|--|--|--|--|
|i18n|mes=String|String|使用app加载的翻译文件进行翻译|
|name|null|String|返回插件名称|
|version|null|String|返回app版本|

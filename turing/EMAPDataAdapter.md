# EMAP DataAdapter

与 EMAP 后端模型对接的 DataAdapter

turing 挂载于 window["tg-turing"] 中

```js
var turing = window["tg-turing"];
```

使用 DataAdapterFactory 中默认为创建 EMAP 类型的 DataAdapter

## 功能示例

### 已有模型定义

```js
var inst = new turing.DataAdapterFactory.create(pageMeta, "T_FUNA_USER_QUERY");
inst.view("grid:table");
```

### 动态加载页面模型

```js
var inst = new turing.DataAdapterFactory.create();
inst.load("url", "T_FUNA_USER_QUERY")
```

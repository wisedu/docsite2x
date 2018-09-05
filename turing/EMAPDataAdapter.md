# EMAP DataAdapter

与 EMAP 后端模型对接的 DataAdapter

turing 挂载于 window["tg-turing"] 中

```js
var turing = window["tg-turing"];
```

使用 DataAdapterFactory 中默认为创建 EMAP 类型的 DataAdapter

## 初始化方式

### 已有模型定义

```js
var inst = new turing.DataAdapterFactory.create(pageMeta, "T_FUNA_USER_QUERY");
inst.view("grid:table");
```

### 动态加载页面模型

```js
var inst = new turing.DataAdapterFactory.create();
inst.load("url", "T_FUNA_USER_QUERY")
let columns = inst.view("默认列表:table")
```

### 加载流程合并的模型

```js
var inst = new turing.DataAdapterFactory.create();
inst.getIntegratedModel("url", "T_FUNA_USER_QUERY")
let fields = inst.view("默认表单:form")
```


## 数据查询

### 获取数据 findAll

findAll 默认会在加载模型后，自动映射动作名称后缀为 `_query` 的动作作为请求地址。

如果需要更换默认的 findAll 请求地址，需要调整其 url 地址，以下给出示例：

```js
//调整默认 findAll 的请求地址
inst.actions["find"].url = "";

inst.findAll({ parentId:"00001" }).then(datas => {
    this.rowData = datas
});
```


### 查询数据动态条件 querySetting

与 EMAP 动态条件对接

```js
/**
 * Dept.vue：
 * this.searchValues = {"字段":"值","User.字段":"值"}
 * 
 * */
methods: {
    query() {
        inst.querySetting = inst.querySettingBuilder(this.searchValues);
        inst.findAll().then(datas => {
            this.data5 = datas;
        });
    },
}
/**
 * 提交值：
 * {
 *   querySetting:{ "Dept":{"字段":"值"},"User":{"字段":"值"} }
 *   where:{...}
 * }
 * */
```

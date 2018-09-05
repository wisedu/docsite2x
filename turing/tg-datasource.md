# DataAdapter 数据适配组件

虽然下面满篇都是 DataSourceManager，但是我想告诉你的是，这是使用 DataAdapter 来操作 DataSource 的方式。
而 DataSource 本身仅仅就是一个结构化数据。

> 底层使用的是 tg-turing，[说明文档](https://github.com/wisedu/turing)

## 功能说明

### 在页面定义数据集
定义的数据集，取页面模型中所有的定义，缓存到本地以便调用。
参数 `hqjxjzlbgsj` 是这个模型集合中作为默认模型的名称
参数 `pageMeta` 是模型集合，从EMAP页面模型获取
参数 `{userid:"aa"}` 是默认模型的查询动作所带的参数。即：findAll 方法的默认参数，自动存储在 actions.find.params 中

```js
var hqjxjzlbgsj = new window["tg-turing"].DataSourceManager("hqjxjzlbgsj", pageMeta, {userid:"aa"});
window["tg-turing"].DataSourceManager.set(hqjxjzlbgsj);
```

### 框架运行时，初始化数据集。

这个步骤一般你不会关心，由框架代理完成

```js
window["tg-turing"].DataSourceManager.ready(function() {
  //数据集已经准备完毕，启动页面js
})
```

### <span style="color:red">***</span> 业务代码获取并执行获取数据

DataSourceManager.get 方法是从本地缓存获取DataSource对象的引用，不会再次发送请求和构造对象，没有性能消耗

```js
var testDS = window["tg-turing"].DataSourceManager.get("hqjxjzlbgsj");
//读取默认模型（hqjxjzlbgsj）的取数据地址
testDS.findAll({"参数1":"1"}).then(function(result){
  console.log(result)
  debugger
});

//findAll方法等同于执行以下方法，当然你也可以执行其他action
testDS.actions.find.params = Object.assgin({"参数1":"1"}, testDS.actions.find.params)
testDS.execute(testDS.actions.find).then(function(result){
  console.log(result)
  debugger
});

//完全自定义的执行也是可以的
emapDS.execute({url:"http://res.wisedu.com/fe_components/mock/table.json", method:"get", params:{}}).then(function(result){
  console.log(result)
  debugger
});
```

### 不需要模型，仅发请求

也有两种方式：

1、 利用 DataAdapter 组件进行数据请求

使用该方法，如果url是相对路径，会自动拼装 `window.apiPath` 的前缀，形成完整路径发送数据请求

```js
var ds = window["tg-turing"].DataAdapterFactory.create();
ds.execute({url:"http://res.wisedu.com/fe_components/mock/table.json", method:"get", params:{}}).then(function(result){
  console.log(result)
  debugger
});
```

2、 使用 axios 进行数据请求

```js
window["tg-turing"].axios.get(url, {params: params}).then(function(result){
  console.log(result)
  debugger
});

window["tg-turing"].axios.post(url, params).then(function(result){
  console.log(result)
  debugger
});
```

## API

### Methods

| 方法名称 | 说明 | 参数 |
|---------- |-------- |---------- |
| execute  | 异步请求数据方法 | `action对象`, `{查询参数1:1,查询参数2:2}`  |
| findAll  | 以actions.find为参数，执行异步请求 | `{查询参数1:1,查询参数2:2}`  |
| getMeta  | 获取原始模型 | 无  |
| load  | 通过远程地址加载模型（手动构建DataSource时使用） | `uri`远程地址, `modelName`默认模型名称, `findParams`默认actions.find的参数  |
| refresh  | 根据传入的数据，刷新模型（手动构建DataSource时使用） | `data`原始模型数据, `modelName`默认模型名称, `findParams`默认actions.find的参数  |

DataSource 是数据结果，而我们所操作的对象实际上是 DataAdapter，由它简化数据的操作
该对象的实例化已由 DataAdapterFactory 对象代理，这样以便屏蔽底层使用的是EMAP的数据源或者三方的数据源。

```js
//refresh 调用示例
var inst = window["tg-turing"].DataAdapterFactory.create(pageMeta, name, findParams);

//load 调用示例
var inst = window["tg-turing"].DataAdapterFactory.create();
inst.load(url, name, findParams)
```

### 属性

属性是通过初始化后，自动生成，无需手动创建。
以结构体来说明

```js
console.log(testDS.actions)

{
    "save":{
        "url": "",
        "method": "post",
        "name": ""
    },
    "delete":{
        "url": "",
        "method": "post",
        "name": ""
    },
    "find":{
        "url": "./bbb/EMAP_SYS_VERSION_INFO_QUERY.do",
        "method": "get",
        "name": "EMAP_SYS_VERSION_INFO_QUERY",
        "params":{
            "bbb": "aa",
            "pageSize": 10,
            "pageNumber": 1
        }
    },
    "EMAP_SYS_VERSION_INFO_QUERY":{
        "url": "bbb/EMAP_SYS_VERSION_INFO_QUERY.do",
        "method": "post"
    }
}
```


### Events

| 事件名称 | 说明 | 回调参数 |
|---------- |-------- |---------- |
| onLoad  | 数据加载完成时触发 | `meta`原始模型  |
| onLoadMeta  | 加载控件模型时触发，用于对控件模型做干预 | `controls`控件模型集合  |

示例代码

```js
var inst = window["tg-turing"].DataAdapterFactory.create();
inst.onLoad = function(meta){
  //做处理
  return meta;
}
inst.onLoadMeta = function(controls){
  //做处理
  return controls;
}
inst.load(url, name, findParams)
```

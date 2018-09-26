# 工具

turing 挂载于 window["tg-turing"] 中

```js
var turing = window["tg-turing"];
```

## 公共方法

### utils.Post

该方法封装了 Axios

```js
window["tg-turing"].utils.Post("url", {key1:"value1",key2:"value2"}).then(result => {
    console.log(result.data)
});
```

* @param {String} url - 请求地址，可以是api中定义的名称，或者具体的url地址
* @param {Object} data - 请求参数
* @param {*} config - 请求配置，详见axios文档 [https://github.com/mzabriskie/axios]


### utils.Get

```js
window["tg-turing"].utils.Get("url", {key1:"value1",key2:"value2"}).then(results => {
    console.log(result.data)
})
```

 * @param {String} url - 请求地址，可以是api中定义的名称，或者具体的url地址
 * @param {Object} data - 请求参数
 * @param {*} config - 请求配置，详见axios文档 [https://github.com/mzabriskie/axios]；


### utils.Delete

```js
window["tg-turing"].utils.Delete("url", {key1:"value1",key2:"value2"}).then(results => {
    console.log(result.data)
})
```

 * @param {String} url - 请求地址，可以是api中定义的名称，或者具体的url地址
 * @param {Object} data - 请求参数
 * @param {*} config - 请求配置，详见axios文档 [https://github.com/mzabriskie/axios]；


### utils.getUrlParam

```js
// url = res.wisedu.com?aa=1&bb=2
let params = turing.utils.getUrlParam(); //获取所有url上的参数
// 结果：params = {aa:1,bb:2}

let aa = turing.utils.getUrlParam("aa"); //直接获取某一个的值
// 结果：1
```

 * @param {String} name [可选]] - 获取参数名称


### utils.setFullUrl

### utils.getContextPath

### utils.cleanProps

### utils.toTreeData

```js
let datas = [{
    "text": "基本信息维护",
    "id": "1",
    "parentid": "-1",
    "value": "$2.3"
},
{ "id": "2",
    "parentid": "1",
    "text": "新增",
    "value": "$2.3"
}, {
    "id": "3",
    "parentid": "1",
    "text": "删除",
    "value": "$2.3"
}, {
    "id": "4",
    "parentid": "1",
    "text": "编辑",
    "value": "$2.3"
}, {
    "id": "5",
    "parentid": "1",
    "text": "上传附件",
    "value": "$2.3"
},  {
    "id": "11",
    "text": "信息历史查询",
    "parentid": "-1",
    "value": "$2.3"
}, {
    "id": "7",
    "parentid": "11",
    "text": "导出",
    "value": "$2.3"
}, {
    "id": "8",
    "text": "附件",
    "parentid": "11",
    "value": "$2.3"
}];
let datas = turing.utils.toTreeData(datas, "-1", {ukey:"id", pkey:'parentid', toCKey:'children'})
```

 * @param {Object} data - 树的平铺数据
 * @param {String} parent_id - 树的根节点值
 * @param {ukey,pkey,toCKey} options - ukey:唯一主键字段名，pkey:关联父节点字段名，toCKey:产生的子节点字段名称


### utils.extend

```js
var object = turing.utils.extend({}, object1, object2, objectN); //浅拷贝
var object = turing.utils.extend(true, object1, object2, objectN); //深拷贝
```

与jQuery的extend用法一致

 * @param {Boolean} deep [可选] - 深度拷贝
 * @param {Object} object1 - 待合并的对象
 * @param {Object} objectN - 将合并的对象


## 过滤器

### 日期 date

### 大写 uppercase

### 小写 lowercase

### 货币 currency

### 百分数 percent


## 指令

### 控件权限过滤 tg-funckey


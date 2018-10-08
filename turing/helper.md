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
// url = http://res.wisedu.com?aa=1&bb=2
let params = turing.utils.getUrlParam(); //获取所有url上的参数
// 结果：params = {aa:1,bb:2}

let aa = turing.utils.getUrlParam("aa"); //直接获取某一个的值
// 结果：1
```

 * @param {String} name [可选]] - 获取参数名称


### utils.getContextPath

```js
// http://localhost:8080/emap/sys/eetablemanage/Capacity/design.do?tgloader=pc
let context = turing.utils.getContextPath();
// 结果： http://localhost:8080/emap
```

### utils.cleanProps

```js
let value = {a:1,b:1,c:1};
let newdata = turing.utils.cleanProps(value);
// 结果： newdata = {};
```

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

```html
<!-- 在双花括号中 -->
{{ brithday | date }}

<!-- 在 `v-bind` 中 -->
<div v-bind:id="brithday | date('YYYY-MM-DD')"></div>
```

* 参数[可选] - 日期格式：YYYY-MM-DD 或其他格式，参考 [momentjs 文档](http://momentjs.cn/docs/#/parsing/string-format/)

### 大写 uppercase

```html
<!-- 在双花括号中 -->
{{ company_name }}

<!-- 在 `v-bind` 中 -->
<div v-bind:id="company_name | uppercase "></div>
```

### 小写 lowercase

```html
<!-- 在双花括号中 -->
{{ my_name }}

<!-- 在 `v-bind` 中 -->
<div v-bind:id="my_name | lowercase"></div>
```

### 货币 currency

```html
<!-- 在双花括号中 -->
{{ amount }}

<!-- 在 `v-bind` 中 -->
<div v-bind:id="amount | currency('$')"></div>
```

* 参数[可选] - symbol： 货币符号，默认值：'￥'
* 参数[可选] - format： 值与符号的先后顺序以及其中的格式，默认值：'%s%v'。  %s = symbol, %v = value/number
* 参数[可选] - precision： 小数位数，默认值：2
* 参数[可选] - thousand： 千分位符号，默认值：','
* 参数[可选] - decimal： 小数符号，默认值：'.'


## 指令

### 控件权限过滤 

在不具备权限的情况，把当前元素彻底remove掉。

该指令依赖数据源：

```js
window.sessionStorage.setItem("tg-authkeys", "func1,func2,func2,func2")
```

```html
<div tg-funckey="'func1'"><button>审核</button></div>
```


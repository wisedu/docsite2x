# 工具

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

### utils.setFullUrl

### utils.getContextPath

### utils.cleanProps

### utils.toTreeData

### utils.extend


## 过滤器

### 日期 date

### 大写 uppercase

### 小写 lowercase

### 货币 currency

### 百分数 percent


## 指令

### 控件权限过滤 tg-funckey


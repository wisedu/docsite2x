# tg-form

该组件是弹窗中的输入项的集合，可以放置在弹窗中 或者 平铺在页面上

通过模型生成表单，主要特性：

* 排列方式：1列、2列、3列、4列 ...
* 组织形式：平铺、分组
* 显示形式：可填写、只读、混排

可以根据实现组件，切换显示组件，以下为PC端的iview组件库的实现。亦或是可以切换为移动端组件库

[formConnector](https://github.com/wisedu/turing/blob/master/formConnector.md)

## 功能

### 2列/只读/平铺 表单

![2列只读表单](../static/form-2-readonly.png)

```html
<tg-form :fields="fields" v-model="formData" :column="2" :readonly="true"></tg-form>
```

#### 平铺表单数据格式

```js
let fields = [
    {"name":"WID","xtype":"text","caption":"WID"},
    {"name":"ACCOUNTID","xtype":"text","caption":"登录账号","dataSize":40}
    ...
]
```

### 弹窗内的 2列/可编辑/分组 表单

![弹窗内的2列表单](../static/form-2cols.png)

```html
<Modal v-model="isModalShow" title="用户信息" @on-ok="ok" @on-cancel="cancel" :width="800">
    <tg-form :fields="fields" v-model="formData" :column="2"></tg-form>
</Modal>
```

#### 分组表单数据格式

```js
let fields = [
    {
        "name":"group:[基本信息]",
        "title":"基本信息",
        "desc":"~基本信息~",
        "items":[
            {"name":"ACCOUNTID","xtype":"text","caption":"登录账号","dataSize":40}
            ...
        ]
    },{
        "name":"group:[附加信息]",
        "title":"附加信息",
        "desc":"~附加信息~",
        "items":[
            {"name":"USERTYPE","url": "/axsfw/code/12eb4f7c-69a1-41c2-b21e-c99fe850264a.do","xtype": "select","dataSize": 6}
            ...
        ]
    },
    ...
]
```

### 页面内的 3列/可编辑/平铺 表单

![页面内的3列表单](../static/form-3cols.png)

```html
<tg-form :fields="fields" v-model="formData" :column="3">
    <div slot="after">
        <FormItem>
            <Button @click="search" type="primary" shape="circle" icon="ios-search">查询</Button>
            <Button @click="clear" type="default" shape="circle">清空</Button>
        </FormItem>
    </div>
</tg-form>
```

## 提交表单数据

### 异步附件提交

附件需要使用异步上传组件，如：uploadfile

```html
<template>
    <tg-form :fields="fields" v-model="formData" :column="2" :readonly="true"></tg-form>
    <button @click="submit"></button>
</template>
<script>
export default {
    data(){
        return {
            fields: [{name:"attachment",caption:"附件",xtype:"uploadfile"}]
            formData: {}
        }
    },
    methods:{
        submit(){
            window["tg-turing"].utils.Post("后台地址", formData).then(result => {
                console.log(result.data)
            })
        }
    }
}
</script>
```

### 同步附件提交

附件需要使用同步上传组件，如：uploadfile-sync

```html
<template>
    <tg-form ref="form" :fields="fields" v-model="formData" :column="2" :readonly="true"></tg-form>
    <button @click="submit"></button>
</template>
<script>
export default {
    data(){
        return {
            fields: [{name:"attachment",caption:"附件",xtype:"uploadfile-sync"}]
            formData: {}
        }
    },
    methods:{
        async submit(){
            let result = await window.$refs.form.submit("后台地址");
            console.log(result);
        }
    }
}
</script>
```

以上的 `后台地址` 是通过POST enctype=multipart/form-data 方式提交的，需要在后台接收该请求并以 multipart 方式获取参数。

由于同步提交机制，需要该后台 controller 需要返回一个标准格式内容，以供前台获取结果。模板如下

```html
<html><script>parent.postMessage({key1:"value1",key2:"value2",key3:"value3"}, '*')</script></html>
```

## 高级

### 替换表单字段内容

这样可以将fields模型中XSBH的字段显示替换为 sortable 的自定义组件

```html
<tg-form :fields="fields" :column="4" :value="data" displayFieldFormat="_DISPLAY">
    <div slot="XSBH">
        <ul id="sortable">
            <li class="ui-state-default">Item 1</li>
            <li class="ui-state-default">Item 2</li>
            <li class="ui-state-default">Item 6</li>
            <li class="ui-state-default">Item 7</li>
        </ul>
    </div>
</tg-form>
```


### 表单最后追加项

```html
<tg-form :fields="fields" :value="formValue">
    <div slot="after">
        <FormItem>
            <Button @click="search" type="primary" shape="circle" icon="ios-search">查询</Button>
            <Button @click="clear" type="default" shape="circle">清空</Button>
        </FormItem>
    </div>
</tg-form>
```


### 组件的全局默认参数

es5 运行时修改，需要在入口JS初始化时设置，以保证全局默认值在tg-form初始化之前就生效

```js
window["tg-turing"].defaults.antd.form["date"].format = "yyyy-MM-dd"
```

es6 需要在入口index.js中，注册组件库的同时，进行全局默认值设置

```js
import tgTuring from 'tg-turing';
Vue.use(tgTuring);
window["tg-turing"] = tgTuring;
import tgTuringAntd from 'tg-turing-antd';
Vue.use(tgTuringAntd);
tgTuringAntd.defaults.antd.form["date"].format = "yyyy-MM-dd"
```

组件及默认值清单：

```js
> window["tg-turing"].defaults.antd.form

{
    "static": {name:"antd-fc-static"},
    "text": {name:"antd-fc-text"},
    "textarea": {name:"antd-fc-textarea"},
    "date": {name:"antd-fc-date"},
    "date-range": {name:"antd-fc-date-range"},
    "date-local": {name:"antd-fc-date"},
    "date-full": {name:"antd-fc-date"},
    "select": {name:"antd-fc-select"},
    "multi-select": {name:"antd-fc-select", multiple:true},
    "buttonlist": {name:"antd-fc-buttonlist"},
    "number-range":{name:"antd-fc-number-range"},
    "number":{name:"antd-fc-number"},
    "uploadfile":{name:"antd-fc-uploadfile"},
    "tree":{name:"antd-fc-tree"},
    "autocomplete":{name:"antd-fc-autocomplete"},
    "selecttable":{name:"antd-fc-autocomplete"},
    "radiolist":{name:"antd-fc-radiolist"},
    "checkboxlist":{name:"antd-fc-checkboxlist"},
    "switcher":{name:"antd-fc-switcher"}
}
```

### 如何在项目中全局更换现有 xtype 的组件

在项目中将内置的组件跟换为自有的组件

* 定义自己的组件，通过 Vue.Components 注册到全局
* 修改 组件的全局默认参数，将原有的 xtype 对应的实现组件名称，更换为自有的组件
* 名称必须一致

```js
Vue.component('my-component-name', { /* ... */ })

window["tg-turing"].defaults.antd.form["date"].name = "my-component-name";

```


### 如何增加一个 xtype，接入 tg-form

新增一个 xtype 与上一种操作方式一致，区别在于新增一种 type

```js
Vue.component('my-component-name', { /* ... */ })

window["tg-turing"].defaults.antd.form["newxtype"].name = "my-component-name";
```


### 接入的组件可以利用的接口

tg-form 会传递一系列参数，需要继承自 tg-turing.ConnectItem 类


es6语法

```html
<template>
    <FormItem :label="caption" :prop="name" :label-width="params.labelWidth" v-if="formReadonly !== true">
        <DatePicker :value="value" type="date" :placeholder="placeholder" style="width:100%" @on-change="onChange" transfer></DatePicker>
    </FormItem>
    <antd-fc-static v-else :caption="caption" :prop="name" :value="value"></antd-fc-static>
</template>
<script>
import {ConnectItem} from 'tg-turing'
export default {
    name:"antd-fc-date",
    extends: ConnectItem,
    methods:{
        onChange(value) {
            let label = value;
            this.$emit("on-item-change", this.name, value, label, this.model)
            this.$emit("input", value)
        }
    }
}
</script>
```

ConnectItem 定义详见 文档接下来的章节：ConnectItem 每个xtype组件的标准属性



### 标准属性

| 属性 | 描述 | 数据类型 | 默认值 |
| :--- | :--- | :--- | :--- |
| name | 字段名 | String | 必填 |
| caption | 显示文字 | String | 空 |
| hidden | 是否隐藏 | Boolean | false |
| format | 前端只读文本格式化 | String | 空 |
| xtype | 显示控件类型 | Enum | text |
| required | 必填 | Boolean | false |
| url | 远程数据地址 | String | 空 |
| fullrow | 占满一行 | Boolean | false |
| placeholder | 提示文字 | String | 空 |
| options | 数据选项 | Array | 空 |
| default | 默认值 | String | 空 |
| dataSize | 最大长度校验值 | Integer | 空 |
| checkType | 校验类型 | Enum | 空 |
| params | 传递个实际组件的参数 | Object | 空 |

format：日期、数字、金额，或字符串格式化，因效率一般通过后端处理

#### xtype 控件类型枚举

| 属性 | 描述 | 特征 |
| :--- | :--- | :--- |
| select | 单选下拉 | 大量数据，远程搜索，展开，字典映射 |
| multi-select | 多选下拉 | |
| autocomplete | 下拉表格/模糊搜索 | 大数据量，远程搜索，展开，补全选择内容 |
| date-ym | 年月选择框， 默认 yyyy-MM | 年月 |
| date-local | 日期选择框， 默认 yyyy-MM-dd | 年月日 |
| date-full | 日期时间选择框， 默认 yyyy-MM-dd HH:mm | 年月日时分 |
| date-range | 日期范围选择， 默认 yyyy-MM-dd | 年月日，开始、结束 |
| radiolist | 单选按钮组 | 平铺，适用极少选项，字典映射 |
| checkboxlist | 多选按钮组 | 平铺，适用极少选项，字典映射 |
| tree | 单选下拉树 | 展开，大量数据，树状结构，字典映射 |
| multi-tree | 多选下拉树
| switcher | 开关
| buttonlist | 单选按钮组
| multi-buttonlist | 多选按钮组
| textarea | 计数文本域
| number | 数字文本框
| number-range | 数字区间
| uploadfile | 文件上传
| uploadsingleimage | 单图片上传
| uploadmuiltimage | 多图片上传
| text | 文本
| div | div占位
| static | 表单静态字段

## API


### 属性

| 参数 | 说明 | 类型 | 可选值 | 默认值 |
|------|-------|---------|-------|--------|
| fields | 字段模型 | Array | | [] |
| value | 表单值 | Object |  | {} |
| column | 每行显示字段数量 | Number | | 4 |
| labelWidth | 字段前的标签宽度 | Number | | 100 |
| readonly | 只读表单 | Boolean | | false |
| displayFieldFormat | 字典翻译列的后缀，可全局配置window["tg-turing"].defaults.displayFieldFormat | String | `_DISPLAY` | 空 |
| validateRules.sync | 校验规则，可在初始化完成后追加自定义的规则。异步时需要写在this.$nextTick()中 | Object | {} |
| loaddata | 数据加载干预 | Function | | 入参：name, callback。 完成时调用 callback([{value:"",label:""}]) |
| before | 表单开头追加项 | Slot |  |  |
| after | 表单最后追加项 | Slot |  |  |
| 动态：字段名 | 可以替换某个字段 | Slot |  |  |

### Methods

| 方法名称 | 说明 | 参数 |
|---------- |-------- |---------- |
| validate  | 对整个表单进行校验，参数为检验完的回调，会返回一个 Boolean 表示成功与失败，支持 Promise | callback |
| validateField  | 对部分表单字段进行校验的方法，参数1为需校验的 prop，参数2为检验完回调，返回错误信息 | callback  |
| resetFields  | 对整个表单进行重置，将所有字段值重置为空并移除校验结果 | 无  |
| getField  | 根据key获取字段模型，匹配不到时返回`undefeind`。异步时需要写在this.$nextTick()中 | key  |
| submit  | 同步表单提交，主要用于 | url  |

### Events

| 事件名称 | 说明 | 回调参数 |
|---------- |-------- |---------- |
| on-value-change  | 表单项的数据变化时触发 | name, value, display, model, formValue  |
| input  | 支持v-model | formValue |



### ConnectItem 每个xtype组件的标准属性

| 参数 | 说明 | 类型 | 可选值 | 默认值 |
|------|-------|---------|-------|--------|
| name | 字段名 | String | | 必填 |
| caption | 显示文字 | String | 空 |
| xtype | 显示组件类型 | String | | static |
| value | 字段值 | Object |  | null |
| display | 字段显示文本。select等字典型组件会显示文本 | Object |  | null |
| placeholder | 文本占位符 | String | |  |
| readonly | 字段内容只读 | Boolean | | false |
| options | 可选项 | Array<label:String, value:String> |  | 空 |
| formReadonly | 表单整体只读 | Boolean | | false |
| required | 必填 | Boolean | | false |
| disabled | 禁用 | Boolean | | false |
| model | 字段模型 | Object | | {} |
| fullrow | 占满一行 | Boolean | false |
| params | 需要透传给组件的个性化参数 | Object | |  |
| loaddata | 数据加载干预 | Function | | 入参：name, callback。 完成时调用 callback([{value:"",label:""}]) |

### Events

| 事件名称 | 说明 | 回调参数 |
|---------- |-------- |---------- |
| on-item-change  | 值变化时触发 | name, value, display, model  |
| input  | 支持v-model | value |


# EMAP DataAdapter

与 EMAP 后端模型对接的 DataAdapter

turing 挂载于 window["tg-turing"] 中

```js
var turing = window["tg-turing"];
```

## 初始化方式

使用 DataAdapterFactory 中默认为创建 EMAP 类型的 DataAdapter

### 加载静态模型定义

适用于已经将模型数据缓存到页面的情况，看起来应该像这样：

```js
var pageMeta = {"models":[{"name":"FORM_GROUP","appName":"应用FORM_GROUP","modelName":"模型FORM_GROUP","url":"http://res.wisedu.com/fe_components/mock/form_group.json","controls":[{"name":"WID","dataType":"String","caption":"请选择您要参加的招聘计划：","placeholder":"","dataSize":4,"xtype":"radiolist","readonly":false,"url":"./mock/select.json","required":false}]}]}
var inst = new turing.DataAdapterFactory.create(pageMeta, "T_FUNA_USER_QUERY");
inst.view("grid:table");
```

### 加载动态页面模型

由于是模型是通过load方法异步加载的，所以通过inst初始化的方法都需要写在 load 完成后。

```js
var inst = new turing.DataAdapterFactory.create();
export default {
    data(){
        return {
            columns:[]
        }
    },
    async mounted(){
        await inst.load("url", "T_FUNA_USER_QUERY");
        this.columns = inst.view("默认列表:table");
    }
}
```

### 加载流程合并的模型

```js
var inst = new turing.DataAdapterFactory.create();
inst.getIntegratedModel("url", "T_FUNA_USER_QUERY")
let fields = inst.view("默认表单:form")
```


## 数据查询

### 执行自定义动作

```js
var inst = new turing.DataAdapterFactory.create();
export default {
    data(){
        return {}
    },
    async mounted(){
        await inst.load("url", "T_FUNA_USER_QUERY")
        let datas = await inst.execute("动作别名", {param1:1,param2:2});
        this.rowData = datas;
    }
}

```

### 获取数据 findAll

findAll 默认会在加载模型后，自动映射动作名称，规则有二：
1. 与名称匹配的模型的url地址会自动赋值给findAll的url
2. 后缀为 `_QUERY` 的动作作为请求地址。

```js
inst.load("url", "T_FUNA_USER_QUERY")
//T_FUNA_USER_QUERY该模型的url地址会自动映射到findAll
```


> 更换默认的 findAll 请求地址，需要调整其 url 地址，以下给出示例：
> this.actions.findAll.params 中可以配置固定查询参数，会与findAll函数传入的参数做合并，以函数传入参数的优先级高

```js
var inst = new turing.DataAdapterFactory.create();
export default {
    data(){
        return {
            columns:[]
        }
    },
    async mounted(){
        await inst.load("url", "T_FUNA_USER_QUERY");
        //调整默认 findAll 的请求地址
        inst.actions["findAll"].url = "";
        inst.actions["findAll"].params = {"status":"已完成"}
        this.columns = inst.view("默认列表:table");
        let datas = await inst.findAll({ parentId:"00001" });
        this.rowData = datas;
    }
}
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


## 保存数据 save

save 默认会在加载模型后，自动映射动作名称后缀为 `_SAVE` 的动作作为请求地址。

```js
inst.save(this.deptData).then(result => {
    alert("ok")
})
```


### 删除数据 delete

delete 默认会在加载模型后，自动映射动作名称后缀为 `_DELETE` 的动作作为请求地址。

```js
inst.delete(deptId).then(result => {
    alert("ok")
})
```


### 排序

使用order方法，设置排序，该参数只在findAll方法中生效。

```js
methods: {
    async query() {
        inst.querySetting = inst.querySettingBuilder(this.searchValues, "Dept");
        let datas = inst.findAll()
        this.data5 = datas;
    },
    sortHandler(param) {
        let keys = param.key.split(".")
        if (param.order !== "normal"){
            inst.order(keys.concat([param.order]));
        } else {
            inst.order(keys);
        }
        this.query()
    }
}
```



### action 默认定义

```js
actions = {
    save:{
        url: "",
        method: "post",
        name: ""
    },
    delete:{
        url: "",
        method: "post",
        name: ""
    },
    findById:{
        url: "",
        method: "get",
        name: ""
    },
    findAll:{
        url: "",
        method: "post",
        name: "",
        params: {},
        orders: [],
        include: []
    }
}
```

### 变量参数

url里面可以写{变量名}，会由params中的数据替换掉
如：
```js
this.actions.delete.url = "/api/dept/{id}";
...

this.delete({id:"123"})

```
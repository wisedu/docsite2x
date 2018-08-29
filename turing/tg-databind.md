
## DataBind 页面数据绑定

数据绑定这个模式是固定的，API 已经被实现的组件所继承，具有该能力的组件：
* [tg-listview](./tg-listview)

以 tg-listview 组件为示例来说明，有两种方式可以加载数据：

#### 1、 设置 autoReadyDataBind 属性，页面加载时数据自动加载。

```html
<tg-listview :datasource="datasource" autoReadyDataBind>
  ...
</tg-listview>
```

如果数据加载需要带有参数，需要在初始化 DataSource 的时候将参数带入。如：

```js
var hqjxjzlbgsj = new window.["tg-turing"].DataSourceManager("hqjxjzlbgsj", pageMeta, {userid:"aa"});
window.["tg-turing"].DataSourceManager.set(hqjxjzlbgsj);
```


#### 2、 @ready 事件，手动调用DataBind方法。

ref 属性是 vuejs 中对组件引用的标识，类似 html 中的 id。[Vue中对ref的文档说明](https://cn.vuejs.org/v2/api/#ref)

```html
<tg-listview ref="tglist" :datasource="ds" @ready="init">
  ...
</tg-listview>
```

有了 DataBind 方法，你也可以在需要的时候反复调用，如：数据刷新

```js
{
  methods:{
      init: function(inst) {
          inst.DataBind();
          // inst.DataBind({param1:"1"});
      },
      refresh: function() {
          this.$refs.tglist.DataBind({param1:"1"});
      }
  }
}
```


### 属性
| 参数 | 说明 | 类型 | 可选值 | 默认值 |
|------|-------|---------|-------|--------|
| datasource | 数据源 | DataSource | | |
| pageSize | 分页大小 | Number |  | 10 |
| autoReadyDataBind | 组件ready事件时，自动执行数据绑定 | Boolean | | false |

### Methods
| 方法名称 | 说明 | 参数 |
|---------- |-------- |---------- |
| DataBind  | 执行findAll查询数据 | `{查询参数1:1,查询参数2:2}`  |
| SetData  | 直接设置数据，适用于自行获取的数据 | `{rows:[{字段1:1,字段2:2},{字段1:1,字段2:2}]}`  |

### Events
| 事件名称 | 说明 | 回调参数 |
|---------- |-------- |---------- |
| ready  | 组件加载完成，主要用于手动做数据绑定 | 组件实例 inst  |

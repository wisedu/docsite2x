# tg-collection-view

## 功能

### 搜索 + 工具栏 + 列表

![完整的示例](../static/collection-view-full.png)

#### 通过data-adapter加载数据

```html
<tg-collection-view :searcher="searcher" :data-adapter="da" :grid="{gutter: 16, column: 3}">
  <div slot="toolbar-left">
    <Button type="primary" @click="openModal(true)" v-tg-funckey="'abc'">新增</Button>
    <Button type="warning" @click="openModal()">修改</Button>
    <Button type="info" @click="viewIt">查看</Button>
    |
    <Button type="error" @click="delIt">删除</Button>
  </div>
  <template slot="itemTemplate" slot-scope="props">
    项模板{{props.data}} / {{props.index}}
  </template>
  <template slot="alternateTemplate" slot-scope="props">
    交替项模板{{props.data}} / {{props.index}}
  </template>
</tg-collection-view>
```

静态模型加载

```js
(function (exports, turing) {
	var inst = new turing.DataAdapterFactory.create(pageMeta, "T_FUNA_USER_QUERY");
	var ClassImpl = {
		data:function(){
			return {
				da:inst,
				searcher: {
					name:"search",
					column:3,
					fields:inst.view("search:form"),
					value:{}
				}
			}
		}
	}
	exports["emap-usermanager"].mixins = [ClassImpl]
})(window.turingform, window["tg-turing"]);

```

动态模型加载

```js
(function (exports, turing) {
	var inst = new turing.DataAdapterFactory.create();
	var ClassImpl = {
		data:function(){
			return {
				da:inst,
				searcher: {
					name:"search",
					column:3,
					fields:[],
					value:{}
				}
				currentRow: {},
				selection: [],
			}
		},
		async mounted(){
            await inst.load("url", "T_FUNA_USER_QUERY");
            this.searcher.fields = inst.view("search:form");
        }
	}
	exports["emap-usermanager"].mixins = [ClassImpl]
})(window.turingform, window["tg-turing"]);

```


#### 外部传递数据加载 collection-view

```html
<tg-collection-view :grid="{gutter: 16, column: 3}" :searcher="searcher" :datas="data" @on-change="reload">
    <template slot="itemTemplate" slot-scope="props">
        <Card style="width:100%">
            <p slot="title">
                <Icon type="ios-film-outline"></Icon>
                <tg-text class="tg-primary-1">主标题{{props.data}}</tg-text>
            </p>
            <tg-text class="tg-grey-3">副标题{{props.index}}</tg-text>
            <tg-text><Badge count="new" class-name="tg-primary-1 tg-bg-white tg-br-primary-1"></Badge></tg-text>
            <tg-text><tg-linkbutton>Text</tg-linkbutton></tg-text>
        </Card>
    </template>
</tg-collection-view>
```

```js
(function (exports, turing) {
	var inst = new turing.DataAdapterFactory.create(pageMeta, "T_FUNA_USER_QUERY");
	var ClassImpl = {
		data:function(){
			return {
				data:[],
				searcher: {
					name:"search",
					column:3,
					fields:inst.view("search:form"),
					value:{}
				}
			}
		},
		created: function(){
			var that = this;
			that.reload();
		},
		methods:{
			reload: function(pager, searchvalue, sorts, source) {
				var that = this;
				inst.pageNumber = pager.index;
				inst.pageSize = pager.size;
				inst.findAll(searchvalue).then(function(results) {
					that.data = results;
				})
			},
		}
	}
	exports["emap-usermanager"].mixins = [ClassImpl]
})(window.turingform, window["tg-turing"]);

```


## API


### 属性

| 参数 | 说明 | 类型 | 可选值 | 默认值 |
|------|-------|---------|-------|--------|
| datas | 静态数据 | Array, Object | [], {count:0, rows:[]} |  |
| searcher | 查询组件 | Object | {name:"search",column:3,fields:[],value:{}} |  |
| toolbar-left | 工具栏-左 | Slot |  |  |
| toolbar-right | 工具栏-右 | Slot |  |  |
| itemTemplate | 显示项 | Slot |  |  |
| alternateTemplate | 交替项 | Slot |  |  |
| search-字段 | 搜索字段 | Slot |  |  |
| datas.sync | 当前页数据 | Array, Object |  |  |
| searchHandler | 查询按钮接管 | Function |  | 查询值，{Key1:1,Key2:2} |
| dataAdapter | 数据源 | DataAdapter | | |
| params | 执行数据查询时，带入的参数 | Object | | |
| pager | 分页，总数大于0时显示。如果设置为null，强制隐藏 | Object |  | {size:20,index:1} |

### Methods
| 方法名称 | 说明 | 参数 |
|---------- |-------- |---------- |
| reload  | 刷新数据 | 查询参数 `{pageNumber:1,pageSize:50,params:{}}`, 加载完回调 `callback` |
| searchClear | 清除搜索条件 | |

### Events
| 事件名称 | 说明 | 回调参数 |
|---------- |-------- |---------- |
| on-change  | 表格数据变化 | 分页:`{index, size}`, 查询值, 排序字段, 触发类型  |
| on-value-change  | 搜索值变化 | 字段名, 值, 显示值, 模型, 全部搜索值  |
| ready  | 组件加载完成，主要用于手动做数据绑定 | 组件实例 inst  |
| data-loaded  | 数据加载完成 | datas  |


## searcher

搜索插件扩展的方式：

name: 为组件名称，最终与实现type 形成完整的组件实现名称，如： antd-gb-search ，中间 -gb- 为固定格式 gridbridge 的缩写

其他参数为该组件所需要的参数，会被直接透传给最终实现组件

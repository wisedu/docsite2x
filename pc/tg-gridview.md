## tg-gridview

### 搜索 + 工具栏 + 列表

![完整的示例](../static/gridview-full.png)

#### 通过data-adapter加载数据

```html
<tg-gridview :searcher="searcher" :columns="columns" :data-adapter="da" autoReadyDataBind :currentRow.sync="currentRow" :selection.sync="selection">
  <div slot="toolbar-left">
    <Button type="primary" @click="openModal(true)" v-tg-funckey="'abc'">新增</Button>
    <Button type="warning" @click="openModal()">修改</Button>
    <Button type="info" @click="viewIt">查看</Button>
    |
    <Button type="error" @click="delIt">删除</Button>
  </div>
  <div slot="columns-opt" slot-scope="scope">
    <tg-linkbutton  @click="resetPassword(scope.row.ACCOUNTID)">重置密码</tg-linkbutton>
  </div>
</tg-gridview>
```

```js
(function (exports, turing) {
	var inst = new turing.DataAdapterFactory.create(pageMeta, "T_FUNA_USER_QUERY");
	var ClassImpl = {
		data:function(){
			var columns = inst.view("grid:table");
			columns.unshift({key: 'opt',title:"操作",width: 120,align: 'center'});
			columns.unshift({type: 'selection',width: 60,align: 'center'});
			return {
				da:inst,
				columns: columns,
				fields: inst.view("form:form"),
				searcher: {
					name:"search",
					column:3,
					fields:inst.view("search:form"),
					value:{}
				}
				currentRow: {},
				selection: [],
			}
		}
	}
	exports["emap-usermanager"].mixins = [ClassImpl]
})(window.turingform, window["tg-turing"]);

```

#### 外部传递数据加载 gridview

```html
<tg-gridview :columns="columns" :data="data" @on-change="reload" :loading="loading" @on-highlight="onSelectedRow" @on-selection-change="onSelectionChange">
  <div slot="toolbar-left">
    <Button type="primary" @click="openModal(true)" v-tg-funckey="'abc'">新增</Button>
    <Button type="warning" @click="openModal()">修改</Button>
    <Button type="info" @click="viewIt">查看</Button>
    |
    <Button type="error" @click="delIt">删除</Button>
  </div>
</tg-gridview>
```

```js
(function (exports, turing) {
	var inst = new turing.DataAdapterFactory.create(pageMeta, "T_FUNA_USER_QUERY");
	var ClassImpl = {
		data:function(){
			var columns = inst.view("grid:table");
			columns.unshift({type: 'selection',width: 60,align: 'center'});
			return {
				columns: columns,
				data:[],
				fields: inst.view("form:form"),
				searcher: {
					name:"search",
					column:3,
					fields:inst.view("search:form"),
					value:{}
				}
				currentRow: {},
				selection: [],
				loading: false,
			}
		},
		created: function(){
			var that = this;
			that.reload({index:1, size:10}, {}, [],"init");
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
			onSelectedRow: function(newRow, oldRow) {
				this.currentRow = newRow;
			},
			onSelectionChange: function(selection) {
				this.selection = selection;
			}
		}
	}
	exports["emap-usermanager"].mixins = [ClassImpl]
})(window.turingform, window["tg-turing"]);

```


### 仅 grid

不设置 fields 时，上面的搜索不会显示

![完整的示例](../static/gridview-simple.png)


当分页的总数 < 0 时，分页不显示

通过 slot: toolbar-left 插入工具栏按钮

```html
<tg-gridview :columns="columns" :data-adapter="da" autoReadyDataBind :currentRow.sync="currentRow" :selection.sync="selection">
  <div slot="toolbar-left">
    <Button type="primary" @click="openModal(true)" v-tg-funckey="'abc'">新增</Button>
    <Button type="warning" @click="openModal()">修改</Button>
    <Button type="info" @click="viewIt">查看</Button>
    |
    <Button type="error" @click="delIt">删除</Button>
  </div>
  <div slot="columns-opt" slot-scope="scope">
    <tg-linkbutton  @click="resetPassword(scope.row.ACCOUNTID)">重置密码</tg-linkbutton>
  </div>
</tg-gridview>
```

### 根据状态控制行颜色

```html
<tg-gridview :columns="columns" :data-adapter="da" autoReadyDataBind :rowRending="rowRending">
  ...
</tg-gridview>
```

```js
export default {
  methods:{
    rowRending(row, index){
      if (row["status"] === "done") {
        return "row-done";
      }
    }
  }
}
```

```css
.row-done td{
  background-color: #2db7f5;
  color: #fff;
}
```
## API


### 属性
| 参数 | 说明 | 类型 | 可选值 | 默认值 |
|------|-------|---------|-------|--------|
| datas | 静态数据 | Array, Object | [], {count:0, rows:[]} |  |
| columns | 字段模型 | Array |  | [] |
| loading | 显示表格加载中动画 | Boolean |  | false |
| searcher | 查询组件 | Object | {name:"search",column:3,fields:[],value:{}} |  |
| toolbar-left | 工具栏-左 | Slot |  |  |
| toolbar-right | 工具栏-右 | Slot |  |  |
| columns-字段 | 表格字段 | Slot |  |  |
| search-字段 | 搜索字段 | Slot |  |  |
| currentRow.sync | 已选行 | Object |  |  |
| selection.sync | 已勾选行集合 | Array |  |  |
| datas.sync | 当前页数据 | Array, Object |  |  |
| rowRending | 渲染行控制样式，返回className | Function |  |  |
| dataAdapter | 数据源 | DataAdapter | | |
| pageSize | 分页大小 | Number |  | 50 |
| autoReadyDataBind | 组件ready事件时，自动执行数据绑定 | Boolean | | false |

### Methods
| 方法名称 | 说明 | 参数 |
|---------- |-------- |---------- |
| reload  | 刷新数据 | 分页 `{index:1,size:50}`, 加载完回调 `callback` |
| searchClear | 清除搜索条件 | |

### Events
| 事件名称 | 说明 | 回调参数 |
|---------- |-------- |---------- |
| on-change  | 表格数据变化 | 分页:`{index, size}`, 查询值, 排序字段, 触发类型  |
| on-value-change  | 搜索值变化 | 字段名, 值, 显示值, 模型, 全部搜索值  |
| on-highlight  | 单选行触发 | 当前选中行, 之前选中行  |
| on-select-all  | 全选触发 | 已选行集合  |
| on-selection-change  | 多选checkbox触发 | 已选行集合  |


## searcher

搜索插件扩展的方式：

name: 为组件名称，最终与实现type 形成完整的组件实现名称，如： antd-gb-search ，中间 -gb- 为固定格式 gridbridge 的缩写

其他参数为该组件所需要的参数，会被直接透传给最终实现组件

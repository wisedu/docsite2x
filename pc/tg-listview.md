# tg-listview

## 代码示例

### 基本用法

该组件支持三种模式：列表、栅格、平铺

datas 属性支持静态数据传入，与 autoReadyDataBind 属性互斥，在组件的 ready 事件后

```html
<tg-listview :datas="[{a:1,b:2},{a:11,b:22}]" bordered>
  <template slot="itemTemplate" slot-scope="props">
    项模板
  </template>
  <template slot="alternateTemplate" slot-scope="props">
    交替项模板
  </template>
  <template slot="pager">
    页脚模板
  </template>
</tg-listview>
```

---

### 列表模式 - 文字列表

![文字列表](../static/listview-list.png)

```html
<tg-listview :data-adapter="da" bordered autoReadyDataBind pagination :page-size="20">
    <template slot="itemTemplate" slot-scope="props">
        <tg-div class="tg-col-6">
            <tg-text class="tg-primary-1">数据内容{{props.data}}</tg-text>
            <tg-text class="tg-grey-3">行标识{{props.index}}</tg-text>
        </tg-div>
        <tg-div class="tg-col-3">
            <tg-text><Badge count="new" class-name="tg-primary-1 tg-bg-white tg-br-primary-1"></Badge></tg-text>
        </tg-div>
        <tg-div class="tg-col-3">
            <tg-text><tg-linkbutton>Text</tg-linkbutton></tg-text>
        </tg-div>
    </template>
</tg-listview>
```

---

### 栅格模式 - 卡片列表

![卡片列表](../static/listview-card.png)

```html
<tg-listview :data-adapter="da" :grid="{gutter: 16, column: 3}" autoReadyDataBind>
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
</tg-listview>
```

### 平铺模式 - 图标列表

![图标列表](../static/listview-icon.png)

```html
<tg-listview :data-adapter="da" :grid="{gutter: 40}" @ready="init">
    <template slot="itemTemplate" slot-scope="props">
        <tg-div>
            <Icon type="stop" size="107"></Icon>
        </tg-div>
        <tg-div class="tg-text-center">
            <tg-text class="tg-primary-1">主标题{{props.data}}</tg-text>
        </tg-div>
    </template>
</tg-listview>
```

如果要精确控制边距，可以给gutter设置字符串，定义为padding属性
```html
<tg-listview :data-adapter="da" :grid="{gutter: '10px 20px'}" @ready="init">
  ...
</tg-listview>
```
这里在标签上设置了 **@ready事件** ，可以手动调用数据加载的方法
```js
{
  methods:{
      init(list){
          list.DataBind();
          // list.DataBind({param1:"1"});
      }
  }
}
```

## API

### 属性

| 参数 | 说明 | 类型 | 可选值 | 默认值 |
|------|-------|---------|-------|--------|
| datas | 静态数据 | Array | [] |  |
| size | 尺寸 | String | 'small','default','large' | 'default' |
| grid | 排列方式，横向 或 纵向 | Object | {gutter: 16, column: 3} / {gutter: '10px 20px'} |  |
| bordered | 是否显示边框 | Boolean | | false |
| pagination | 是否显示分页按钮 | Boolean | | false |
| itemTemplate | 显示项模板 | Slot |  | {data:[], index:0} |
| pagerTemplate | 分页模板 | Slot |  |  |
| emptyTemplate | 无数据模板 | Slot |  |  |
| dataAdapter | 数据源 | DataAdapter | | |
| pageSize | 分页大小 | Number |  | 10 |
| autoReadyDataBind | 组件ready事件时，自动执行数据绑定 | Boolean | | false |

### Methods
| 方法名称 | 说明 | 参数 |
|---------- |-------- |---------- |
| DataBind  | 执行findAll查询数据 | `{index:1,size:10}`,callback  |
| SetData  | 直接设置数据，适用于自行获取的数据 | `{rows:[{字段1:1,字段2:2},{字段1:1,字段2:2}]}`  |
| LoadMore  | 触发加载更多，根据`pageSize`获取数据 | 无  |

### Events
| 事件名称 | 说明 | 回调参数 |
|---------- |-------- |---------- |
| ready  | 组件加载完成，主要用于手动做数据绑定 | 组件实例 inst  |
| data-loaded  | 数据加载完成 | datas  |
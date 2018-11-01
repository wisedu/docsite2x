# tg-editable-grid

高性能可编辑表格，底层基于 Canvas 技术，仅绘制可视区域内的元素，达到 百万行 * 上千列数据，显示流畅的效果

该组件底层是基于 [fin-hypergrid](https://github.com/fin-hypergrid/core)  [官方教程](https://fin-hypergrid.github.io/tutorial/?p=2)

## 功能

通过模型配置可编辑列：

* select - 下拉
* tree - 下拉树 （需要额外引入组件）
* date-full - 日期 （需要额外引入组件）
* switcher - 开关


## 初始化示例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>webpack v4</title>
    <script src="./dist/tg-editable-grid.min.js"></script>
    <link rel="stylesheet" type="text/css" href="./tg-editable-grid.css">
</head>
<body>
    <button id="addrow">新增一行</button> / <button id="getData">获取数据</button>
    <div id="root"></div>
</body>
<script>
    var schema = [{
            name: "SZDWDM_DISPLAY",
            caption: 'SZ单位',
            xtype: "tree"
        },
        {
            name: 'SZDWDM',
            caption: 'SZDWDM',
            xtype: "text"
        },
        {
            name: 'CZRQ',
            caption: '操作日期',
            xtype: "datetime"
        },
        {
            name: 'WID',
            caption: 'WID',
            xtype: "text"
        },
        {
            name: 'SFCYLK',
            caption: 'SFCYLK',
            xtype: "switcher"
        },
        {
            code: 'ZZMMDM',
            caption: '政治面貌',
            name: "ZZMMDM_DISPLAY",
            xtype: "select"
        }
    ];

    var EditableGrid = window["tg-editable-grid"].default;
    var inst = new EditableGrid($("#root"), {displayFieldFormat:"_DISPLAY"});
    inst.setSchema(schema);

    var datas = [{SZDWDM_DISPLAY:"",SZDWDM:"",CZRQ:"",WID:"",SFCYLK:"",ZZMMDM:""}]
    inst.setData(datas);


    document.getElementById("addrow").addEventListener("click", function (e) {
        inst.getData().push({
            SZDWDM: "",
            SZDWDM_DISPLAY: "",
            CZRQ: "",
            WID: "",
            ZZMMDM: ""
        });
        document.getElementById("root").style.height = "200px";
    })

    document.getElementById("getData").addEventListener("click", function (e) {
        console.log(inst.getData());
    })
</script>
</html>
```


## 原生组件 API

### Methods

| 方法名称 | 说明 | 参数 |
|---------- |-------- |---------- |
| setSchema  | 设置结构 | `列结构定义` |
| setData | 设置数据 | [{"字段1":"值1"}] |
| getData | 获取数据 | 无 |
| onEditorLoadData | 针对后端，获取数据处理，必须实现该方法 | 回调参数：model, value, callback |
| resetWidth | 重设表格宽度 | 无 |

onEditorLoadData 示例

```js
inst.onEditorLoadData = function(model, value, callback) {
    switch (model.xtype) {
        case "tree":
            if (model.dict !== undefined) {
                defaults.getDictTreeData[0](model.dict, {key:value}, datas => {
                    let treedatas = inst.utils.toTreeData(datas, "", {ukey:"id", pkey:'pId', toCKey:'children'})
                    callback(treedatas);
                });
            } else if (model.options !== undefined) {
                callback(model.options);
            }
            break;
        default:
            if (model.dict !== undefined) {
                defaults.getDictData[0](model.dict, {key:value}, datas => {
                    callback(datas);
                });
            } else if (model.options !== undefined) {
                callback(model.options);
            }
            break;
    }
}
```

### 列结构定义

| 属性 | 描述 | 数据类型 | 默认值 |
| :--- | :--- | :--- | :--- |
| name | 字段名 | String | 必填 |
| caption | 显示文字 | String | 空 |
| xtype | 显示控件类型 | Enum | text |
| code | 用于字典字段对应的code字段名 | String | 空 |

### Events

| 事件名称 | 说明 | 回调参数 |
|---------- |-------- |---------- |
| fin-editor-data-change  | 数据更改后事件 | event  |
| fin-click  | 单元格点击 | event |
| fin-row-header-clicked  | 整行点击 | event |
| fin-grid-rendered  | 表格渲染完成 | event |


```js
this.inst.grid.addEventListener('fin-editor-data-change', event => {
    let name = event.detail.input.column.schema.name;
    let newValue = event.detail.newValue;
    let oldValue = event.detail.oldValue;
    let schema = event.detail.input.column.schema;
    let row = event.detail.input.event.dataRow;
    let index = event.detail.input.event.dataCell.y;
});
this.inst.grid.addEventListener('fin-click', event => {
    let row = event.detail.row;
    let rowIndex = event.detail.dataCell.y;
    this.activedIndex = rowIndex;
});
this.inst.grid.addEventListener('fin-row-header-clicked', event => {
    let row = event.detail.row;
    let rowIndex = event.detail.dataCell.y;
    this.activedIndex = rowIndex;
});
this.inst.grid.addEventListener('fin-grid-rendered', event => {
    
});
```
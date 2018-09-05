# tg-linkbutton

## 代码示例

可以作为超链接 或者 按钮来使用，设置超链接时 click事件 无效

```html
<tg-linkbutton>操作按钮</tg-linkbutton>

<tg-linkbutton href="http://www.baidu.com" target="_blank">操作按钮</tg-linkbutton>
```

其他暂无特别
未来要与表单提交事件做绑定

## API

### 属性
| 参数 | 说明 | 类型 | 可选值 | 默认值 |
|------|-------|---------|-------|--------|
| href | 超链接 | string |  |  |
| target | 打开方式 | string | `_blank`,`_parent`,`_self`,`_top` | _self |
|  | 默认slot，加入内容以显示 | Slot | html |  |

### Events
| 事件名称 | 说明 | 回调参数 |
|---------- |-------- |---------- |
| click  | 点击事件 | 事件对象  |

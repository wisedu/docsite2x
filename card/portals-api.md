# API

### 内嵌应用API



###### ajax

示例：
```
PA.utils.ajax({
    url: '地址',
    type: '请求类型，默认post',
    data: {}
}).then(function(_res){
    //逻辑操作
})
```


###### 创建唯一标识guid

示例：
```
var guid = PA.utils.newGuid();
```


###### 获取节点位置和宽高信息
```
//el为原生dom节点
var position = PA.utils.getElementPosition(el)
```


###### 数组转对象
```
//arr，要转换的数组
//field，以数组中其中一个字段的值作为对象的key
var obj = PA.utils.arrToObj(arr, field)
```


###### 在新页面打开一个应用
```
PA.app.open({
    url: '必填，应用地址',
    pageId: '可选，页面id',
    appId: '可选，应用id',
    stringId: '可选，应用名称对应的字符串id',
    menuSourceId: '可选，应用对应的菜单源id',
    menuItemGuid: '可选，应用对应的菜单节点id'
})
```


###### 收藏应用
```
PA.app.favorite({
    favorite: '必填，true为执行收藏动作，false为执行取消收藏动作',
    url: '必填，应用地址',
    pageId: '可选，页面id',
    appId: '必填，应用id',
    stringId: '可选，应用名称对应的字符串id',
    menuSourceId: '可选，应用对应的菜单源id',
    menuItemGuid: '可选，应用对应的菜单节点id'
}).then(function(_res){
    //收藏结束后的操作
})
```


###### 获取首页缓存数据
```
//type，数据类型，favorite（收藏），recently（最近使用），menu（菜单）
var data = PA.data.getExtend(type);
```



###### 获取首页信息
```
var info = PA.data.getPageInfo();
```



###### 根据stringId获取对应的语言内容
```
var title = PA.data.getLanguageContentById(stringId)
```



###### 移除菜单中没有子节点的目录

```
PA.menu.removeEmpty(data);
```



###### 移除菜单中不可用的数据

```
PA.menu.removeNotCanUse(data);
```



###### 移除菜单中的空目录和不可用的数据

```
PA.menu.removeEmptyAndNotCanUse(data);
```



###### 根据菜单父节点是否可用的权限，检查和重置子节点的可用权限

```
PA.menu.checkAndResetChildCanUse(data);
```



###### 给菜单中的每个节点添加层级属性

```
PA.menu.setLevel(data);
```








### 卡片与首页交互

1. 卡片扩展信息消息
```
window['tg-turing'].utils.sendMessageToParent({
    type: 'card-header-extend-show',
    data: {
        content: '要显示的扩展信息内容'
})
```

2. 卡片高度重置消息
```
window['tg-turing'].utils.sendMessageToParent({
    type: 'portals-card-height-reset',
    data: {
        height: '要重置的卡片高度'
})
```

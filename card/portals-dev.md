


### 卡片与首页交互

###### 卡片扩展信息消息
```
window['tg-turing'].utils.sendMessageToParent({
    type: 'card-header-extend-show',
    data: {
        content: '要显示的扩展信息内容'
})
```

###### 卡片高度重置消息
```
window['tg-turing'].utils.sendMessageToParent({
    type: 'portals-card-height-reset',
    data: {
        height: '要重置的卡片高度'
})
```

###### 发送获取卡片信息消息
```
window['tg-turing'].utils.sendMessageToParent({
    type: 'get-card-info'
})
```

###### 接收首页返回的卡片信息消息
```
window.addEventListener('message',function(e){
        let data = e.data;
        let type = data.type;
        switch (type){
            case 'get-card-info':
                //相关操作
                break;
        }
},false);
```

# API

### 内嵌应用API



###### ajax

|       参数      |       类型     |       必填      |      说明      |      默认值      |
|:--------------:|:--------------:|:--------------:|:--------------|:--------------:|
|       url      |       string     |       是      |      请求地址      | |
|       data  |       object     |       否      |      请求数据      | |
|       method |       string |       否  |   请求方式，get/post      | post |

示例：
```
PAUtils.ajax(url, data, method).then(function(_res){
    //逻辑操作
})
```


###### 创建唯一标识guid

示例：
```
var guid = PAUtils.createGuid();
```



#### 下面的dom操作，只支持原生dom节点
###### 插入dom元素,支持字符串和dom节点插入

|       参数      |       类型     |       必填      |      说明      |      默认值      |
|:--------------:|:--------------:|:--------------:|:--------------|:--------------:|
| container | dom | 是 |  要插入的容器 | |
| node | dom/html | 是 |  要添加的元素 | |

示例：
```
var container = document.querySelector('#xxx');
var html = '<div></div>';
PADom.append(container, html);
```


###### 在指定的dom元素之前，插入新的元素

|       参数      |       类型     |       必填      |      说明      |      默认值      |
|:--------------:|:--------------:|:--------------:|:--------------|:--------------:|
| node | dom | 是 |  当前元素 | |
| newNode | dom/string | 是 |  新的节点 | |

示例：
```
var node = document.querySelector('#xxx');
var html = '<div></div>';
PADom.before(node, html);
```



###### 删除dom节点

|       参数      |       类型     |       必填      |      说明      |      默认值      |
|:--------------:|:--------------:|:--------------:|:--------------|:--------------:|
| node | dom | 是 |  要删除的节点 | |

示例：
```
var node = document.querySelector('#xxx');
PADom.remove(node, html);
```


###### 查找最近找到的一个父节点,会已当前元素为起始匹配元素

|       参数      |       类型     |       必填      |      说明      |      默认值      |
|:--------------:|:--------------:|:--------------:|:--------------|:--------------:|
| node | dom | 是 |  起始节点 | |
| selector | string | 是 |  要匹配的css选择器，目前只能单独使用id，样式类，属性进行匹配 | |

示例：
```
var node = document.querySelector('#xxx');
var dom = PADom.append(node, '.xxx');
```



###### 判断节点是否存在该样式类

|       参数      |       类型     |       必填      |      说明      |      默认值      |
|:--------------:|:--------------:|:--------------:|:--------------|:--------------:|
| node | dom | 是 |  要判断的节点 | |
| className | string | 是 |  样式类名 | |

示例：
```
var hasClass = PADom.append(node, 'xxx');
```




###### 给元素添加样式类

|       参数      |       类型     |       必填      |      说明      |      默认值      |
|:--------------:|:--------------:|:--------------:|:--------------|:--------------:|
| node | dom | 是 |  要添加的节点 | |
| className | string | 是 |  样式类名 | |

示例：
```
var node = document.querySelector('#xxx');
PADom.addClass(node, 'xxx');
```



###### 删除元素样式类

|       参数      |       类型     |       必填      |      说明      |      默认值      |
|:--------------:|:--------------:|:--------------:|:--------------|:--------------:|
| node | dom | 是 |  要删除的节点 | |
| className | string | 是 |  样式类名 | |

示例：
```
var node = document.querySelector('#xxx');
PADom.removeClass(node, 'xxx');
```



###### 元素样式类切换

|       参数      |       类型     |       必填      |      说明      |      默认值      |
|:--------------:|:--------------:|:--------------:|:--------------|:--------------:|
| node | dom | 是 |  要处理的节点 | |
| className | string | 是 |  样式类名 | |

示例：
```
var node = document.querySelector('#xxx');
PADom.toggleClass(node, 'xxx');
```








### 卡片与首页交互

1. 卡片给首页发送消息
```
parent.postMessage({
    type: "发送的消息名称",
    data: {} //要发送的数据
},'/');
```

2. 卡片扩展信息消息
```
parent.postMessage({
	type: 'card-header-extend-show',
	data: {
	    href: window.location.href,
	    content: '要显示的扩展信息内容'
	}
},'/');
```

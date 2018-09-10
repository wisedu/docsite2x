### 字体


<h1>页面最重要的标题</h1>

```html
    <h1>页面最重要的标题</h1>
    <div class="tg-h1">页面最重要的标题</div>
```


<h2>页面次重要的标题</h2>

```html
  <h2>页面次重要的标题</h2>
  <div class="tg-h2">页面次重要的标题</div>
```

<h3>应用标题</h3>

```html
  <h3>应用标题</h3>
  <div class="tg-h3">应用标题</div>
```


<h5>卡片或内容标题</h5>

```html
  <h5>卡片或内容标题</h5>
  <div class="tg-h5">卡片或内容标题</div>
```


<div class="tg-text-bold">需要强调的正文内容</div>

```html
  <div class="tg-text-bold">需要强调的正文内容</div>
```

<div class="tg-text">正文</div>

```html
  <div class="tg-text">正文</div>
```

<div class="tg-text-link">链接文字</div>

```html
  <div class="tg-text-link">链接文字</div>
```

<div class="tg-text-caption">帮助/辅助信息，次级文本内容</div>

```html
  <div class="tg-text-caption">帮助/辅助信息，次级文本内容</div>
```


### 居中

###### 文字居中

```
<div class="tg-text-center"></div>
```


###### 容器居中 <span style="color: red;">（注：需对容器设置宽度才能生效）</span>

```
<div class="tg-container-center" style="width:300px;" ></div>
```


###### 栅格居中 <span style="color: red;">（注：下面的居中，仅在栅格上生效，不兼容IE9，IE9的表现形式为居上居左）</span>

* 该行下的所有列垂直水平居中 <span style="color: red;">（注：该水平居中仅对内容为文本时生效）</span>

```
<div class="tg-row tg-row-center">
    <div class="tg-col-6"> 内容 </div>
    <div class="tg-col-6"> 内容 </div>
</div>
```

* 该行下的所有列垂直居中

```
<div class="tg-row tg-row-center-v">
    <div class="tg-col-6"> 内容 </div>
    <div class="tg-col-6"> 内容 </div>
</div>
```

* 该行下的所有列水平居中 <span style="color: red;">（注：该水平居中仅对内容为文本时生效）</span>

```
<div class="tg-row tg-row-center-h">
    <div class="tg-col-6"> 内容 </div>
    <div class="tg-col-6"> 内容 </div>
</div>
```

* 对列单独设置垂直水平居中 <span style="color: red;">（注：该水平居中仅对内容为文本时生效）</span>

```
<div class="tg-row">
    <div class="tg-col-6 tg-col-center"> 该列垂直水平居中 </div>
    <div class="tg-col-6"> 内容 </div>
</div>
```

* 对列单独设置垂直居中

```
<div class="tg-row">
    <div class="tg-col-6 tg-col-center-v"> 该列垂直居中 </div>
    <div class="tg-col-6"> 内容 </div>
</div>
```

* 对列单独设置水平居中 <span style="color: red;">（注：该水平居中仅对内容为文本时生效）</span>

```
<div class="tg-row">
    <div class="tg-col-6 tg-col-center-h"> 该列水平居中 </div>
    <div class="tg-col-6"> 内容 </div>
</div>
```



### 常用样式

| 左浮动 | tg-left |
|--------:|:--------|
| 右浮动 | tg-right |
| 清除浮动 | tg-clear |
| 仅清除子节点浮动 | tg-clear-child |
| <label style="font-size: 32px;line-height: 45px;font-family: PingFang SC;">文字<br>大小</label> | <div style="font-size: 32px;line-height: 45px;font-family: PingFang SC;">文字<br>大小</div> |




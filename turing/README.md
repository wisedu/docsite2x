## Turing 前端开发框架

### 浏览器支持范围

* 360 安全 >= 9.0
* 360 极速 >= 9.1
* Chrome >= 55
* Firefox >= 61
* Safari >= 10 
* Explorer >= 9 
* Edge >= 13 
* iOS >= 10 
* Android >= 6

### 原生 es6 语法与模块化开发

开发时使用 Chrome 63 以上，使用 es6 的语法特性，进行开发调试。集成 Vue、Vue Router、Vuex

支持的 js api 兼容

* [ECMAScript: Object](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object)
* [ECMAScript: Array](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array)
* [ECMAScript: String](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String)
* [ECMAScript: Promise](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise)
* [ECMAScript: Reflect](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Reflect)

不支持:

* ECMAScript: Symbol
* ECMAScript: Collections
* ECMAScript: Typed Arrays
* DOM API、CSS功能。这两类是低版本浏览器本身不支持


引用框架库:

```html
<!-- PC -->
<script src="http://res.wisedu.com/fe_components/turing-form/wisedu-vue.pc.min.js">

<!-- mobile -->
<script src="http://res.wisedu.com/fe_components/turing-form/wisedu-vue.mobile.min.js">
```


### 命令行编译,全面处理兼容性,无需安装环境

支持以下多浏览器兼容:

* js es6 语法兼容性
 * 箭头函数=>
 * async & await 
 * import & export 
 * 展开运算符... 
 * 类定义 class & extend 
 * 动态导入js, import('./xx.js')
* css 兼容性
* Js、css文件合并

可以在后端环境（如：java、node）集成开发，无需实时前端编译。

提供独立的 tgbuilder 程序进行编译打包处理（[win64](#) / [linux](#) / [macOS](#)），内部集成 node环境 和 webpack 配置，运行命令即可编译


```
--windows x64
./tgbuilder.exe compile

--linux / macOS
./tgbuilder compile
```



### 要点

* 学习 es6 import / export 模块化开发
* 学习 Vue 相关开发技术



## 工程目录结构

```
web
├─Branch
│  ├─card
│  ├─mobile.css （tgbuilder 生成）
│  ├─mobile.js （tgbuilder 生成）
│  ├─mobile
│  └─pc
├─Capacity
│  ├─card
│  ├─mobile.css （tgbuilder 生成）
│  ├─mobile.js （tgbuilder 生成）
│  ├─mobile
│  │  ├─main.js (入口文件)
│  │  ├─components
│  │  │  ├─biz-com1
│  │  │  └─...
│  │  ├─pages
│  │  │  ├─page1
│  │  │  │   ├─subpage1
│  │  │  │   └─...
│  │  │  └─...
│  │  └─store
│  │      └─modules
│  └─pc
├─public
│  └─doc_resource
│      ├─schedule-form
│      └─smile-form
└─static
```
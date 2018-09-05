# Turing 前端开发框架

## 特性

### 浏览器引擎支持范围

| PC   | Mobile  | 
| --------   | -----  |
| Chrome >= 55 | Android >= 6  |
| Safari >= 10  | iOS >= 10  |
| Firefox >= 63 | -   |
| Edge >= 13  |  -  |
| Explorer >= 9  | -   |


双核浏览器:
* 360 安全 >= 9.0
* 360 极速 >= 9.1

### 原生 es6 语法与模块化开发

开发时使用 Chrome 63 以上，使用 es6 的语法特性，进行开发调试。集成 Vue、Vue Router、Vuex

| 支持的 JS API   | 不支持的 JS API  | 
| --------   | -----:  |
| [ECMAScript: Object](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object)  | ECMAScript: Symbol | 
| [ECMAScript: Array](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array) | ECMAScript: Collections |
| [ECMAScript: String](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String) | ECMAScript: Typed Arrays |
| [ECMAScript: Promise](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise) | DOM API * |
| [ECMAScript: Reflect](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Reflect)  | CSS功能 * |

*低版本浏览器本身不支持


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



## 工程目录结构 - EMAP

```
web/
├─Branch/
│  ├─mobile.css （tgbuilder 生成）
│  ├─mobile.js （tgbuilder 生成）
│  ├─mobile/
│  └─pc
├─Capacity/
│  ├─mobile.css （tgbuilder 生成）
│  ├─mobile.js （tgbuilder 生成）
│  ├─mobile/
│  │  ├─main.js (入口文件)
│  │  ├─components/
│  │  │  ├─biz-com1
│  │  │  └─...
│  │  ├─pages/
│  │  │  ├─page1/
│  │  │  │   ├─subpage1
│  │  │  │   └─...
│  │  │  └─...
│  │  └─store/
│  │      └─modules
│  └─pc/
├─public/
│  └─doc_resource/
│      ├─schedule-form
│      └─smile-form
└─static/
```

### 入口文件 - 可由工具生成

入口文件包括了对该项目中所有文件的引用，可由工具生成

* Capacity/mobile.js
* Capacity/mobile.css
* Capacity/pc.js
* Capacity/pc.css

他们对应各自名称的目录内所有 js文件、css文件

### main.js - 开发入口




## 页面说明

以文件夹并包含3个文件为完整的一个页面。名称都与文件夹名称一致，便于debug

例如页面名称为page1，应创建如下格式：
* page1/
* page1/page1.js
* page1/page1Impl.js
* page1/page1.css （可选）

### page1.js - 页面布局

export 对象提供给 Vue 使用，具体语法参考 Vue 文档。

特别注意，该文件仅编写 template属性，可配合页面设计器生成该文件代码，所以请不要在此编写任何js逻辑。 

js逻辑在 Impl.js 文件中编写

```js
import impl from './page1Impl.js';
export default {
    template:`
    	<div>开始的页</div>
    `,
    mixins:[impl]
}
```



### page1Impl.js - 页面 js 逻辑

编写规则参见 Vue 文档

```js
export default {
    data() {
        return {};
    },
};
```
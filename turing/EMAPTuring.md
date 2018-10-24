# Turing for EMAP 前端开发框架

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
| [ECMAScript: Promise](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise) |  |
| [ECMAScript: Reflect](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Reflect)  |  |
| DOMTokenlist / classList / relList | DOM API * |
| requestAnimationFrame / cancelAnimationFrame | CSS功能 * |

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
├─Adjustment/
│  ├─mobile/
│  │  ├─index.js (ES5语法)
│  └─pc/
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
│  │  ├─private-router.js
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


### Capacity & Branch & Adjustment

与EMAP的合并策略一致

对原有产品覆盖，包名： 产品文件夹名 + $A。还可以有 $B、$C 等

覆盖原则为，项目中 同路径 且 同名的文件 会根据优先级覆盖，优先级： $A、$B、$C ...

* Capacity 为产品源码目录。产品所有功能都该目录下开发。定制包中如果有对于 Capacity 文件夹覆盖，则判定为C级定制。产品不可升级。
* Branch 为定制分支功能源码目录。打包过程中，文件参与打包。定制包中对 Branch 文件夹覆盖，判定为B级定制，产品可升级。
* Adjustment 为产品扩展目录。该文件夹下的代码允许被动态替换，所以必须使用ES5语法


标识为 turingBoot 的 script标签

```html
<script id="turingBoot" src="http://res.wisedu.com/fe_components/turing-form/turing_loader_Capacity.js" backup-source></script>
```

Branch 入口文件（如果需要）

```html
<link rel="stylesheet" href="../Branch/mobileBranch.min.css" backup-href="../Branch/mobile.css">
<script src="../Branch/mobileBranch.min.js" backup-type="module" backup-src="../Branch/mobile.js"></script>
```

Adjustment 入口（如果需要）

```html
<script src='/oadx2_71/sys/newoaydapp/Adjustment/mobile/index.js'></script>
```

完整的示例如下：

```html
<script src='/oadx2_71/sys/newoaydapp/Adjustment/mobile/index.js'></script>
<link rel="stylesheet" href="../Branch/mobileBranch.min.css" backup-href="../Branch/mobile.css">
<script src="../Branch/mobileBranch.min.js" backup-type="module" backup-src="../Branch/mobile.js"></script>
<script type="text/javascript" src="http://res.wisedu.com/fe_components/turing-form/wisedu-vue.mobile.min.js"></script>
<script id="turingBoot" src="http://res.wisedu.com/fe_components/turing-form/turing_loader_Capacity.js" backup-source></script>
```


### turing_loader_Capacity.js 作用

1. 页面加载动画
2. 合并服务端返回的有权访问的路由信息
3. 主题色切换
4. 开发时态与运行时态 js 切换加载
5. 加载了 EMAP 特征的实现


### 入口文件 - 可由工具生成

入口文件包括了对该项目中所有文件的引用，可由工具生成

* Capacity/mobile.js
* Capacity/mobile.css
* Capacity/pc.js
* Capacity/pc.css

他们对应各自名称的目录内所有 js文件、css文件

*特别提示，三方的库以及css，请放在 public 目录下，使用src的方式在html*

### main.js - 开发入口

主要包含以下功能：

```js
//私有路由，用于子页面跳转等。
import route from './private-router.js';

//合并公开路由，一般是根据权限过滤的一级菜单。
var router = window.TG_MergePublicRouter(route.routes);

let config = {
    data() {
        return {
            //整体布局组件所需要的页头完整的参数，如logo、菜单、用户信息等
            header: window.TG_getHeaderInfo(window.TG_CONFIG.header)
        };
    },
    created() {
    },
    mounted() {

    },
    router
};
var app = new Vue(config).$mount('#page');
//清除加载动画
document.querySelector('#page').classList.remove('__hide')
document.querySelector('.app-loading').classList.remove('app-loading-show')
```

### private-router.js - 路由清单

结构参考 Vue Router

```js
import queryFiles from './pages/query/files/files.js';
import queryFileDetail from './pages/query/files/fileDetail.js';
import queryFileReply from './pages/query/files/fileReply.js';

export default {
    routes: [{
        path: '/xxwj',
        name: 'xxwj',
        component: queryFiles,
        children: [{
            path: 'fileDetail',
            name: 'xxwjDetail',
            component: queryFileDetail
        }, {
            path: 'fileReply',
            name: 'xxwjReply',
            component: queryFileReply
        }]
    }]
}
```

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


## 局部组件 - components/

组件都写在 components/ 目录下，按照Vue完整的写法进行编写

```js
//dutyReportHandle.js
export default {
  name: 'duty-report-handle',
  template: ` <div class="container dutyReportHandle">
        <img class="img" src='../static/assets/PC.png' /><span class="dutyReport">请进入PC端进行上报</span>
    </div>`,
  data() {
    return {

    };
  }
};
```

使用的页面使用 [Vue 局部注册](https://cn.vuejs.org/v2/guide/components-registration.html#%E5%B1%80%E9%83%A8%E6%B3%A8%E5%86%8C)

```js
//xxxImpl.js
import dutyReportHandle from '../../components/dutyReportHandle.js';
export default{
  el: '#app'
  components: {
    [dutyReportHandle.name]: dutyReportHandle
  }
}

//xxx.js
import impl from './xxxImpl.js';
export default {
    template:`
    	<duty-report-handle>开始的页</duty-report-handle>
    `,
    mixins:[impl]
}
```

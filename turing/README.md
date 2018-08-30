## Turing 前端开发框架

### 可与后端公用开发环境

可以在后端环境（如：java、node）集成开发，无需实时前端编译。

开发时使用 Chrome 63 以上，使用 es6 的语法特性，进行开发调试。集成 Vue、Vue Router、Vuex

提供独立的 tgbuilder 程序进行编译打包处理（win64 / linux / macOS），内部集成 node环境 和 webpack 配置，运行命令即可编译



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
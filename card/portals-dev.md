# 使用说明

### 环境安装
1. 安装node.js[下载](https://nodejs.org/en/)

2. 安装依赖包，执行命令：npm install

3. 运行环境，执行命令： node app.js

4. 在浏览器输入地址：localhost:9999/views/index.html


### 开发卡片的配置
1. 打开配置文件 /config/config.js
2. 修改 config.js 字段 environment 为 dev
3. 修改 config.js 字段 dev.cards.path.url 为卡片访问地址


### 内嵌应用-菜单的配置
1. 打开配置文件 /config/config.js
2. 在文件夹 /dev/extends/menu/ 下，添加卡片开发文件夹，请参照（/dev/extends/menu/two_panel）
3. 修改 config.js 字段 environment 为 dev
4. 修改 config.js 字段 dev.extends.category 为menu，即你要开发的应用类型
5. 修改 config.js 字段 dev.extends.name 为应用名称（如：two_panel）
5. 修改 config.js 字段 dev.extends.container 为应用展示位置，header为显示在头部区域，container为显示在卡片上
6. 文件名统一使用extend
7. 开发时使用的id、css类名，都必须有前缀（为了避免与其他应用出现冲突），一般与文件夹名一致
8. 该应用开发不可使用插件，首页提供的公共API和方法请参看"OA首页开发API"



### 内嵌应用-消息的配置
1. 打开配置文件 /config/config.js
2. 在文件夹 /dev/extends/news/ 下，添加卡片开发文件夹，请参照（/dev/extends/menu/two_panel）
3. 修改 config.js 字段 environment 为 dev
4. 修改 config.js 字段 dev.extends.category 为news，即你要开发的应用类型
5. 修改 config.js 字段 dev.extends.name 为应用名称（如：two_panel）
6.开发规范与菜单一致

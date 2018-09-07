# layout-tmb 上中下布局

![上中下布局](../static/layout-tmb.png)

## 代码示例

```html
<layout-tmb v-bind="header">
    <div slot="content">
        <router-view></router-view>
    </div>
    <div slot="footer">
        金智教育
    </div>
</layout-tmb>
```

```js
export default {
    data(){
        return {
            header:{
                appName:"应用的名字",
                activeName:"B",
                logo:"http://my.wisedu.com/new/portal/custom/img/logo/logo-mini.png",
                userImage:"http://my.wisedu.com/portal/img/icon/user-role-teacher.png",
                userName:"qiyu",
                logoutUrl: "",
                menu:[{
                    name:"A",
                    icon:"ios-people",
                    uri:"http://www.baidu.com"
                },{
                    name:"B",
                    uri:"#/table"
                },{
                    name:"C",
                    uri:""
                },{
                    name:"D",
                    uri:"",
                    icon:"stats-bars",
                    items:[{
                        name:"DD",
                        icon:"settings",
                        uri:""
                    }]
                }],
                dropMenu:[{
                    name:"个人中心",
                    callback: function() {
                        alert("个人中心");
                    }
                },{
                    name:"退出",
                    url:"http://www.baidu.com",
                    callback: function() {
                        alert("退出");
                    }
                }]
            }
        };
    },
}
```


## 属性

| 参数 | 说明 | 类型 | 可选值 | 默认值 |
|------|-------|---------|-------|--------|
| appName | 应用的名字 | String |  |  |
| menu | 菜单数据 | Array | `[{"name":"A","icon":"ios-people","url":"http://www.baidu.com"},{"name":"D","url":"","icon":"stats-bars","items":[{"name":"DD","icon":"settings","url":""}]}]` |  |
| logo | logo url地址 | String |  |  |
| userImage | 用户头像url | String |  |  |
| userName | 用户名称 | String |  |  |
| logoutUrl | 登出地址 | String |  |  |
| dropMenu | 下拉菜单 | Array | `[{id:"role1",text:"角色1",active:"true"}]` |  |
| navPath | 导航路径，层级以数组顺序决定 | Array | `[{"name":"应用","icon":"ios-people","url":"http://www.baidu.com"},{"name":"菜单","url":"http://www.baidu.com"},{"name":"页面","url":"http://www.baidu.com"}]` |  |
| header | 整个头部插槽 | Slot |  |  |
| logo | logo 插槽 | Slot |  |  |
| menu | menu 插槽 | Slot |  |  |
| nav | 路径导航插槽 | Slot | | |
| content | 内容插槽 | Slot |  |  |
| footer | 页脚插槽 | Slot |  |  |


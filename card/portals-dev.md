


### js模板

```
/**
 * 在页面加载时触发
 * @param data
 * @param data.position {object} 被点击的功能块的位置信息（top，bottom，left，right，width，height）
 * @param data.target {object} 被点击的功能块dom对象
 * @private
 */
function onloaded(data) {

}

/**
 * 每次点击该应用所配置的触发功能块时，都会执行
 * @param data
 * @param data.position {object} 被点击的功能块的位置信息（top，bottom，left，right，width，height）
 * @param data.target {object} 被点击的功能块dom对象
 * @private
 */
function init(data) {

}

/**
 * 当点击并非该应用所配置的触发功能块时，都会执行
 * @param data
 * @private
 */
function destroy(data) {

}
```
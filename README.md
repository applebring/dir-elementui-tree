##自定义树图角色管理插件
> A tree component base on Elementui
```
组件属性(component props):
```
## 配置参数selector,params
字段(props)|参数值(default value)|注释(describe)
-|-|-|  
dataarr| array []|加载树图所需数组
id|string|节点id,唯一标识
label|string|节点名称
searchtext|string|模糊搜索字段，用于输入框模糊搜索
defaultsel| array []|树图默认选中项
defaultChecked|array []|左侧选中树图id
visibledismiss|Boolean|是否展示取消按钮
```
```
##方法:
-|-|-|
名称 (method name)|返回值(value the method return)|注释(describe)
tree-submit|data(Array[]) 选中项|提交按钮事件
close-modal| 无  |  关闭模态框，取消按钮事件     
## Build Setup

``` bash
#install tabaodb
npm install -g cnpm --registry=https://registry.npm.taobao.org

# install dependencies
cnpm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).

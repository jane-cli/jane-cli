## jane
+ [https://github.com/lin-hun/jane](https://github.com/lin-hun/jane)

## install
+ npm install -g @linhun/jane-cli

## usage
+ jane --help

## 插件机制
+ css 
```javascript
let less = require('less')
let fs = require('fs')
// {file:'path'}
module.exports = (option)=>{
	return new Promise((resolve,rej)=>{
	less.render(fs.readFileSync(option.file,'utf8'))
    .then(function(output) {
    	resolve(output)
     },
     function(error) {
     	rej(error)
    })
})
}
```
+ js 基于babel
[babel插件文档](https://github.com/jamiebuilds/babel-handbook/blob/master/translations/zh-Hans/plugin-handbook.md)

## 参数
使用`--using-plugin`可以将所有js代码中的 `requirePlugin` 转换成普通的`require`语句
只需要在项目目录中新建一个`plugin`目录，并且将对应代码放进去就行。
```bash
myXcxProjectSrcDir
|-- app.json
|-- app.js
|-- app.scss
|-- plugin
|   |-- myPlugin1
|   |   |-- index.js
|   |
|   |-- myPlugin2
|
|-- pages
|   |-- index
|       |-- index.js
|       |-- index.scss
|       |-- index.json

```
pages/index/index.js
```javascript

const app = getApp();
const myPlugin = requirePlugin('myPlugin1')

Page({
    ...
})
```
will be trans to bellow
pages/index/index.js
```javascript

const app = getApp();
const myPlugin = require('./plugin/myPlugin1/index.js')

Page({
    ...
})
```
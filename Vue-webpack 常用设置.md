# Syllabus:
1. 添加支持Jade/ Pug依赖
2. 生产编译环境去掉Console.log
3. 给生产环境和发布环境配置不同的接口地址

---

## 1. 添加支持Jade/ Pug依赖
**1、首先安装相关依赖。 **

```
// 安装支持pug依赖 
npm install pug pug-loader pug-filters -D (-D=== --save-dev)
// 安装支持jade依赖 
npm install jade jade-loader -D 
// 安装支持scss依赖 
npm install sass sass-loader node-sass -D
```

**2、安装完成后，进入到/build目录下，打开webpack.base.conf.js 文件，**module.rules**内添加： **
```
{
	test: /\.scss$/,
	loader: 'style!css!sass?sourceMap'
},
{
	test: /\.jade$/,
	loader: "jade"
},
{
	test: /\.pug$/,
	loader: 'pug'
},
```

**3、使用pug，scss语法 **
```
//使用pug语法
<template lang="pug">
	***
</template>
//使用scss语法
<style lang="scss">
	***
''</style>
```

---
## 2. 生产编译环境去掉Console.log

webpack.prod.conf.js 的 plugins 里面加上:
> drop_debugger: true,
> drop_console: true
变成:
```
new webpack.optimize.UglifyJsPlugin({
	compress:{
		warnings: false,
		drop_debugger: true,
		drop_console: true
	}
})
```
---

## 3. 给生产环境和发布环境配置不同的接口地址

1、分别设置不同的接口地址
> /config/dev.env.js
> /config/prod.env.js

这两个文件就是针对生产环境和发布环境设置不同参数的文件。

2、分别在两个文件中添加**API\_ROOT**
```
@: dev.env.js
var merge = require('webpack-merge')
var prodEnv = require('./prod.env')

module.exports = merge(prodEnv, {
	NODE_ENV: '"development"',
	API_ROOT: '"//127.0.0.1:1337/"'
})
```
```
@:prod.env.js
module.exports = {
	NODE_ENV: '"production"',
	API_ROOT: '"//api.ftisland.com/"'
}
```

3、调用参数
在需要调用API的位置使用：
```
// 配置API接口地址
var root = process.env.API_ROOT
```
重启项目，配置生效。
```
npm run dev // 开发环境接口
npm run build // 自动切换到生产环境接口
```

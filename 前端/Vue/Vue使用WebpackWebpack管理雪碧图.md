**1、安装webpack-spritesmith**
```
npm install --save-dev webpack-spritesmith
```
**2、webpack.config.js添加如下代码：**
```
var SpritesmithPlugin = require('webpack-spritesmith');

module.exports = {
	//代码
	plugins: [
		new SpritesmithPlugin({
			// 目标小图标
			src: {
				cwd: path.resolve(__dirname, './src/assets/imgs/icons'),
				glob: '*.png'
			},
			// 输出雪碧图文件及样式文件
			target: {
				image: path.resolve(__dirname, './dist/sprites/sprite.png'),
				css: path.resolve(__dirname, './dist/sprites/sprite.css')
			},
			// 样式文件中调用雪碧图地址写法
			apiOptions: {
				cssImageRef: '../sprites/sprite.png'
			},
			spritesmithOptions: {
				algorithm: 'top-down'
			}
		})
	]
}
```
**3、执行webpack打包指令,执行后打包生成dist/sprites/文件**

**4、index.html文件中引入sprite.css，如：**
```
<link rel="stylesheet" type="text/css" href="./dist/sprites/sprite.css" /\>
```
**5、App.vue中通过class引用小图标（具体图标class进入sprite.css查看），如：**

i标签是行内元素，可以添加css为i.icon{display:inline-block}

**6、重启服务**

---

[参考:webpack雪碧图实现（webpack管理小图标素材）](https://segmentfault.com/a/1190000008630212)



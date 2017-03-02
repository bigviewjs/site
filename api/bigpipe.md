## 介绍

https://github.com/bigviewjs/bigview.js

针对bigview前端优化，参考微博的方式

## 使用

在布局模板里引入bigpipe.js即可

## 生命周期

- bigview.ready
- bigview.view
- bigview.end

## 事件

- pageletArrive：当pagelet到达页面的时候，触发bigview默认的pageletArrive
- domid事件

```
var loaded_modules = [];

bigview.on('pageletArrive', function(payload) {
	loaded_modules.push({'domid': payload.domid})
});
```

可以在页面中获取加载的模块顺序，继而完成某些功能，比如根据页面加载模块，显示右侧导航等。

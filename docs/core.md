## bigview

针对视图渲染和模块进行的封装，主要用于管理模块和提供生命周期回调。

## biglet即pagelet

biglet是pagelet的别名，提供了生命周期封装，包括before、fetch、parse、end等，这样更加便于组装带有http接口请求的模块。

由于bigpipe的特点，在特别大的页面里，返回数据优先渲染，保证首屏渲染速度，并且在某些情况下，可以允许某些模块因网络请求或者其他原因的延时显示，甚至不显示也没有问题。

如果模块设计的好

- 无依赖
- 可以进行独立发布和测试
- 模块可以有子模块

无论出于哪种考虑，biglet都可以非常好的支持。

## 渲染模式

支持5种bigpipe渲染模式

- parallel.js   并行模式， 先写布局，并行请求，但在获得所有请求的结果后再渲染
- pipeline.js  (默认) 管线模式：即并行模式， 先写布局，并行请求，并即时渲染
- reduce.js    顺序模式： 先写布局，按照pagelet加入顺序，依次执行，写入
- reducerender.js 先写布局，然后顺序执行，在获得所有请求的结果后再渲染
- render.js 一次渲染模式：即普通模式，不写入布局，所有pagelet执行完成，一次写入到浏览器。支持搜索引擎，用来支持那些不支持JS的客户端。

## 生命周期

bigview的生命周期

- before
- .then(this.beforeRenderLayout.bind(this))
- .then(this.renderLayout.bind(this))
- .then(this.afterRenderLayout.bind(this))
- .then(this.beforeRenderPagelets.bind(this))
- .then(this.renderPagelets.bind(this))
- .then(this.afterRenderPagelets.bind(this)
- end

bigview的生命周期精简

- before
- renderLayout
- renderPagelets
- end

biglet的生命周期

- before
- .then(self.fetch.bind(self))
- .then(self.parse.bind(self))
- .then(self.render.bind(self))
- end
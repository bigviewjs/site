
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
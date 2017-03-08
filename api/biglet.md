## 生命周期

- before 准备或预处理
- fetch 网络请求
- parse 解析处理数据（E抽取、T转换、L加载、C清洗）
- compile（不对外暴露）
- render（不对外暴露）
- end 结束前要处理

每个生命周期都要遵循一个原则，结果必须返回promise对象，否则无法正常运行。

## 子模块

```js
'use strict'

const debug = require('debug')('bigview')
const fs = require('fs')
const MyBigView = require('./MyBigView')
const Biglet = require('../../../packages/biglet')

module.exports = function (req, res) {
  var bigpipe = new MyBigView(req, res, 'nest/index', { title: "测试" })

  var Pagelet1 = require('./p1')
  var pagelet1 = new Pagelet1()
    
  // pipeline | parallel | reduce | reducerender | render
  pagelet1.mode = 'pipeline'

  var Pagelet2 = require('./p2')

  pagelet1.addChild(Pagelet2)

  bigpipe.add(pagelet1,Biglet)

  // bigpipe.preview('aaaa.html')
  // bigpipe.isMock = true
  // bigpipe.previewFile = 'aaaa.html'

  bigpipe.start()
}
```

说明

- 通过pagelet1.addChild方法来增加子模块
- pagelet1.mode = 'pipeline'是用来设置子模块的请求模式的，支持的和bigview的mode是一样的

## 自定义payload

在biglet里

```js
this.payload = {
	a : 1,
	b : 2
}
```

然后在前端

```js

bigview.on('pageletArrive', function(payload) {
  console.log(payload.a) //1
  console.log(payload.b) //2
})
```
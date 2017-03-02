## 组件

- bigview（Node.js）视图的基类
- biglet（Node.js）模块的基类
- bigview.js（前端引用）

## 特性

- 模块化
- 具有测试性
- 支持mock数据
- 生成html片段（便于对比）
- 提供Scaffold（bigview-cli）
- 提供调试UI（bigconsole）

## 功能点

- 支持静态布局和动态布局
- 支持5种bigpipe渲染模式
  - parallel.js   并行模式， 先写布局，并行请求，但在获得所有请求的结果后再渲染
  - pipeline.js  (默认) 管线模式：即并行模式， 先写布局，并行请求，并即时渲染
  - reduce.js    顺序模式： 先写布局，按照pagelet加入顺序，依次执行，写入
  - reducerender.js 先写布局，然后顺序执行，在获得所有请求的结果后再渲染
  - render.js 一次渲染模式：即普通模式，不写入布局，所有pagelet执行完成，一次写入到浏览器。支持搜索引擎，用来支持那些不支持JS的客户端。
- 支持子pagelet，无限级嵌套
- 支持根据条件渲染模板，延时输出布局
- bigview支持错误模块显示，仅限于布局之前

## 感谢

- 冯地木
- 张凯mik
- 张代应
- 陈愉镔
- 马涛told
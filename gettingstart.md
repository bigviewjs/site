## 开发过程概览

1. 编写静态页面
1. 根据静态页面和功能切分模块，并决定采用的视图渲染模式
1. 准备项目目录，并编写具体模块
1. QA+测试
1. 部署

了解开发过程，提前做好准备工作，避免项目里的反复，下面就跟着我一起开始bigview入门吧

## 安装bigview

```bash
$ npm i -S bigview
```

## 路由定义

采用express的路由定义方式

```js
router.get('/some_url',
    auth(), //检查权限
    require('../bpmodules/detail'));
```

## 创建bigview对象

代码位于`/bpmodules/detail/index.js`，内容如下：

```
'use strict';

const BigView = require('bigview');

module.exports = function(req, res) {
    let bigview = new BigView(req, res,
        'pages/detail/index', {
            title: "国内机票-去哪儿网Qunar.com"
        });
    
    bigview.add(require('./header'));
    bigview.add(require('./menu'));
    bigview.add(require('./zzz'));
    bigview.add(require('./yyy'));
    bigview.add(require('./xxx'));
    bigview.add(require('./sidebar'));
    bigview.add(require('./footer'));
    
    bigview.addErrorPagelet(require('./error'));

    bigview.start();
}

```

要点说明

1. 创建bigview对象，可以是BigView或者BigView子类的实例化对象
1. 通过bigview.add方法增加模块
1. 通过bigview.addErrorPagelet方法增加出错显示的模块
1. 通过bigview.start()来开始渲染视图


> 说明：bigview支持5种渲染模式 pipeline | parallel | reduce | reducerender | render，默认是采用是性能最好的pipeline模式，如果需要可以通过bigview.mode来设置。

## 创建模块

安装脚手架

```bash
$ npm i -g bigview-cli
```

创建多个模块

```bash
$ bpm a b c
generate ~/a/MyPagelet.js
generate ~/a/index.html
generate ~/a/index.js
generate ~/a/req.js
generate ~/b/MyPagelet.js
generate ~/b/index.html
generate ~/b/index.js
generate ~/b/req.js
generate ~/c/MyPagelet.js
generate ~/c/index.html
generate ~/c/index.js
generate ~/c/req.js
```

### 模块目录

```
$ tree bpmodules/detail/header 
bpmodules/detail/header
├── const.js
├── index.js
├── parse.js
└── tpl
    └── index.handlebars

1 directory, 4 files
```

说明

- index.js是入口，继承biglet
- const.js用于定义常量
- parse.js用于解析数据，用于etl数据处理（抽取、转换、加载、清洗）
- tpl是防止模板的目录，默认biglet使用的是tpl/index

### index.js
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
copy tpl /bigview_site/test/a/tpl
copy tpl /bigview_site/test/b/tpl
copy tpl /bigview_site/test/c/tpl
generate /bigview_site/test/a/const.js
generate /bigview_site/test/b/const.js
generate /bigview_site/test/c/const.js
generate /bigview_site/test/a/parse.js
generate /bigview_site/test/a/index.js
generate /bigview_site/test/b/index.js
generate /bigview_site/test/b/parse.js
generate /bigview_site/test/c/parse.js
generate /bigview_site/test/c/index.js
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

```
'use strict'

const Pagelet = require('biglet')

module.exports = class QPagelet extends Pagelet {
  constructor() {
    super()
    this.root = __dirname
    this.domid = 'a'
  }

  fetch() {
    return Promise.resolve()
  }
  
  parse() {
      return Promise.resolve()
  }
}

```

### const.js

```
'use strict';

module.exports = {
    "changeStatus" : {
        'CHANGING': 40,
        'CHANGE_DONE': 42
    }
};
```

### parse.js

```
'use strict';

const { changeStatus } = require('./const');
const { CHANGING, CHANGE_DONE} = changeStatus;

module.exports = function(pagelet) {
    let data = {
      a:1
    };

    return Promise.resolve(data);
};

```

### tpl/index.handlebars


```
<div class="m-warp m-line">
	<h1> hello world </h1>
</div>

```

## 启动和部署

由于项目是express项目，只是view变成了bigview，所以启动和部署都和express一模一样。

## 下面就开始你的项目吧

有任何问题请issue
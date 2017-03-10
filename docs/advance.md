
## 扩展bigview

主要是根据bigview的生命周期来实现某种功能

```
'use strict';

const BigView = require('bigview');

module.exports = class QBigView extends BigView {
	afterRenderLayout(data) {
		....
	}
}

```

## 扩展biglet 

```
'use strict'

const Pagelet = require('biglet');

module.exports = class MyPagelet extends Pagelet {
    constructor() {
        super();
        this.root = __dirname;
        this.domid = 'reimburse';
    }
    
    parse() {
        let pagelet = this;
        return new Promise(function(resolve, reject) {
            return parse(pagelet).then(function (data) {
                resolve(pagelet.data = data);
            });
        });
    }

    fetch() {
		... 
    };
}
```

## bigview与异步流程控制

讲解不同模式，如何使用异步流程控制来处理

## bigview与浏览器渲染

浏览器bigview.js实现与渲染原理，以及可以做的事儿

## bigview与微服务

- 无处不在的Node.js：Proxy层、api层

## bigview与移动端hybrid

双向绑定、VirtualDom


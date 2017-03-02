
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
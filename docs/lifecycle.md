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
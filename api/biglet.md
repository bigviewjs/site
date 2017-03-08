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
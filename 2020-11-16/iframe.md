#### iframe页面间的通信（跨域可实现）

子页面js
```js
 $("#id1").click(function() {
    var fun="click"; // 传递的信息
    window.parent.postMessage(fun, '*'); // 向父页面推送消息
    // window.parent.postMessage(fun, 'http://example.com'); // 向指定页面推送消息
  })
```

父页面js
```js
// 监听消息
window.addEventListener('message', function(e) {
    console.log(e);
    var fun = e.data;
    if (fun == "click") {
        alert("aaa");    
    }
}, false);
```
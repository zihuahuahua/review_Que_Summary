#### iframe页面间的通信（跨域可实现）

- 1 iframe向父页面传递消息

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

- 2 父页面向iframe传递消息

父页面js
```js
//获取iframe元素
iFrame = document.getElementById('myframe')
 
//iframe加载完毕后再发送消息，否则子页面接收不到message
iFrame.onload = function(){
  iFrame.contentWindow.postMessage('MessageFromIndex','*');
}
```

iframe页面
```js
// 需在页面渲染前开始监听
window.addEventListener("message", function(e){
  console.log(e)
  var fun = e.data;
  if (fun == "MessageFromIndex") {
      alert("aaa");    
  }
}, false);
```

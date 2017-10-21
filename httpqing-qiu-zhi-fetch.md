# http请求之fetch

我们都知道，在网页向服务器发送请求使用最多的技术就是ajax，或者在其他框架中使用第三方封装的http 工具库（如axios、$http等），今天我们来介绍一下浏览器提供的一个新兴的API：fetch，原生ajax 接口。同时，它还提供了一个全局的方法 fetch\(\)，为异步请求资源更加简洁的方法。

fetch 提供了许多与XMLHttpRequest 相同的功能，但它的设计更易于扩展和高效。

## ajax 的原理

```
var xhttp = new XMLHttpRequest();
  xhttp.onreadystatechange = function() {
    if (this.readyState === 4 && this.status === 200) {
      console.log(this.responseText);
    }
  };
  xhttp.open("GET", "/", true);
  xhttp.send();
```

看了上面的代码是不是感觉很麻烦？

正如很多前端框架的流行（react.js、vue.js 和 angular.js），都是在底层对 XMLHttpRequest 进行封装，像jQuery 使用$.ajax 一样，直接提供简单的方式即可实现ajax 请求，那么fetch 实现的原理，其实直接将$.ajax、$http 等这些方法直接进一步封装，直接让浏览器直接调用。

## 如何使用 fetch？

因为是新兴的API，在使用fetch 时，我们有必要了解一下 fetch **兼容性**，如下图：![](/assets/fetch.png)如何处理这里的兼容问题呢？

我们需要借助 [Fetch polyfill](https://github.com/github/fetch) 来实现 fetch 功能。
















































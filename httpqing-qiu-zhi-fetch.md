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

正如很多前端框架的流行（react.js、vue.js 和 angular.js），都是在底层对 XMLHttpRequest 进行封装，像jQuery 使用$.ajax 一样，直接提供简单的方式即可实现ajax 请求，那么fetch 实现的原理，其实直接将$.ajax、$http 等这些方法直接进一步封装，直接让浏览器直接调用，且 fetch 是基于 [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) 实现的。

## 与 jQuery.ajax 的不同

* fetch 在服务器不会对 404 和 500 抛出错误，而是手动通过 ok 字段和 status 字段进行调试判断
* 默认情况下，fetch 并不会向服务器发送或接受cookie，必须在 **Header** 参数上加 **credentials: ‘include’ **配置

## 如何使用 fetch？

因为是新兴的API，在使用fetch 时，我们有必要了解一下 fetch **兼容性**，如下图：![](/assets/fetch.png)如何处理这里的兼容问题呢？

我们需要借助 [Fetch polyfill](https://github.com/github/fetch) 来实现 fetch 功能。

## fetch 接口

* [Body](https://developer.mozilla.org/en-US/docs/Web/API/Body)
* [Header](https://developer.mozilla.org/en-US/docs/Web/API/Headers)
* [Request](https://developer.mozilla.org/en-US/docs/Web/API/Request)
* [Response](https://developer.mozilla.org/en-US/docs/Web/API/Response)

## 使用方法

### 创建请求

```
var myImage = document.querySelector('img');

fetch('flowers.jpg').then(function(response) {
  return response.blob();
}).then(function(myBlob) {
  var objectURL = URL.createObjectURL(myBlob);
  myImage.src = objectURL;
});
```

上面代码是请求一个图片然后对图片在做处理，此处形成实体的图片需要借助 [blob\(\)](https://developer.mozilla.org/en-US/docs/Web/API/Body/blob) 方法，由[ Blob ](/objectURL)实例创建objectURL 然后将其插入img 标签中。

### 设置请求选项

```
var myHeaders = new Headers();

var myInit = { method: 'GET',
               headers: myHeaders,
               mode: 'cors',
               cache: 'default' };

fetch('flowers.jpg', myInit).then(function(response) {
  return response.blob();
}).then(function(myBlob) {
  var objectURL = URL.createObjectURL(myBlob);
  myImage.src = objectURL;
});
```

fetch\(\) 方法的第二个参数是初始化的请求选项，可以通过一个 myInit 对象根据需求设置。[所有选项参数入口](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/fetch)。

### 发送带有认证（credentials）的请求

#### 跨资源请求

```
fetch('https://example.com', {
  credentials: 'include'  
})
```

#### 同源请求

```
// The calling script is on the origin 'https://example.com'

fetch('https://example.com', {
  credentials: 'same-origin'  
})
```

#### 不带认证的请求

```
fetch('https://example.com', {
  credentials: 'omit'  
})
```

### 检查请求是否成功

```
fetch('flowers.jpg').then(function(response) {
  if(response.ok) {
    return response.blob();
  }
  throw new Error('Network response was not ok.');
}).then(function(myBlob) { 
  var objectURL = URL.createObjectURL(myBlob); 
  myImage.src = objectURL; 
}).catch(function(error) {
  console.log('There has been a problem with your fetch operation: ' + error.message);
});
```

### 自定义请求对象

```
var myHeaders = new Headers();

var myInit = { method: 'GET',
               headers: myHeaders,
               mode: 'cors',
               cache: 'default' };

var myRequest = new Request('flowers.jpg', myInit);

fetch(myRequest).then(function(response) {
  return response.blob();
}).then(function(myBlob) {
  var objectURL = URL.createObjectURL(myBlob);
  myImage.src = objectURL;
});
```

这里需要借助 [Request\(\)](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request) 方法才能自定义请求对象。

## 参考

* [fetch API  mdn](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)
* [fetch example](https://github.com/mdn/fetch-examples/)








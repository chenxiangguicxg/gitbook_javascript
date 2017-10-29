# axios 详解

Axios 是一个基于Promise 的 HTTP 库，可以用在浏览器和 node.js  中。

## 特点

* 从浏览器中创建 XMLHttpRequests
* 从 node.js 创建 http 请求
* 支持 Promise API
* 拦截请求和响应
* 转换请求数据和响应数据
* 取消请求
* 自动转换 JSON 数据
* 客户端支持防御 XSRF 

## 浏览器兼容

![](/assets/axiosCompatibility.png)

## 安装

使用 npm 

```
npm install axios
```

使用 bower

```
bower install axios
```

使用 cdn

```
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
```

## 使用示例

### 执行一个 GET 请求

```
// 位给定的用户 ID 创建请求
axios.get('/user?ID=12345')
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });
 
// 参数可选，上面的写法也可以这样做
axios.get('/user', {
    params: {
      ID: 12345
    }
  })
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });
```

### 执行 POST 请求

```
axios.post('/user', {
    firstName: 'firstName',
    lastName: 'lastName'
})
.then(function(res) {
    console.log(res);
})
.catch(function(err) {
    console.log(err);
});
```

### 执行多个并发请求

```
function getUserAccount() {
    return axios.get('/user/12345');
}

function getUsetPermissions() {
    return axios.get('/user/12345/permissions')
}

axios.all([getUserAccount(), getUserPermissions()])
    .then(axios.spread(function (acct, pers) {
        // 两个请求现在都执行完成
    }));
```

## axios API

通过向 axios 传递相关参数创建请求

#### axios\(config\)

```
// 发送 POST 请求
axios({
    method: 'post',
    url: '/user/12345',
    data: {
        firstName: 'frstName',
        lastName: 'lastName'
    }
});
```

```
// 获取远程图片资源
axios({
    method: 'get',
    url: 'http://bit.ly/2mTM3nY',
    responseType: 'stream'
})
.then(function(res) {
    res.data.pipe(fs.createWriteStream('ada_lovelace.jpg'))
});
```

#### axios\(url\[,config\]\)

```
// 发送 GET 请求（默认方法）
axios('/user/12345');
```

## 请求方法别名

* **axios.request\(config\)**
* **axios.get\(url\[,config\]\)**
* **axios.delete\(url\[,config\]\)**
* **axios.head\(url\[,config\]\)**
* **post\(url\[, data\[, config\]\]\)**
* **axios.put\(url\[, data\[, config\]\]\)**
* **axios.patch\(url\[, data\[, config\]\]\)**

**注意**

在使用别名方法时，url、method、data 这些属性都不必在配置中指定

### 并发

```
// 处理并发时，需要借助辅助函数
axios.all(iterable)
axios.spread(callback)
```

### 创建实例




















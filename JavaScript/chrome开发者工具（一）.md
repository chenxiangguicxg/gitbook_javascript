# Chrome 开发者工具使用（一）

对于前端开发，总是少不了与浏览器接触，如何能利用好浏览器的开发者工具，是提高工作效率的关键之一。本文以chrome 浏览器为样例，介绍相关的开发者工具的使用。

首先，我们来先了解一下console 的使用：

1、- console.log：普通信息

* console.info：提示类信息

* console.error：错误信息

* console.warn：警示信息

* console.debug：用于输出调试信息![](/assets/开发者工具/consoles.png)

如果再配合 **console.group**  与 **console.groupEnd**，可以将这种分类管理的思想发挥到极致。这适合于在开发一个规模很大模块很多很复杂的Web APP时，将各自的log信息分组到以各自命名空间为名称的组里面。

2、console.log 的第一个参数可以包含一些格式化的指令，比如 **“%c”**

```
console.log('%chello world','font-size:36px;color:green;');
```

输出结果：

![](/assets/开发者工具/import.png)

在控制台上输出一个**图片**：

```
console.log("%c", "padding:50px 300px;line-height:120px;background:url('http://wayou.github.io/2014/09/10/chrome-console-tips-and-tricks/rabbit.gif') no-repeat;");
```

![](/assets/开发者工具/consoleImage.png)

3、console.table：以**表格**的形式输出

```
var data = [{'书名': 'JavaScript高级程序设计', '数量': 1}, {'笔名': 'pencil', '数量': 3}];
console.table(data);
```

![](/assets/开发者工具/consoleTable.png)

4、console.count：**计数**

```
function foo(){
  //其他函数逻辑
  console.count('foo 被执行的次数：');
}
foo();
foo();
foo();
```

![](/assets/开发者工具/consoleCount.png)

5、console.dir：将DOM节点以**JavaScript对象的形式**输出-- 而console.log 输出的是**html 结构**

```
console.dir(document.body)
```

![](/assets/开发者工具/consoleDir.png)

6、console.time & console.timeEnd ： 测试一段代码**执行的时间**

```
console.time("Array initialize");
var array= new Array(1000000);
for (var i = array.length - 1; i >= 0; i--) {
  array[i] = new Object();
};
console.timeEnd("Array initialize");
```

![](/assets/开发者工具/consoleTime.png)

7、console.timeline  &  console.timelineEnd : 记录一段时间轴

8、console.profile &  console.profileEnd : 查看CPU使用的相关信息

```
console.profile("Array initialize");
var array= new Array(1000000);
for (var i = array.length - 1; i >= 0; i--) {
  array[i] = new Object();
};
console.profileEnd ("Array initialize");
```

![](/assets/开发者工具/consoleProfile.png)

在控制台上调试profiles

![](/assets/开发者工具/profileIntro.png)

三种显示性能的调试方法参考：[http://www.h3399.cn/201610/8494.html](http://www.h3399.cn/201610/8494.html)


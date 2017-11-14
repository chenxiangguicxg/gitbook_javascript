# 数组 reduce 的用法

这reduce 方法是数组中常用到的一种迭代的方法，本章将结合相关代码案例深入了解其用法。

首先，我们来看一下简单的一个例子：

```
var arr = [1, 2, 3, 4];
sum = arr.reduce(function(pre, cur, index, arr) {
    console.log(pre, cur, index);
    return pre + cur;
}, 0);
console.log(sum, arr);
```




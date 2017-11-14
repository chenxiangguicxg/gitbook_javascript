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

// 输出结果
0 1 0
1 2 1
3 3 2
6 4 3
10 [1, 2, 3, 4]
```

从上面代码可以看出，数组 reduce 迭代方法的**语法**如下：

```
arr.reduce(callback[, initialValue])
```

**参数解析**

**callback **是执行数组中每个值的函数，有四个参数：

* pre：累加器（第一项值或者上一次累加的结果）
* cur：当前会参加累加的项
* index：数组正在处理的元素的索引值，**如果提供了initialVale 参数，则reduce 从索引值为0开始依次执行 callback 函数，否则从索引值为1 开始执行callback**。
* arr：调用reduce 的数组

**initialValue** 是reduce方法**可选**的第二个参数，**设置 pre 的初始类型和初始值。**

上面的代码，initialValue 值为0，是设置了pre 类型为数值型，返回的结果为数值10，我们也可以对初始值为数值的数据进行一些运算（如进行减10 的操作，返回值是215）：

```
var result = [
    {
        subject: 'math',
        score: 80
    },
    {
        subject: 'chinese',
        score: 95
    },
    {
        subject: 'english',
        score: 80
    }
];
var sum = result.reduce(function(prev, cur) {
    return cur.score + prev;
}, -40);
console.log(sum);
// 215
```

此外，我们还可以通过设置initialValue 类型来设置返回值类型，**对返回的类型进行转换操作**，如下计算数组中每个元素出现次数的例子：

```
var names = ['Alice', 'Bob', 'Tiff', 'Bruce', 'Alice'];
var countedNames = names.reduce((pre, cur) => {
    pre[cur] ? pre[cur] ++ : pre[cur] = 1;
    return pre;
}, []);
console.log(countedNames); 
// [Alice: 2, Bob: 1, Tiff: 1, Bruce: 1]
```

此例子返回的数组，下面返回的是对象（只需把 \[\] 改成 {} 即可）：

```
var names = ['Alice', 'Bob', 'Tiff', 'Bruce', 'Alice'];
var countedNames = names.reduce((pre, cur) => {
    pre[cur] ? pre[cur] ++ : pre[cur] = 1;
    return pre;
}, {});
console.log(countedNames); 
// {Alice: 2, Bob: 1, Tiff: 1, Bruce: 1}
```

**经典例子**

* 扁平化数组

```
var flattened = [[0, 1], [2, 3], [4, 5]].reduce(
  function(a, b) {
    return a.concat(b);
  },
  []
);
// flattened is [0, 1, 2, 3, 4, 5]
```

* 从字符串中找相同字母出现的次数

```
var arrString = 'abcdaabc';
arrString.split('').reduce(function(res, cur) {
    res[cur] ? res[cur] ++ : res[cur] = 1
    return res;
}, {})
// {a: 3, b: 2, c: 2, d: 1}
```

* 使用拓展运算符和initialValue 绑定包含在对象数组的数组

```
var friends = [{
  name: 'Anna',
  books: ['Bible', 'Harry Potter'],
  age: 21
}, {
  name: 'Bob',
  books: ['War and peace', 'Romeo and Juliet'],
  age: 26
}, {
  name: 'Alice',
  books: ['The Lord of the Rings', 'The Shining'],
  age: 18
}];

var allbooks = friends.reduce(function(prev, curr) {
  return [...prev, ...curr.books];
}, ['Alphabet']);

// allbooks = [
//   'Alphabet', 'Bible', 'Harry Potter', 'War and peace', 
//   'Romeo and Juliet', 'The Lord of the Rings',
//   'The Shining'
// ]
```

**兼容性**

![](/assets/reducePolyfill.png)

这里需要注意的是，reduce方法在 IE9 以下的浏览器器不支持。

**与 reduce 类似的方法 是 reduceRight**

两者的区别是：迭代的方向不同，前者方向是从左至右，后者是从右至左。


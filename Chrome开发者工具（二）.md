# Chrome 开发者工具（二）

上一章了解了console 的在控制台中的使用方法，本文来介绍一下开发者工具的快捷键的使用。

1、**Ctrl + p**：快速切换文件（在DevpTools 可以快速搜索和打开你项目中的文件）

```
 ![](/assets/开发者工具/shortcutKey1.png)
```

2、**Ctrl + shift + f**：在源代码中搜索（搜索源代码的字符中特定串）

```
![](/assets/开发者工具/shortcutKey2.png)3、**Ctrl + g**：快速跳转到指定行
```

![](/assets/开发者工具/shortcutKey3.png)

4、**Ctrl + o **：输入“？”，选择相应的操作

![](/assets/开发者工具/shortcutKey4.png)

5、在控制台选择元素

* $\(\)–document.querySelector\(\)简写，返回第一个和css选择器匹配的元素。例如$\(‘div’\)返回这个页面中第一个div元素

* $$\(\)–document.querySelectorAll\(\)的简写，返回一个和css选择器匹配的元素数组。

* $0-$4–依次返回五个最近你在元素面板选择过的DOM元素的历史记录，$0是最新的记录，以此类推。

![](/assets/开发者工具/shortcutKey5.png)

6、使用多个插入符进行选择（在console 面板操作）

     **按住 Ctrl ；鼠标点击要插入的地方**

7、保存记录（勾选在Console标签下的保存记录选项（**Preserve log**），你可以使DevTools的console继续保存记录而不会在每个页面加载之后清除记录。当你想要研究在页面还没加载完之前出现的bug时，这会是一个很方便的方法。）![](/assets/开发者工具/shortcutKey6.png)8、优质打印（或者叫做代码格式化：将页面引入的压缩过的代码解压出来）

     Chrome’s Developer Tools有内建的美化代码，可以返回一段最小化且格式易读的代码。Pretty Print的按钮在Sources标签的左下角**（左下角有一个“{}”的符号）**。![](/assets/开发者工具/shortcutKey7.png)






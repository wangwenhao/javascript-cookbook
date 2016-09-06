# 1.2. 在字符串中提取列表

## 问题

有一个包含若干句子的字符串，其中的一个句子包含了一个列表。这个列表从冒号（:）开始，到句号（.）结束，每个列表项之间用一个逗号分开。你想要提取这个列表。

输入:
```
This is a list of items: cherries, limes, oranges, apples.
```
输出:
```
['cherries','limes','oranges','apples']
```
## 解决方案

这个问题的解决方案需要两个操作：提取出包含这个列表的字符串，然后将它转换成一个列表。

使用`String`的`indexOf()`来定位冒号，再用它来定位这个冒号后的第一个句号。有了这两个位置，就可以用`String`的`substring()`方法来提取出这个字符串了：
``` javascript
var sentence = 'This is one sentence. This is a sentence with a list of items:' +
'cherries, oranges, apples, bananas. That was the list of items.';
var start = sentence.indexOf(':');
var end = sentence.indexOf('.', start+1);
var listStr = sentence.substring(start+1, end);
```
当你有了一个由列表项所组成的字符串之后，使用`String`的`split()`方法来使它成为一个数组：
``` javascript
var fruits = listStr.split(',');
console.log(fruits); // ['cherries', ' oranges', ' apples', ' bananas']
```
## 讨论
`indexOf()`方法的第一个参数是一个需要查找的值，第二个参数是可选的来表示开始的索引位置。

这个列表由一个冒号开始到一个句号结束。`indexOf()`方法在第一次查找的时候省去了第二个参数，来查找冒号。第二次调用的时候从冒号的位置（加1）来查找句号：
``` javascript
var end = sentence.indexOf('.',start+1);
```
如果在查找结束句号的时候不做修改，会查找到一个个句子的句号而不是包含列表的字符串的那个句号。

当我们有了列表的开始和结束位置，我们用`substring()`方法来进行截断，传入字符串开始位置和结束位置的索引值：
``` javascript
var listStr = sentence.substring(start+1, end);
```
提取出来的字符串是：
```
cherries, oranges, apples, bananas
```
然后用`split()`方法来分离这个列表，使之成为一系列独立的值：
``` javascript
var fruits = listStr.split(',') ; // ['cherries', ' oranges', ' apples', ' bananas']
```
还有另外一个提取字符串的方法`substr()`，它从开始位置的索引值开始提取第二个参数指定长度的字符串。可以很容易的用结束位置的索引值减去开始位置的索引值来计算出这个长度：
``` javascript
var listStr = sentence.substr(start+1, end-start);
var fruits = listStr.split(',');
```

## 进阶

分割这个提取出来的字符串的结果是一个由列表项所组成的数组。然而，这些项有一些从句子遗留下来的空格。在大多数的程序里，我们会需要给列表里的项做清理。

我们会在第二章里面详细讨论数组对象，目前，我们使用`Array`的`forEach()`方法和`String`对象的`trim()`方法来清理这个数组：
``` javascript
fruits = listStr.split(',');
console.log(fruits); // [' cherries', ' oranges', ' apples', ' bananas']
fruits.forEach(function(elmnt,indx,arry) {
  arry[indx] = elmnt.trim();
});
console.log(fruits); // ['cherries', 'oranges', 'apples", "bananas"]
```
`forEach()`方法在每一个数组元素上应用作为参数（回调）传入的一个方法。这个回调方法支持三个参数：数组元素的值和两个可选参数，数组元素的索引值和数组本身。

另外还有一个更简单的方法来提取字符串是给`split()`方法传入一个正则表达式在结果返回之前就进行修剪：
``` javascript
var fruits = listStr.split(/\s*,\s*/);
```
现在，符合返回条件的值就是不含有空格的字符串了。

> `forEach()`方法会在2.5节中做更多讨论。这节中的代码通过遍历的方式修改了数组。还有另一种方式是使用`Array`中更新的`map()`，这会在2.7节中进行讨论。

## 补充: 使用链式编程来简化代码

这一节的样例代码是正确的，但是不是觉得有点啰嗦？我们可以用JavaScript中的方法链来压缩代码，在对象和方法支持的情况下，我们可以将一个方法调用跟在另外一个方法调用的后面。在这个例子中，我们可以把`split()`方法链在`substring()`方法的后面：
``` javascript
var start = sentence.indexOf(":");
var end = sentence.indexOf(".", start+1);
var fruits = sentence.substring(start+1, end).split(",");
```
代码并没有变得更精确，但是更少而且更容易读懂了。我们会在4.9节中更详细得讨论方法链。

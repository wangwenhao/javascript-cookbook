# 1.1. JavaScript 对象，基本类型以及字面量之间的区别

## 问题 

大家经常挂在嘴边的对象，基本类型和字面量，它们三个之间有区别，你能分清哪个是哪个吗？

## 解决

JavaScript字面量表示一个特定类型的值，比如引号中的字符串`(String)`，浮点数`(Number)`或者布尔类型`(Boolean)`：

``` javascript
"this is a string"
1.45
true
```
JavaScript基本类型是一个特定数据类型的一个实例，在这个语言中，有5种基本类型：`String`，`Number`，`Boolean`，`null`和`undefined`。下面是一些例子：
``` javascript
"this is a string"
null
```
在基本类型中，有三种类型拥有构造器对象：`String`，`Number`和`Boolean`。这些对象让我们在可以简单赋值和后续访问的基础上，可以访问内建属性和方法：
``` javascript
var str1 = "this is a string";
console.log(str1.length); // 使用String对象的length属性。
```
## 讨论 

当我们声明一个变量的时候，可能看上去好像我们只是在操作简单的字符串或数字：
``` javascript
var str1 = "this is a simple string";
```
然而，实际上我们走进了一个更广泛的功能集的大门。不依赖JavaScript对象，我们可以将一个字符串，一个数字或者一个布尔值赋给一个变量，然后在你想要的时候访问它。但是，如果我们想要对这个变量进行更多的操作，这时候就需要靠数据类型的JavaScript对象和它的属性了。

举个例子，假如你想知道一个字符串的长度，你可以访问`String`对象的`length`属性：
``` javascript
var str1 = "this is a simple string";
console.log(str1.length); // 在浏览器的控制台中输出23
```
在这个场景之后，当代码在一个字面量上访问一个`String`对象的属性的时候，一个新的`String`对象就被创建了，它的值被设置为这个变量中的字符串的值。`length`属性被访问到然后进行输出，最后，这个新创建的对象就会被丢弃。

> JavaScript 引擎没有必要在需要访问对象属性的时候真的创建一个对象来包装这个基本类型数据，它要做的只是模拟这个类型的行为。

在JavaScript中总共就5中基本类型数据：`String`，`Number`，`Boolean`，`null`和`undefined`。只有字符串，数字和布尔类型的数据有相应的构造器对象。而字符串，浮点数字，整数和布尔值的真正的值是字面量：

``` javascript
var str1 = "this is a simple string"; // 引号中是字符串是字面量
var num1 = 1.45; // 1.45的值是字面量
var answer = true; // true和false的值是布尔类型的字面量
```
我们可以用字面量表达或使用对象但是不带`new`操作符的方法来创建基本类型的布尔值，字符串和数字变量：

``` javascript
var str1 = String("this is a simple string"); // primitive string
var num1 = Number(1.45); // primitive number
var bool1 = Boolean(true); // primitive boolean
```
或者用`new`操作符来创建一个对象的实例：
``` javascript
var str2 = new String("this is a simple string"); // String object instance
var num2 = new Number(1.45); // Number object instance
var bool2 = new Boolean(true); // primitive boolean
```
可以用严格等于来比较一个对象实例和一个字面量而快速区分出基本类型和对象实例。例如，在浏览器中运行下面的代码：
``` javascript
var str1 = String("string"); 
var num1 = Number(1.45); 
var bool1 = Boolean(true);

if (str1 === "string") { 
  console.log('equal');
}
if (num1 === 1.45) { 
  console.log('equal');
}
if (bool1 === true) { 
  console.log('equal');
}

var str2 = new String("string"); 
var num2 = new Number(1.45); 
var bool2 = new Boolean(true);

if (str2 === "string") { 
  console.log('equal');
} else {
  console.log('not equal');
}

if (num2 === 1.45) {
  console.log('equal');
} else { 
  console.log('not equal');
}

if (bool2 === true) {
  console.log('equal');
} else {
  console.log('not equal');
}
```
控制台的输出如下：
```
 equal
 equal
 equal
 not equal
 not equal
 not equal
```
基本类型变量是严格等于字面量的，但是对象实例就不是。为什么基本类型变量严格等于字面量？因为基本类型比较的是它的值，而它们的值就是字面量。

大多数的情况下，JavaScript的开发者不会直接创建这三种类型的对象实例。他们只是想要一个数字，布尔类型或者字符串变量，而不是一个对象；我们不需要加强版的对象。更重要的是，当开发者在代码中使用严格等于或类型检查的时候，他们希望的是这个变量的数据类型符合自己的预期，而不是悄悄的变成了一个“对象“：
``` javascript
var num1 = 1.45;
var num2 = new Number(1.45);
console.log(typeof num1); // prints out number 
console.log(typeof num2); // prints out object
```
为此，像JSHint之类的代码检查器，会在你实例化一个基本类型对象的时候输出警告。
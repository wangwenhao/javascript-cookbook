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
> Many of the examples in this book use the console.log() function to display JavaScript results. “The Console Is Your Friend” on page 589 provides a quick how-to on accessing the JavaScript console in modern browers, and Appendix A also provides directions for set‐ ting up your environment and running the code snippets found in the solutions.

##  Discussion 

It may seem as if we’re working with simple strings or numbers when we declare a variable:

var str1 = "this is a simple string";

However, we’re actually creating doorways into an extensive set of functionality. Without reliance on JavaScript objects, we can assign a string, number, or boolean value to a variable and then access it at a later time. However, if we want to do more with the variable, we’ll need to use the data type’s complementary JavaScript object and its properties.

As an example, if we want to see the length of a string, we’ll access the String object’s length property:

var str1 = "this is a simple string"; console.log(str1.length); // prints out 23 to browser console

Behind the scenes, when the code accesses a String object’s property on the literal, a new String object is created and its value is set to the value of the string contained in the variable. The length property is accessed and printed out, and the newly created String object is discarded.

> JavaScript engines don’t have to actually create an object to wrap the primitive when you access object properties; they only have to emu‐ late this type behavior.

There are exactly five primitive data types in JavaScript: string, number, boolean, null, and undefined. Only the string, number, and boolean data types have complementary constructor objects. The actual representation of strings, floating-point numbers, inte‐ gers, and booleans are literals:

var str1 = "this is a simple string"; // the quoted string is the literal

var num1 = 1.45; // the value of 1.45 is the literal

var answer = true; // the values of true and false are boolean literals We can create primitive boolean, string, and number variables either by using a literal

representation or using the object without using the new operator: var str1 = String("this is a simple string"); // primitive string

var num1 = Number(1.45); // primitive number

var bool1 = Boolean(true); // primitive boolean To deliberately instantiate an object, use the new operator:

var str2 = new String("this is a simple string"); // String object instance

var num2 = new Number(1.45); // Number object instance

var bool2 = new Boolean(true); // primitive boolean

You can quickly tell the difference between a primitive and an object instance when you compare an object instance to a literal value using strict equality. For example, running the following code in a browser:

var str1 = String("string"); var num1 = Number(1.45); var bool1 = Boolean(true);

if (str1 === "string") { console.log('equal');

}
if (num1 === 1.45) { console.log('equal');

}

if (bool1 === true) { console.log('equal');

}

var str2 = new String("string"); var num2 = new Number(1.45); var bool2 = new Boolean(true);

if (str2 === "string") { console.log('equal');

}else{ console.log('not equal');

}

if (num2 === 1.45) { console.log('equal');

}else{ console.log('not equal');

}

if (bool2 === true) { console.log('equal');

}else{ console.log('not equal');

}

Results in the following print outs to the console:

 equal equal equal not equal not equal not equal

The primitive variables (those not created with new) are strictly equal to the literals, while the object instances are not. Why are the primitive variables strictly equal to the literals? Because primitives are compared by value, and values are literals.

For the most part, JavaScript developers don’t directly create object instances for the three primitive data types. Developers just want a number, boolean, or string variable to act like a number, boolean, or string, rather than an object; we don’t need the enhanced functionality of the object. More importantly, when developers use strict equality or type checking in the code, they want a variable to match their expectations of data type, rather than be defined as “object”:
var num1 = 1.45;

var num2 = new Number(1.45);

console.log(typeof num1); // prints out number console.log(typeof num2); // prints out object

Code validators, such as JSHint, output a warning if you instantiate a primitive data type object directly for just this reason.

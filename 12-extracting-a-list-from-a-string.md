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
Solution

The solution requires two actions: extract out the string containing the list of items, and

then convert this string into a list.

Use String’s indexOf() to locate the colon, and then use it again to find the first period

following the colon. With these two locations, extract the string using String’s sub

string():

var sentence = 'This is one sentence. This is a sentence with a list of items:' +

'cherries, oranges, apples, bananas. That was the list of items.';

var start = sentence.indexOf(':');

var end = sentence.indexOf('.', start+1);

var listStr = sentence.substring(start+1, end);

Once you have the string consisting of the list items, use the String split() to break

the string into an array:
var fruits = listStr.split(',');
console.log(fruits); // ['cherries', ' oranges', ' apples', ' bananas']
Discussion
The indexOf() method takes a search value, as first parameter, and an optional beginning
index position, as second.
The list is delimited by a beginning colon character and an ending period. The index
Of() method is used without the second parameter in the first search, to find the colon.
The method is used again but the colon’s position (plus 1) is used to modify the beginning
location of the search for the period:
var end = sentence.indexOf('.',start+1);
If we didn’t modify the search for the ending period, we’d end up with the location of
the first sentence’s period rather than the period for the sentence containing the list.
Once we have the beginning and ending location for the list, we’ll use the sub
string() method, passing in the two index values representing the beginning and ending
positions of the string:
var listStr = sentence.substring(start+1, end);
The extracted string is:
cherries, oranges, apples, bananas
We’ll finish by using split() to split the list into its individual values:
var fruits = listStr.split(',') ; // ['cherries', ' oranges',
' apples', ' bananas']
There is another string extraction method, substr(), that begins extraction at an index
position marking the start of the substring and passing in the length of the substring as
the second parameter. We can easily find the length just by subtracting the beginning
position of the string from the end position:
var listStr = sentence.substr(start+1, end-start);
var fruits = listStr.split(',');
See Also
Another way to extract the string is to use regular expressions and the RegExp object,
covered beginning in Recipe 1.5.

Advanced

The result of splitting the extracted string is an array of list items. However, the items

come with artifacts (leading spaces) from sentence white space. In most applications,

we’ll want to clean up the resulting array elements.

We’ll discuss the Array object in more detail in Chapter 2, but for now, we’ll use the

Array forEach() method in addition to the String object’s trim() method to clean up

the array:

fruits = listStr.split(',');

console.log(fruits); // [' cherries', ' oranges', ' apples', ' bananas']

fruits.forEach(function(elmnt,indx,arry) {

arry[indx] = elmnt.trim();

});

console.log(fruits); // ['cherries', 'oranges', 'apples", "bananas"]

The forEach() method applies the function passed as parameter (the callback) to each

array element. The callback function supports three arguments: the array element value,

and optionally, the array element index and the array itself.

Another simpler approach is to pass a regular expression to the split() that trims the

result before it’s returned:

var fruits = listStr.split(/\s*,\s*/);

Now the matching returned value is just the string without the surrounding white space.

The forEach() method is also covered in Recipe 2.5. The code in this

section mutates the array in place, which means it actually modifies

the array as it’s traversed. Another nondestructive approach is to use

the newer map() Array method, covered in Recipe 2.7.


# JavaScript 类型

JavaScript是**动态类型**的语言，所以在执行的时候变量的类型是可变的。所以有类型与运行时类型。

## 类型

类型是指变量或表达式在代码中定义时候的类型。
常见的类型有

- undefine
- null
- string
- number
- boolean
- object
- sybool
- bigint


## 运行时类型（Runtime Type）
运行时类型是指，在程序执行的时候，变量实际的类型。
例如
```javascript
let x = 42;  // 'x' 的类型是 number -- 类型
x = "hello"; // 现在 'x' 的类型变成了 string -- 运行时类型
```

## string -> number

字符串到数字的类型转换，支持十进制、二进制、八进制以及十六进制。
比如
- 222
- 0b11011110
- 0o336
- 0xDE

parseInt从左到右解析字符串，遇到非数字就停止解析。 第一位参数是需要转换的字符串， 第二位参数是转换的进制。
常见的parseInt 面试题

```js
// 下面代码的输出是什么？
console.log(parseInt("100", 2)); // 4
console.log(parseInt("100", 8)); // 64
console.log(parseInt("100", 10)); // 100
console.log(parseInt("100", 16)); // 256

// parseInt 从左到右解析字符串， 遇到非数字就停止。
console.log(parseInt("3.14")); // 3
console.log(parseInt("0.5")); // 0
console.log(parseInt(".5")); // NaN

// 忽略前导空格, 空串无数字就是NaN
console.log(parseInt("123abc")); // 123
console.log(parseInt("abc123")); // NaN
console.log(parseInt("  42")); // 42
console.log(parseInt("  ")); // NaN
console.log(parseInt("")); // NaN

console.log(parseInt("012")); // 12
console.log(parseInt("0x12")); // 18 
console.log(parseInt("0b11")); // 0 parseInt不会识别0b 

console.log(Number("10")); // 10
console.log(Number("10px")); // NaN
console.log(parseInt("10px")); // 10
console.log(parseFloat("10.5px")); // 10.5
console.log(Number("0b101")); // 5
console.log(Number("0xF")); // 15


/**
`map(parseInt)` 相当于 `parseInt(value, index)`，其中 `index` 作为 `radix`（进制）。
传入0 等于10进制。故parseInt("10", 0) 输出 10;
传入 1 ，进制不存在， 输出NaN
传入 2， 2进制不存在3， 输出NaN
**/
console.log(["10", "20", "30"].map(parseInt)); // 10 NaN NaN
console.log(["10", "20", "30"].map(x => parseInt(x, 10))); // 10 20 30
```

## typeof

```js
console.log(typeof null); // Object
console.log(typeof []); // Object
console.log(typeof function(){}); // function
console.log(typeof NaN); // number
console.log(typeof new Date()); // object
console.log(typeof /regex/); // object

```

## instanceof

```js
console.log([] instanceof Array); // true
console.log([] instanceof Object); // true
console.log(function(){} instanceof Function); // true
console.log(new Date() instanceof Date); // true
console.log(new Date() instanceof Object); // true
console.log(null instanceof Object); // false

```

## == 隐式转换

```js
console.log([] == false); // [] -> "" -> 0 -> false
console.log([] == 0); // [] -> "" => 0
console.log([1] == true); // [] -> "1" -> true
console.log([1,2] == "1,2"); // [1,2] => "1,2"

true
true
true
true

```
## +运算

```js
console.log(1 + "1"); // -> "1" + "1"  -> "11"
console.log("1" + 1); // "11"
console.log(1 + 1 + "1"); // 从左至右，先执行1+1=2；2+"1" -> "21"
console.log("1" + 1 + 1); // 从左至右 , "1"+ 1 -> "11"; "11"+ 1-> "111"
console.log([] + {}); // [] -> "", {} -> [object object] -> "[object object]"
console.log({} + []); // 0由于这里{}在前面，被js解析成一个代码块，但是此代码块没有返回值所以表达式实际上等于 + [], 而对[]执行toString的时候[]=""，+"" =0.

"11"
"11"
"21"
"[object object]"
0
```


## 关于类型的常见问题

- 字符串是否有最大长度？<br/>
> string类型有最大长度是2^53-1

- 为什么0.1 + 0.2 !== 0.3?

> 点数运算的精度问题导致等式左右的结果并不是严格相等，而是相差了个微小的值。正确的比较是使用js提供的最小精度值。```javascript Math.abs(0.1 + 0.2 - 0.3) <= Number.EPSILON ```

- 为什么有的编程规范要求用 void 0 代替 undefined?

> 在es5之前，undefined是一个变量而不是一个关键字，而void 0 的值 永远等于undefined。所以为了避免无意中被篡改，建议用void 0 来代替undefined值。但在es5以后， undefined已经变成一个不可写的全局属性，无法重新赋值。

- 如何判断 `null`、`array`、`date` 的类型？

> Object.prototype.toString.call(value)

```js
console.log(Object.prototype.toString.call(null));       // "[object Null]"
console.log(Object.prototype.toString.call([]));         // "[object Array]"
console.log(Object.prototype.toString.call(new Date())); // "[object Date]"
console.log(Object.prototype.toString.call(/regex/));    // "[object RegExp]"

```

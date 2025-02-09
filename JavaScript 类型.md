# JavaScript 类型

JavaScript是**动态类型**的语言，所以在执行的时候变量的类型是可变的。所以有类型与运行时类型。

## 类型

类型是指变量或表达式在代码中定义时候的类型。
常见的类型有

- undefined
- null
- string
- number
- boolean
- object
- symbool
- bigint


## 运行时类型（Runtime Type）
运行时类型是指，在程序执行的时候，变量实际的类型。
例如
```javascript
let x = 42;  // 'x' 的类型是 number -- 类型
x = "hello"; // 现在 'x' 的类型变成了 string -- 运行时类型
```


## 关于类型的常见问题

问题 | 解答
------------ | -------------
字符串是否有最大长度 | string类型有最大长度是2^53-1
为什么0.1 + 0.2 !== 0.3 | 浮点数运算的精度问题导致等式左右的结果并不是严格相等，而是相差了个微小的值。正确的比较是使用js提供的最小精度值。`` Math.abs(0.1 + 0.2 - 0.3) <= Number.EPSILON ``
symbol是什么 | symbol是es6新增的一种数据类型 - Symbol 适用于定义 私有属性
typeof 与 instanceof 的区别 | typeof用来判断基本类型，不能判断null 对象与数组，因为都会返回Objec。 instanceof用来判断对象的类型，判断是否在原形链中找到该类型的原型。
如何判断变量是否为数组 | `Array.isArray(arr) // true`<br>`arr.__proto__ === Array.prototype // true`<br>`arr instanceof Array; // true`<br>`Object.prototype.toString.call(arr); // "[object Array]"`
typeof null === "object" 的原因 | null在js中被视为是一个**特殊的“空”对象**。


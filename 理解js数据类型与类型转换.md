> 本文参考地址 [点我直达](http://www.jianshu.com/p/b161aeecb6d6)

- Primitive 原始类型
  
  - number
  
    * NaN,Infinity也是

  - string

  - boolean

  - null

  - undefined

  - Symbol(ES6新定义，还没用过)
  
- Object 类型

  > 参考[MDN标准库](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects)，注意，上面这个MDN链接中给出的“值属性”那一栏中的值并不是对象。
  
next

- 理解原始类型的自动装箱

  number，boolean，string既然为原始类型，那么我们为何可以调用类似toLowerCase等这种定义在对象类型的上的方法呢，那么原因就是js运用了自动装箱，也就是将原始类型包装到Boolean，Number，String对象上
  
- 理解类型转换的valueOf 和 toString()

  以下是部分内置对象调用valueOf()的行为
  
  对象|  返回值
  ------|----
  Array|  数组本身（对象类型）。
  Boolean|  布尔值（原始类型）。
  Date|   从 UTC 1970 年 1 月 1 日午夜开始计算，到所封装的日期所经过的毫秒数（原始类型）。
  Function|   函数本身（对象类型）。
  Number|   数字值（原始类型）。
  Object|   对象本身（对象类型）。如果自定义对象没有重写valueOf方法，就会使用它。
  String|   字符串值（原始类型）。
  
  由上表可见，valueOf()虽然期望返回原始类型的值，但是实际上有一些对象在逻辑上无法找到与之对应的原始值，因此只能返回对象本身。

  toString()则不一样，因为不管什么对象，我们总有办法“描述”它，因此js内置对象的toString()总能返回一个原始string类型的值。

  ```javascript
  var d = new Date();
  d.toString()
  // "Fri Apr 21 2017 14:54:04 GMT+0800 (中国标准时间)"
  ```
  
  我们自己在重写toString()的时候也应该返回合理的string。
  
- js内部用于实现类型转换的4个函数
  
  这4个方法实际上是ECMAScript定义的4个抽象的操作，它们在js内部使用，进行类型转换。我们js的使用者不能直接调用这些函数，但是了解这些函数有利于我们理解js类型转换的原理。

  - ToPrimitive ( input [ , PreferredType ] )
  
  - ToBoolean ( argument )
  
  - ToNumber ( argument )
  
  - ToString ( argument )
  
  > 请区分这里的ToString ()和上文谈到的toString()，一个是js引擎内部使用的函数，另一个是定义在对象上的函数。
  
- 隐式类型转换
  
  '<'、'>'的情况与'+'类似，但是处理方式与'+'有些不同。如果好奇请自行[查阅文档](https://tc39.github.io/ecma262/#sec-abstract-relational-comparison)
  
- 显式类型转换

  > 在不确定隐式转换的情况下最好利用显式转换

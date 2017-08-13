front-end interview 汇总（前端面试汇总2017）

- JavaScript 的 typeof 返回哪些数据类型？

  分析：

  > 这道题检验的是 JS 基本功，只要对 typeof 运算符是了解的，就没有太大难度。具体在回答的时候，再结合理论知识和编码过程中实际情况进行回答即可。另外，考虑到面试时的严谨性.

  建议回复：

  > 首先，JavaScript 中一共有两大数据类型：

  > 基础类型
  引用类型
  基础类型包括：Number、String、Boolean、Null、Undefined、Symbol（该类型位 ES2015 中新增类型）
  引用类型包括：Object typeof 运算符把类型信息以字符串形式返回，需要注意的是 typeof 返回的类型和 JavaScript 定义的类型有细微的差异。 typeof 返回七种可能的值：“number”、“string”、“boolean”、“object”、"symbol"、“function”和“undefined”。

- 请写出以下运算结果：

  ```javascript
  alert(typeof null);
  alert(typeof undefined);
  alert(typeof NaN);
  alert(NaN == undefined);
  alert(NaN == NaN);
  var str = "123abc";
  alert(typeof str++);
  alert(str);
  ```
  分析：

  > 这道题与“题目一”是连环扣，当“题目一”回答完后，通过此题再一次强化运算符和数据类型的基本功。

  建议回复：

  > 本题主要是考察 typeof 判断值的类型，它们输出的结果依次是：
  ```javascript
  alert(typeof null);  // object
  alert(typeof undefined);  // undefined
  alert(typeof NaN);  // number
  alert(NaN == undefined);  // false
  alert(NaN == NaN);  // false
  var str = "123abc";
  alert(typeof str++);  // number
  alert(str);  // NaN
  ```

- 例举至少 3 种强制类型转换和 2 种隐式类型转换?

  分析：

  > 类型转换听起来可能有点宽泛，但这道题明确给出了回答的范围

  建议回复：

  > 1. 强制类型转换： 明确调用内置函数，强制把一种类型的值转换为另一种类型。强制类型转换主要有：Boolean、Number、String、parseInt、parseFloat
  > 2. 隐式类型转换： 在使用算术运算符时，运算符两边的数据类型可以是任意的，比如，一个字符串可以和数字相加。之所以不同的数据类型之间可以做运算，是因为 JavaScript 引擎在运算之前会悄悄的把他们进行了隐式类型转换。隐式类型转换主要有：+、–、==、!

- AJAX 的局限性?

  > AJAX 不支持浏览器 back 按钮。
  安全问题 AJAX 暴露了与服务器交互的细节。
  对搜索引擎的支持比较弱。不会执行你的 JS 脚本，只会操作你的网页源代码；
  跨域请求有一定限制。解决方式：jsonp；

- new 操作符具体干了什么呢?

  1. AJAX 不支持浏览器 back 按钮。
  1. 安全问题 AJAX 暴露了与服务器交互的细节。
  1. 对搜索引擎的支持比较弱。不会执行你的 JS 脚本，只会操作你的网页源代码；
  1. 跨域请求有一定限制。解决方式：jsonp；

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

  1. 创建一个新对象；
  1. 把函数中上下文（作用域）对象this指向该对象；
  1. 执行代码，通过this给新对象添加属性或方法；
  1. 返回对象；

- null 和 undefined 的区别？

  - null： null表示空值，转为数值时为0；

  - undefined：undefined表示"缺少值"，就是此处应该有一个值，但是还没有定义。

    1. 变量被声明了，但没有赋值时，就等于undefined。
    1. 对象没有赋值的属性，该属性的值为undefined。
    1. 函数没有返回值时，默认返回undefined。

- this的原理
  
  [引用地址](http://blog.anchengjian.com/#/posts/2016/js中this的一些总结.md) 

- 数据类型
  
  undefined 派生自 null 所以ECMAScript262 规定 undefined == null

- 理解this
  
  [彻底理解this](http://blog.anchengjian.com/#/posts/2016/js中this的一些总结.md)

  > 一些重点
  ECMAScript 5 引入了 Function.prototype.bind。调用 fn.bind(someObject) 方法会创建并返回一个与 fn 具有相同函数体和作用域的函数，但是在这个新函数中，this 将永久地被绑定到了 bind 的第一个参数，无论这个函数是如何被调用的。

- 闭包

- new 操作符具体干了什么呢？

  new共经历了四个过程。

  ```javascript
  var fn = function () { };
  var fnObj = new fn();
  ```

  1. 创建了一个空对象
  ```javascript
  var obj = new object();
  ```
  2. 设置原型链
  ```javascript
  obj._proto_ = fn.prototype;
  ```
  3. 让fn的this指向obj，并执行fn的函数体
  ```javascript
  var result = fn.call(obj);
  ```
  4. 判断fn的返回值类型，如果是值类型，返回obj。如果是引用类型，就返回这个引用类型的对象。
  ```javascript
  if (typeof(result) == "object"){  
      fnObj = result;  
  } else {  
      fnObj = obj;
  }  
  ```

- 编写一个方法 求一个字符串的字节长度

  ```javacsript
    //ES6有一些新的增加方法，对于4字节有支持String.fromCodePoint s.codePointAt()
    function getBytes(str){
    const byte2 = 255,
      byte4 = 65535;
    let size = 0;
    for(let i =0; i<str.length; i++){
      
      if(str[i] > byte2){
        size += 2;
      }
      else{
        size += 1;
      }
    }
    return size;
  }

  console.log('结果：',getBytes('爱𠮷你一万年1234') );
  ```

- 深度拷贝、浅拷贝、extend

  [github上的一种实现](https://github.com/wengjq/Blog/issues/3link)

  ```javascript
  // 自己实现了一把
  let my = (()=>{
    const types = 'Undefined Boolean Number String Function Object Null Date RegExp Array Symbol'.split(' ');
    const my = {};
    function getType(){
      return Object.prototype.toString.call(this).slice(8,-1);
    }
    types.forEach((type,i) => {
      my[`is${type}`] = ((self) => {
        return (elem) => {
          return getType.call(elem) === self;
        };
      })(type);
    });
    return my;
  })();

  function copy(obj,deep){
    let target ,value;
    if(obj === null || (typeof obj != 'object' && !my.isFunction(obj))){
      return obj;
    }
    else if(my.isFunction(obj)){
      return new Function(`return ${obj.toString()}`)();
    }
    else if(my.isDate(obj)){
      return new Date(obj);
    }
    else if(my.isRegExp(obj)){
      return new RegExp(obj);
    }
    else if(my.isObject(obj) || my.isArray(obj)){
      target = my.isArray(obj) ? [] : {};
      for(let key in obj){
        value = obj[key];
        if(value === obj){
          continue;
        }
        if(deep && (my.isArray(value) || my.isObject(value))){
          target[key] = copy(value,deep);
        }
        else{
          target[key] = value;
        }
        
      }
      return target;
    }
  }

  function extend(...args){
    let deep, 
      target = args[0] || {},
      src,
      key,
      option,
      value,//对象value值
      index = 1;
    const len = args.length;
    if(typeof args[0] === 'boolean'){
      deep = true;
      target = args[1] || {};
      index += 1;
    }
    for(;index<len;index++){
      // 开始循环扩展每个形参
      option = args[index];
      
      src = copy(option,deep);
      for(key in src){
        target[key] = src[key];
      }
    }
    return target;
  }
  ```

- 请给出异步加载js方案

  异步加载方式：
  defer，
  async：
  创建script，插入到DOM中，加载完毕后callBack，见代码：
  ```javascript
  function loadScript(url, callback){
    var script = document.createElement("script")
    script.type = "text/javascript";
    if(script.readyState){ //IE
      script.onreadystatechange = function(){
        if (script.readyState == "loaded" ||script.readyState == "complete"){
          script.onreadystatechange = null;
          callback();
        }
      };
    } 
    else {
    // Others: Firefox, Safari, Chrome, and Opera
      script.onload = function(){
        callback();
      };
    }
    script.src = url;
    document.body.appendChild(script);
  }
  ```

- 一些代码实现

```javascript

// 转换url search为对象形式
function parseQueryString(search){
  let query = decodeURIComponent(search).split('?')[1],
    output = {},
    key,
    value;
  if(!query){
    return {};
  }
  query.split('&').forEach((item) => {
    [key,value] = item.split('=');
    if(typeof value === 'undefined'){
      // 等号右边没有数值，那么默认就是true值
      value = true;
    }
    output[key] = value;
  });
  return output;
}

// 实现array forEach
function forEach(fn){
  for(let i=0; i<this.length; i++){
    fn(this[i],i,this);
  }
}

// 判断是不是质数
function isPrime(num){
  let index = num - 1;
  for(;index>1;index--){
    if(num%index === 0){
      return false;
    }
  }
  return true;
}

// 删除数组重复元素，利用hash，空间增大，减少时间复杂度
function delDul(arr){
  let tmp = {};
  return arr.filter((item) => {
    if(item in tmp){
      return false;
    }
    tmp[item] = item;
    return true;
  });
}

// 插入排序的实现
function sort(arr){
  let i,j;
  for(i=1; i<arr.length; i++){
    for(j=0; j<i; j++){
      if(arr[i] < arr[j]){
        arr.splice(j,0,arr[i]);
        arr.splice(i+1,1);
        break;
      }
    }
  }
  return arr;
}

// 快速排序的递归实现
function quick(){
  let pivot = this[0];
  let left = [],
    right = [];
  if(this.length <= 1){
    return this;
  }
  this.forEach((item,index) => {
    if(index == 0){
      return;
    }
    if(item > pivot){
      right.push(item);
    }
    else{
      left.push(item)
    }
  });

  return quick.call(left).concat(pivot,quick.call(right));
}

// 获取字符串中字符出现的总次数，
function getDul(){
  let chars = {};
  Array.prototype.slice.call(this).forEach((item) => {
    if(item in chars){
      chars[item] += 1;
    }
    else{
      chars[item] = 1;
    }
  });
  let charsA = [];
  for(let key in chars){
    charsA.push({key:key,times:chars[key]});
    console.log(`${key}出现了${chars[key]}次`);
  }
  return charsA;
}

// bind的普通实现
function bind(obj,fn){
  return function(){
    return fn.apply(obj,arguments);
  }
}

// curry化的通用实现
function curry(...args){
  let outerArgs = args.slice(1);
  return (...innerArgs) => {
    let finalArgs = outerArgs.concat(innerArgs);
    return args[0].apply(null,finalArgs);
  }
}

// 函数curry化，实现add(1)(2)(3)(4)(5)(6) 无限加
function add(num){
  let helper = function(next){
    num = typeof next === 'undefined' ? num : num + next;
    return helper;
  };
  helper.valueOf = () => {
    return num;
  };
  return helper;
}

// add = (a,b) => {return a+b;};
// curry(add,3)  变成了函数 x  外层包含了3 需要调用x(5)这样就是调用了add(3,5)
// 如果在curry(x,5) 变成了函数y 外层包含了5 需要调用y()相当于调用了x(5)相当于调用了add(3,5)


// curry化bind方法
function curryBind(...args){
  let [context,fn] = [args[0],args[1]];
  let outerArgs = args.slice(2);
  return (...innerArgs) => {
    let finalArgs = outerArgs.concat(innerArgs);
    return fn.apply(context,finalArgs);
  }
}


// 没有记忆函数的实现,阶乘的实现
let factorial = (() => {
  let index = 0;
  let fac = (num) => {
    index++;
    let number = parseInt(num);
    if(typeof number != 'number'){
      return 0;
    }
    
    if(number == 0){
      console.log(`我被调用了${index}次`);
      index = 0;
      return 1;
    }

    return number * factorial(number-1);
  }
  return fac;
})();

// 带有记忆函数的实现
let factorialM = (() => {
  let index = 0,
    memo = [1],
    result;
  let fac = (num) => {
    index++;
    let number = parseInt(num);
    if(typeof number != 'number'){
      return 0;
    }
    if(typeof memo[num] === 'number'){
      console.log(`我被调用了${index}次`);
      index = 0;
      return memo[num];
    }
    result = number * factorialM(number-1);
    memo[number] = result;
    return result;
  }
  return fac;
})();


// 自己实现一个reduce函数
let reduce = (()=>{
  let index = 0,
    prev;
  let redu = (fn,arr) => {
    if(arr.length === 0){
      index = 0;
      return ;
    }
    if(arr.length === 1){
      index = 0;
      return arr[0];
    }
    
    prev = fn(arr[0],arr[1],index++,arr);
    arr.splice(0,2,prev);
    return reduce(fn,arr); 
  };
  return redu;
})();

function add(a,b,index,arr){
  console.log(`prev：${a},next:${b},index:${index},arr:${arr}`);
  return a+b;
}

reduce(add,[1,2,3,4]) ; // 返回10


// 自己实现一个reduce函数，改进版
let reduce = (()=>{
  let index = 0,
    prev;
  let redu = function(...args){
    if(args.length >=2){
      prev = args[1];//有初始值的情况
      if(this.length == 0){
        return prev;
      }
    }
    else{
      if(this.length == 0){
        return '出错了，啥都没有';
      }
      if(this.length == 1){
        return this[0];
      }

      prev = this[index];
      index += 1;
    }
    
    while(index < this.length){
      if(index in this){
        prev = args[0].call(this,prev,this[index],index,this);
      }
      index += 1;
    }
    index = 0;//恢复
    return prev;
  };
  return redu;
})();

function add(a,b,index,arr){
  console.log(`prev：${a},next:${b},index:${index},arr:${arr}`);
  return a+b;
}

reduce.call([1,2,3,4],add) ; // 返回10


// 自己实现一个reduce函数 箭头函数this不能改变，所以自己改了一下
let reduce = ((that)=>{
  let index = 0,
    prev;
  let redu = (...args) => {
    if(args.length >=2){
      prev = args[1];//有初始值的情况
      
      if(that.length == 0){
        return prev;
      }
    }
    else{
      
      if(that.length == 0){
        return '出错了，啥都没有';
      }
      if(that.length == 1){
        return that[0];
      }

      prev = that[index];
      index += 1;
    }
    
    while(index < that.length){
      if(index in that){
        prev = args[0].call(that,prev,that[index],index,that);
      }
      index += 1;
    }
    index = 0;//恢复
    return prev;
  };
  return redu;
});

function add(a,b,index,arr){
  console.log(`prev：${a},next:${b},index:${index},arr:${arr}`);
  return a+b;
}

reduce([1,2,3,4])(add) ; // 返回10


```

- 箭头函数里的this

  “箭头函数”的this，总是指向定义时所在的对象，而不是运行时所在的对象。

  [阮一峰的这个箭头函数的this讲得好](https://github.com/ruanyf/es6tutorial/issues/150)

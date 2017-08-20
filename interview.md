# front-end interview 汇总（前端面试汇总2017）

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

// 支持new的 currybind
Function.prototype.bind = Function.prototype.bind || function(ctx,...args){
  if(typeof this !== 'function'){
    return 'bind对象应该为函数';
  }
  let fBind = this,
    FNOP = function(){},// 用于判别是否是new操作的instanceof作用
    bound = function(...innerArgs){
     return fBind.apply(this instanceof FNOP ? this : (ctx || {}), args.concat(innerArgs));     
    };
    FNOP.prototype = fBind.prototype;
    bound.prototype = new FNOP(); // 原型式继承
    return bound;
};


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

  ```javascript

  // 彻底理解this
  function underThis(){
    console.log('outer',this);
    var that = this;
    return function hi(){
      console.log('hi',that)
      return this;
    }
  }
  ```

- 请描述一个网页从开始请求道最终显示的完整过程？
  
  1. 浏览器中输入网址；
  1. 发送至DNS服务器并获得域名对应的WEB服务器IP地址；
  1. 与WEB服务器建立TCP连接；
  1. 浏览器向WEB服务器的IP地址发送相应的HTTP请求；
  1. WEB服务器响应请求并返回指定URL的数据，或错误信息，如果设定重定向，则重定向到新的URL地址；
  1. 浏览器下载数据后解析HTML源文件，解析的过程中实现对页面的排版，解析完成后在浏览器中显示基础页面；
  1. 分析页面中的超链接并显示在当前页面，重复以上过程直至无超链接需要发送，完成全部数据显示。

- 行内元素 空元素 块级元素

  input span img a label 

  br hr 

  div ol ul li dl dt dd h1 form 

- html5 新增 删除

  新增 article等等
  localStorage webworker
  表单 date calendar等

- iframe 有哪些缺点？

  1. iframe会阻塞主页面的Onload事件；
  1. 搜索引擎的检索程序无法解读这种页面，不利于SEO；
  1. iframe和主页面共享连接池，而浏览器对相同域的连接有限制，所以会影响页面的并行加载。
  1. 使用iframe之前需要考虑这两个缺点。如果需要使用iframe，最好通过JavaScript动态给iframe添加src属性值，这样可以绕开以上两个问题。

- 元素竖向的百分比设定是相对于容器的高度吗？

  [12个你未必知道的CSS小知识](https://segmentfault.com/a/1190000002528855link)

- # 全屏滚动的原理是什么？用到了CSS的那些属性？ 【演习项目】

  [H5全屏滑动](https://segmentfault.com/a/1190000003691168)

- 如果需要手动写动画，你认为最小时间间隔是多久，为什么？（阿里）

  多数显示器默认频率是60Hz，即1秒刷新60次，所以理论上最小间隔为1/60＊1000ms ＝ 16.7ms

- display:inline-block 什么时候会显示间隙？(携程)

  移除空格、使用margin负值、使用font-size:0、letter-spacing、word-spacing

- 什么是Cookie 隔离？（或者说：请求资源的时候不要让它带cookie怎么做）

  如果静态文件都放在主域名下，那静态文件请求的时候都带有的cookie的数据提交给server的，非常浪费流量，
  所以不如隔离开。

  因为cookie有域的限制，因此不能跨域提交请求，故使用非主要域名的时候，请求头中就不会带有cookie数据，
  这样可以降低请求头的大小，降低请求时间，从而达到降低整体请求延时的目的。

  同时这种方式不会将cookie传入Web Server，也减少了Web Server对cookie的处理分析环节，
  提高了webserver的http请求的解析速度。

- # 什么是CSS 预处理器 / 后处理器？【演习项目】

  - 预处理器例如：LESS、Sass、Stylus，用来预编译Sass或less，增强了css代码的复用性，
    还有层级、mixin、变量、循环、函数等，具有很方便的UI组件模块化开发能力，极大的提高工作效率。

  - 后处理器例如：PostCSS，通常被视为在完成的样式表中根据CSS规范处理CSS，让其更有效；目前最常做的
    是给CSS属性添加浏览器私有前缀，实现跨浏览器兼容性的问题。

- # 如何将浮点数点左边的数每三位添加一个逗号，如12000000.11转化为『12,000,000.11』? 【研究正则写法】

  > [参考string.replace](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/replace)

  ```javascript
  function commafy(num){
    return num && num
      .toString()
      .replace(/(\d)(?=(\d{3})+\.)/g, function($1, $2){
        return $2 + ',';
      });
  }
  ```
- 在事件中，this指向触发这个事件的对象，特殊的是，IE中的attachEvent中的this总是指向全局对象Window；

- # 获取event对象的引用

  ```javascript
  // 获取event对象的引用，取到事件的所有信息，确保随时能使用event；
    getEvent : function(e) {
      var ev = e || window.event;
      if (!ev) {
        var c = this.getEvent.caller;
        while (c) {
          ev = c.arguments[0];
          if (ev && Event == ev.constructor) {
            break;
          }
          c = c.caller;
        }
      }
      return ev;
    }
  ```

- # JS模块加载器的轮子怎么造，也就是如何实现一个模块加载器？

- # 移动端最小触控区域是多大？

- # 移动端的点击事件的有延迟，时间是多久，为什么会有？ 怎么解决这个延时？（click 有 300ms 延迟,为了实现safari的双击事件的设计，浏览器要知道你是不是要双击操作。）

  [参考地址](https://thx.github.io/mobile/300ms-click-delay)

- # 前端路由

  [前端路由参考](https://segmentfault.com/a/1190000007238999)

- # 移动前端开发和 Web 前端开发的区别是什么？

  [比较](https://www.zhihu.com/question/20269059)

- 前端面试题，利用给定接口获得闭包内部对象

  [连接地址](https://segmentfault.com/q/1010000002916478)

- 前端疑难杂症

  [参考地址](https://juejin.im/entry/58bcf765a22b9d005eef5623)

- 备注

  [面试备注](https://segmentfault.com/a/1190000009200927)

- 实现一个LazyMan 

  > 实现一个LazyMan，可以按照以下方式调用:
  > 
  > LazyMan("Hank")输出:
  > 
  > Hi! This is Hank!
  >  
  > LazyMan("Hank").sleep(10).eat("dinner")输出
  > 
  > Hi! This is Hank!
  > 
  > //等待10秒..
  > 
  > Wake up after 10
  > 
  > Eat dinner~
  >  
  > LazyMan("Hank").eat("dinner").eat("supper")输出
  > 
  > Hi This is Hank!
  > 
  > Eat dinner~
  > 
  > Eat supper~
  >  
  > LazyMan("Hank").sleepFirst(5).eat("supper")输出
  > 
  > //等待5秒
  > 
  > Wake up after 5
  > 
  > Hi This is Hank!
  > 
  > Eat supper
  >  
  > 以此类推。

  ```javascript

  (function(window){
    let tasklist = [],
      param;
    function subscribe(fn,...args){
      param = {
        fn: fn,
        args: args,
      };
      if(fn === 'sleepFirst'){

        tasklist.unshift(param);
      }
      else{
        tasklist.push(param);
      }
    };
    function publish(){
      if(tasklist.length > 0){
        run(tasklist.shift());
      }
    }
    function run(task){
      let func = task.fn,
        args = task.args;
      switch(func){
        case 'eat': 
          eat.apply(null,args);
          break;
        case 'sleep': 
          sleep.apply(null,args);
          break;
        case 'sleepFirst': 
          sleepFirst.apply(null,args);
          break;
        case 'lazyMan': 
          lazyMan.apply(null,args);
          break;
      }
    }
    const LazyMan = function(){};
    LazyMan.prototype.eat = function(str){
      subscribe('eat',str);
      return this;
    }
    LazyMan.prototype.sleep = function(time){
      subscribe('sleep',time);
      return this;
    }
    LazyMan.prototype.sleepFirst = function(time){
      subscribe('sleepFirst',time);
      return this;
    }

    function log(str){
      console.log(str);
    }
    function lazyMan(name){
      log(`Hi!This is ${name}!`);
      publish();
    }
    function eat(str){
      log(`eat ${str}`);
      publish();
    }
    function sleep(time){
      setTimeout(() => {
        log("Wake up after "+ time);
        publish();
      }, time * 1000);
    }
    function sleepFirst(time){
      setTimeout(() => {
        log("Wake up after "+ time);
        publish();
      }, time * 1000); 
    }

    window.LazyMan = function(name){
      subscribe("lazyMan", name);
      setTimeout(function(){
        publish();
      }, 0);
      return new LazyMan();
    };
  })(window);

  ```

- css flex

  > [一劳永逸flex](https://juejin.im/post/58e3a5a0a0bb9f0069fc16bb)

  首先说下flex的相关的css属性吧，display:flex,首先要设置这个，将dom元素变为FFC。
  
  主轴方向利用参数 justify-content: 用的最多的可能就是center了，flex-start(默认值), flex-end，space-between,space-around 这两个并不常用

  交叉轴方向用 align-items: 同上，不过没有后两个属性，替换为baseline,strech(默认值)

  子元素 flex: 这个是flex-grow flex-shrink flex-basis 三个值的缩写
 
  最常用的就是flex:1  表示flex-grow  flex:1 1; 表示flex-grow:1; flex-shrink:1;

  flex-basis : 可以为px em auto 和content；

  flex-direction: row colomn row-reverse

  flex-wrap: wrap nowrap wrap-reverse 

  上面这俩 合起来就是flex-flow(不算很常用)

  父元素还一个不算常用的  align-content(他是按交叉轴排序的，属性同align-items,不过删除了baseline,多了space-between,space-around,他是多行排列时用的)

  align-self: 可以覆盖父元素的align-items

  最后还有一个order属性 ，属性值越小，排列越靠前

- Web 优化

  1. html层
    
    - css的link写在head里
    - script标签写在body之前
    - 利用defer或者async属性
  
      defer是按照先后顺序（现实中不一定，也不一定在DOMContentLoaded事件完成前执行），会马上下载，但是延迟执行，遇到</html>标签后才会开始加载
    
      async不会按照先后顺序,也就是不按顺序，下载完就执行。

      > [参考一个解释](https://segmentfault.com/q/1010000000640869)
    
    - 语义化，用section,article,aside,main,header,footer等语义化标签
    - meta keywords description描述
    - 页面H1的利用，搜索优化就少用ajax请求数据
    - 缓存，if-modified-since/last-modified(这个只是到秒级别)  E-tag/if-none-match，服务端可以发cache-control 和expire,etag弊端，负载均衡
      > [参考](http://tech110.blog.51cto.com/438717/549764)
   
  2. css层

    - 减少层级
    - 尽量避免通配符
    - 尽量避免使用import
    - 尽量使用缩写（颜色，属性值合并等）
    - 尽量缩写类名
    - 雪碧图

  3. js层次

    - 尽可能少的dom操作
    - 懒加载
    - localStorage，sessionStorage
    - webpack打包外部请求文件为一个文件
    - 小图片转化为base64，牺牲带宽减少请求

  4. 其他方面

    - CDN加速
    - 减少301重定向
    - gzip压缩

- http常用状态码
  
  > [301,302参考](http://www.cnblogs.com/5207/p/5908354.html)

  1. 200
  2. 301
  3. 304
  4. 403
  4. 404
  5. 500
  6. 502

- http2.0

  - url输入之后到底发生了什么 [参考](https://segmentfault.com/a/1190000006879700)

  - [参考地址](http://www.alloyteam.com/2016/07/httphttp2-0spdyhttps-reading-this-is-enough/)

  - [你应该知道的http1.1 http2.0](http://www.alloyteam.com/2016/07/httphttp2-0spdyhttps-reading-this-is-enough/#prettyPhoto) 
  

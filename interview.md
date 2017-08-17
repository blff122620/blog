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

function forEach(fn){
  for(let i=0; i<this.length; i++){
    fn(this[i],i,this);
  }
}

function isPrime(num){
  let index = num - 1;
  for(;index>1;index--){
    if(num%index === 0){
      return false;
    }
  }
  return true;
}

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


### call、apply和bind
  都是Function.prototype上的方法。
  call, apply调用一个具有给定this值的函数,以及参数;
  bind创建一个新函数, 这个新函数的 this 被指定为 bind() 的第一个参数，而其余参数将作为新函数的参数，供调用时使用;
  
```
  let obj = {
    name: 'test1'
  }

  function sayHello(arg) {
    console.log('hi,' + this.name + arg);
  }
  
  sayHello.call(obj, ',ok') // hi,test1,ok

  sayHello.apply(obj, [',ok']) // hi,test1,ok
  
  sayHello.bind(obj, ',ok')(); // hi,test1,ok
  
```
call, apply的区别:
call方法接受一个若干参数的列表, apply方法接受一个包含多个参数的数组。

#### 如何实现call、apply和bind
思路：先将对象上添加一个函数，然后执行，完成后删除。

```
  let obj = {
    name: 'test1'
  }

  function sayHello(arg) {
    console.log('hi,' + this.name + arg);
  }

```

call的实现:
```
  Function.prototype.call2 = function(obj, ...args) {
    let context = obj || window;
    context.__fn__ = this;
    let result = context.__fn__(args);
    delete context.__fn__;
    return result;
  }
```

apply的实现:
```
  Function.prototype.apply2 = function(obj, arr) {
    let context = obj || window;
    context.__fn__ = this;
    
    let result;
    if(!arr) {
      result = context.__fn__()
    } else {
      result = context.__fn__(...arr);
    }
    delete context.__fn__;
    return result;
  }
```

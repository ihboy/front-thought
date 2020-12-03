### var、let和const
  声明变量:  
  var: 声明一个变量，并可选地将其初始化为一个值。   
  let: 声明一个<b>块级作用域</b>的本地变量，并且可选的将其初始化为一个值。   
  const: 声明一个<b>块级作用域</b>的本地常量, 需要初始值。  
  
#### 1.块级作用域
  var 没有块级作用域; let和const有块级作用域。
```
  if(true) {
    var test = 'test';
  }
  console.log(test);

  if(true) {
    let test1 = 'test1';
    const test2 = 'test2';
  }
  console.log(test1, test2);  // 报错 未定义
```
#### 2. 重定义
  var 重复定义变量不会报错，后面会覆盖前面; let 和 const 重复定义会报错。
  
#### 3. 变量提升
  var 和 let 都存在变量提升, 代码如下:
```
 let x = 'global'
  {
    console.log(x) // Uncaught ReferenceError: x is not defined
    let x = 1
  }

  if(true) {
    console.log(test);   // undefined
    var test = 'test'
  }

```
#### 4. 暂时性死区
  暂时性死区就是进入当前作用域, 变量在声明之前已经存在,但是无法访问, 声明后才可以访问。
  如3中代码, x打印的应该是'global',然而是报错, 这是由于let存在<b>暂时性死区</b>
  
  
  
### 参考
1.https://stackoverflow.com/questions/31219420/are-variables-declared-with-let-or-const-hoisted/31222689#31222689
2.https://juejin.cn/post/6844903704189992973


# 前置准备

**promise的原理和then,catch,all,race的用法！**

> https://blog.csdn.net/qq_34645412/article/details/81170576
> ==**https://segmentfault.com/a/1190000007463101#articleHeader2**==



## _准备_ - 函数对象与实例对象

1. 函数对象与实例对象
    - 函数对象: 将函数作为对象使用时, 简称为函数对象
  - 实例对象: new 函数产生的对象, 简称为对象

```html
  <script>
    function Fn() {   // Fn函数 
    }
    const fn = new Fn() // Fn是构造函数  fn是实例对象(简称为对象)
    console.log(Fn.prototype) // Fn是函数对象
    Fn.call({}) // Fn是函数对象
    $('#test') // jQuery函数
    $.get('/test') // jQuery函数对象

    function Person(params) {
      
    }
  </script>
```

`const  实例对象 = new  构造函数( )`

( ) 左边的是函数 

. 左边的是函数对象





## _准备_ - 回调函数的分类

回调函数的三个条件：

- 我自己定义的【setTimeout( ) 就不是回调函数，因为不是自主定义的】

- 但是我没有亲自去调用

- 最后也需要执行

  

1). 同步回调: 
  理解: 立即执行, 完全执行完了才结束, 不会放入回调队列中
  例子: 数组遍历（forEach）相关的回调函数 / Promise的excutor函数
2). 异步回调: 
  理解: 不会立即执行, 会放入回调队列中将来执行
  例子: 定时器回调 / ajax回调 / Promise的成功|失败的回调

```html
  <script>
    // 1. 同步回调函数
    // const arr = [1, 3, 5]
    arr.forEach(item => { // 遍历回调, 同步回调函数, 不会放入列队, 一上来就要执行完
      console.log(item)
    })
    console.log('forEach()之后')

    // 2. 异步回调函数
    setTimeout(() => { // 异步回调函数, 会放入队列中将来执行
      console.log('timout callback()')
    }, 0)
    console.log('setTimeout()之后')
  </script>
```





## _准备_ - JS的error处理

  目标: 进一步理解JS中的错误(Error)和错误处理
    mdn文档: https: //developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Error

1. 错误的类型
    Error: 所有错误的父类型
    ReferenceError: 引用的变量不存在
    TypeError: 数据类型不正确的错误
    RangeError: 数据值不在其所允许的范围内
    SyntaxError: 语法错误
2. 错误处理
    捕获错误: try ... catch
    抛出错误: throw error
3. 错误对象
    message属性: 错误相关信息
    stack属性: 函数调用栈记录信息



```html
<script>
  // 1. 常见的内置错误
  // =======1). ReferenceError: 引用的变量不存在========
  // console.log(a) // ReferenceError: a is not defined
  // console.log('-----') // 没有捕获error, 下面的代码不会执行

  // =======2).TypeError: 数据类型不正确的错误=======
  // let b   // 因为这里的b不是一个对象，不能获取他的属性xxx【如果要让控制台不报错，至少要让他是一个空对象，let b = { }】
  // // console.log(b.xxx) // TypeError: Cannot read property 'xxx' of undefined
    
  // b = {}   // 这里可以使用b.xxx，但是结果为undefined，并且这不是一个函数
  // // b.xxx() // TypeError: b.xxx is not a function


  // =======3).RangeError: 数据值不在其所允许的范围内=======
  // 这里的递归调用要有次数限制，否则就是死循环
  // function fn() {
  //   fn()
  // }
  // fn() // RangeError: Maximum call stack size exceeded

  // ========4).SyntaxError: 语法错误==========
  // 双引号里面不应该再出现双引号。应该是单引号
  // const c = """" // SyntaxError: Unexpected string

    
  // 2. 错误处理
  // 捕获错误: try ... catch
  // try {
  //   let d
  //   console.log(d.xxx)
  // } catch (error) {
  //   console.log(error.message)
  //   console.log(error.stack)
  // }
  // console.log('出错之后')

  // 抛出错误: throw error
  function something() {
    if (Date.now()%2===1) {
      console.log('当前时间为奇数, 可以执行任务')
    } else { // 如果时间是偶数抛出异常, 由调用来处理
      throw new Error('当前时间为偶数无法执行任务')  
    }
  }

  // 捕获处理异常
  try {
    something()
  } catch (error) {
    alert(error.message)
  }
</script>
```





# promise

## promise是什么？

抽象表达：

promise是JS中进行异步编程的新的解决方案【旧的是谁？】



具体表达：

- 从语法上来说：promise是一个构造函数

  > ```
  > var promise = new Promise(function(resolve,reject){
  >     //do something;
  > })
  > ```
  >
  > Promise 是[异步编程](https://so.csdn.net/so/search?q=异步编程&spm=1001.2101.3001.7020)的一种解决方案，其实是一个构造函数，自己身上有all、reject、resolve这几个方法，原型上有then、catch等方法。

- 从功能上来说，promise对象用来封装一个异步操作并可以获取其结果

  

## promise的状态改变

1. pending（未确定的）变为resolved（成功）
2. pending（未确定的）变为rejected（失败）

说明：只有这两种，且每一个promise对象只能改变一次

​			无论变成成功还是失败，都会有一个结果数据

​			成功的数据一般称为**value**，

​			失败的结果数据一般称为**reason**





## promise基本运行流程

![image-20220511143855445](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220511143855445.png)





## promise基本使用

```html
  <script>
    // 1. 创建一个新的promise对象
    // 定义一个新的变量，首先是定义成const ，如果后面产生了变化，再把他变成let【能不改就不改】
    const promise = new Promise((resolve,reject)=>{
      // 执行异步操作任务
      setTimeout(() => {
        // 如果当前时间是偶数就代表成功, 否则代表失败
        const time = Date.now()
        // 如果成功，就执行resolve(value), promise对象变成resolved状态
        if(time % 2 == 0){
          resolve('成功的数据'+time)  // value
        }
        // 如果失败，就执行reject(reason), promise对象变成rejected状态
        else{
          reject('失败的数据'+time)   // reason
        }
      }, 2000);
    })

    promise.then(
      // onResolved() 回调 ，value是接收到的成功数据 -- ('成功的数据'+time)
      value =>{
        console.log('成功的回调',value)
      },

      // onRejected() 回调，reason是接收到的失败数据 -- ('失败的数据'+time)
      reason=>{
        console.log('失败的回调',reason);
      }
    )

    // promise.then(
    //   function(){},
    //   function(){}
    // )

    // promse.then(
    //   ()=>{},
    //   ()=>{}  // 上面的value，reason省略了参数的括号
    // )

  </script>
```



## 为什么要用promise

1. **指定回调函数的方式更加灵活:** 
   

  【使用纯回调函数】旧的: 必须在启动异步任务前指定

  ![image-20220511160252847](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220511160252847.png)  

  

  【使用promise】新的：promise: 启动异步任务 => 返回promie对象 => 给promise对象绑定回调函数(甚至可以在异步任务结束后指定)

  ![image-20220511160340560](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220511160340560.png)

  ![image-20220511161709401](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220511161709401.png)

  

2. **支持链式调用, 可以解决回调地狱问题**

     - 什么是回调地狱? 回调函数嵌套调用, 外部回调函数异步执行的结果是嵌套的回调函数执行的条件
     - 回调地狱的缺点?  不便于阅读 / 不便于异常处理
     - 解决方案? promise链式调用
     - 终极解决方案? async/await

【回调地狱】

![image-20220511162219252](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220511162219252.png)



【链式调用】

![image-20220511162305871](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220511162305871.png)

类似

> ![image-20220511231152375](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220511231152375.png)

【async 和 await 】

![image-20220511162326361](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220511162326361.png)



（）





## Promise的API

```
new Promise ( ( resolve, reject )=>{ } )
p.then( 两个回调函数 )
```

![image-20220511165148665](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220511165148665.png)

1. Promise构造函数: Promise (**excutor**){}
    excutor函数: **同步回调**    (resolve, reject) => {}
    
    
    
    resolve函数: 内部定义成功时我们调用的函数 value => {}
    reject函数: 内部定义失败时我们调用的函数 reason => {}
    ==**说明: excutor会在Promise内部立即同步回调,异步操作在执行器中执行**==
    
    ![image-20220511161648442](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220511161648442.png)
    
2. Promise.prototype.then方法: (**onResolved, onRejected**)  => {}
    onResolved函数: 成功的回调函数  (value) => {}
    onRejected函数: 失败的回调函数 (reason) => {}
    说明: 指定用于得到成功value的成功回调和用于得到失败reason的失败回调
          返回一个新的promise对象

3. Promise.prototype.catch方法: (**onRejected**)  => {}
    onRejected函数: 失败的回调函数 (reason) => {}
    说明: then()的语法糖, 相当于: then(undefined, onRejected)

    
    
4. Promise.resolve方法: (**value**)  => {}
    value: 成功的数据或promise对象
    说明: 返回一个成功/失败的promise对象

5. Promise.reject方法: (**reason**)  => {}
    reason: 失败的原因
    说明: 返回一个失败的promise对象

    ![image-20220511173721026](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220511173721026.png)
    
6. Promise.all方法: (**promises**) => {}
    promises: 包含n个promise的数组
    说明: 返回一个新的promise, 只有所有的promise都成功才成功, 只要有一个失败了就直接失败
    
7. Promise.race方法: (**promises**)  => {}
    promises: 包含n个promise的数组
    说明: 返回一个新的promise, 第一个完成的promise的结果状态就是最终的结果状态



## promise的几个关键问题

    如何改变promise的状态?
    一个promise指定多个成功/失败回调函数, 都会调用吗?
    promise.then()返回的新promise的结果状态由什么决定?
    改变promise状态和指定回调函数谁先谁后?
    promise如何串连多个操作任务?
    promise异常传(穿)透?
    中断promise链

1. 如何改变promise的状态?

   (1)resolve(value): 如果当前是pending就会变为resolved

   (2)reject(reason): 如果当前是pending就会变为rejected

   (3)抛出异常: 如果当前是pending就会变为rejected

  

2. 一个promise指定多个成功/失败回调函数, 都会调用吗?

   当promise改变为对应状态时都会调用

```html
  <script>
    const p = new Promise((resolve,reject)=>{
      // resolve(1)  // promise 变成resolved 成功状态
      // reject(2)   // promise 变成rejected 失败状态
      // throw new Error('出错了')  // 抛出异常，promise变成rejected失败状态，reason为抛出的error
      throw 3  // 抛出异常，promise变成rejected失败状态，reason为抛出的 3 [类似于reject(3)]
    })
    p.then(
      value => {},
      reason =>{console.log('reason',reason);}
    )
  </script>
```





3. 改变promise状态和指定回调函数谁先谁后?

   (1)都有可能, 正常情况下是先指定回调再改变状态, 但也可以先改状态再指定回调

   (2)如何先改状态再指定回调?

​    ①在执行器中直接调用resolve()/reject()，不使用setTimeout( ()=>{},xxxx )

​    ②延迟更长时间才调用then()

   (3)什么时候才能得到数据?

​    ①如果先指定的回调, 那当状态发生改变时, 回调函数就会调用, 得到数据

**【先指定的回调函数，此时promise的状态还是pending；然后当状态发生改变（pending->resolved 或者 pending->rejected，也就是excutor中执行resolve()或者reject()）的时候，回调函数(异步执行)就会调用，得到数据（成功就是value,失败就是reason）】**

​    ②如果先改变的状态, 那当指定回调时, 回调函数就会调用, 得到数据



**// 如果上面的是异步操作，就代表成功的回调函数会放在回调队列中执行，**
==**// 而 js渲染的时候是先将初始化的代码执行完之后，再执行队列里的回调**==

```html
<script>    
 // 常规：先指定回调函数，再改变状态
    new Promise((resolve,reject)=>{
      // 异步执行操作
      setTimeout(() => {
        resolve(222)  // 后改变状态（同时指定数据）。异步执行回调函数
      }, 1000);
    }).then(  // 先指定回调函数，状态还没改，所以这里先保存当前指定的回调函数
      value=>{
        console.log('成功的回调'+value);
      }
    )


    // 去掉异步操作：先改变状态，后指定回调函数
    new Promise((resolve,reject)=>{
        // 这里没有设置延时器，所以是同步执行的 
        resolve(222)  // 先改变状态（同时指定数据）
    }).then(  // 后指定回调函数，.then是同步执行的
      value=>{
        console.log('成功的回调'+value);
      }
    )
// 如果上面的是异步操作，就代表成功的回调函数会放在回调队列中执行，
// 而 js渲染的时候是先将初始化的代码执行完之后，再执行队列里的回调
// 所以如果先输出===============，再输出回调，就代表是异步的
    console.log('=================');
</script>
```





4.  promise.then()返回的新promise的结果状态由什么决定?==【P16-P18】==

   (1)简单表达: 由then()指定的回调函数执行的结果决定

   (2)详细表达:

​     ①如果抛出异常, 新promise变为**rejected**, reason为抛出的异常

​			throw 5

​     ②如果返回的是非promise的任意值, 新promise变为**resolved**, value为返回的值

​			return 2

​     ③如果返回的是另一个新promise, 此promise的结果【resolve,reject二选一】就会成为新promise的结果

​			return 	Promise.resolve(3) 

​			return 	Promise.reject(4) 

```html
  <script>
    /* 
    4.	promise.then()返回的新promise的结果状态由什么决定?
      (1)简单表达: 由then()指定的回调函数执行的结果决定
      (2)详细表达:
          ①如果抛出异常, 新promise变为rejected, reason为抛出的异常
          ②如果返回的是非promise的任意值, 新promise变为resolved, value为返回的值
          ③如果返回的是另一个新promise, 此promise的结果就会成为新promise的结果 
    */

    new Promise((resolve, reject) => {
      resolve(1)
      // reject(1)
      // throw 1
      // return 1 // 这个在这里没有效果
    }).then(
      value => {
        console.log('onResolved1()', value)
        // return 2

        // return Promise.resolve(3)
        // 等同于上面的作用 == Promise.resolve(3)是简化的语法糖
        /**
         *return new Promise((resolve,reject)=>{
         *  resolve(3)
         *})
        */
        
        // return Promise.reject(4)
        // throw 5
      },
      reason => {
        console.log('onRejected1()', reason)
        // return 2
        // return Promise.resolve(3)
        // return Promise.reject(4)
        throw 5
      }
    ).then(
      value => {
        console.log('onResolved2()', value)
      },
      reason => {
        console.log('onRejected2()', reason)
      }
    )

  </script>
```



5.promise如何串连多个操作任务?

   (1)promise的then()返回一个新的promise, 可以开成then()的链式调用

   (2)通过then的链式调用串连多个同步/异步任务



=>作用：

1. 定义匿名函数

2. 看作为return，但是此时不能有{ }  

   ```
   reason => Promise.reject ( reason )
   等同于
   return Promise.reject ( reason )
   ```

   { } 是函数体的标记

   ```
   reason => { throw reason }
   这里的 =>不是return
   ```

   





  6.promise异常传透?

   (1)当使用promise的then链式调用时, 可以在最后指定失败的回调, 

```
reason => { throw reason }

reason => Promise.reject ( reason )
```

   (2)前面任何操作出了异常, 都会传到最后失败的回调中处理



  7.中断promise链?

   (1)当使用promise的then链式调用时, 在中间中断, 不再调用后面的回调函数

   (2)办法: 在回调函数中返回一个pendding状态的promise对象





# 自定义promise

```
1. 定义整体结构
2. Promise构造函数的实现
3. promise.then()/catch()的实现
4. Promise.resolve()/reject()的实现
5. Promise.all/race()的实现
6. Promise.resolveDelay()/rejectDelay()的实现
7. ES6 class版本
```



- ==excutor中的resolve(1) ,这一行并不是立即同步执行，而是状态立即变成了成功。从而立即将.then()中的onResolved放入微队列【从而进行异步回调】==

```js
 try {
            /**
             * 例如：excutor中的resolve(1) ,这一行并不是立即同步执行，
             * 而是状态立即变成了成功。从而立即将.then()中的onResolved放入微队列【从而进行异步回调】
             * 这里实现将onResolved放入微队列的手段是：将onResolved放在定时器setTimeout，但是本质上setTimeout属于宏队列的一种
             */
            const result = onResolved(self.data) // 这一行获取到的是excutor的promise结果
            if(result instanceof Promise){  //3.如果返回的是另一个新promise, 此promise的结果【resolve,reject二选一】就会成为新promise的结果
              result.then(
                value => resolve(value),
                reason => reject(reason)
              )
            }else{ // 2.如果返回的是非promise的任意值, 新promise变为resolved, value为返回的值
              resolve(result)
            }
          } catch (error) {
            reject(error)  // 1.如果抛出异常, 新promise变为rejected, reason为抛出的异常
          }
```



# async 和 await 

  目标: 进一步掌握async/await的语法和使用
    mdn文档:

- async：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/async_function   

-  await：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/await

    1. async 函数
            函数的返回值为promise对象
            promise对象的结果由async函数执行的返回值决定
       2. await 表达式
             await右侧的表达式一般为promise对象, 但也可以是其它的值
               如果表达式是promise对象, await返回的是promise成功的值
               如果表达式是其它值, 直接将此值作为await的返回值
3. 注意:
    await必须写在async函数中, 但async函数中可以没有await
    如果await的promise失败了, 就会抛出异常, 需要通过try...catch来捕获处理



# JS异步之宏队列与微队列💥💥

1. 宏列队: 用来保存待执行的宏任务(回调), 比如: 定时器回调/DOM事件回调/ajax回调
2. 微列队: 用来保存待执行的微任务(回调), 比如: promise的回调/MutationObserver的回调
3. JS执行时会区别这2个队列
	**JS引擎首先必须==先执行所有的初始化同步任务代码==**
	💥💥💥**==每次==准备取出==第一个宏任务==执行前, 都要将所有的微任务一个一个取出来执行**💥💥💥

![宏队列与微队列](http://vipkshttp1.wiz.cn/ks/share/resources/49c30824-dcdf-4bd0-af2a-708f490b44a1/92b8cbfb-a474-4859-943b-6048e9dc66f6/index_files/60b9ff398449db2dcfef9197e2187ae6.png)

# 重点案例💥💥💥💥

**先指定的回调，此时promise状态还是pending，先将回调函数保存起来；等待resolve(1)去触发onResolved回调函数**

**定时器时间一到，状态改变是立即改变的，但是回调函数是异步执行的==【异步执行的体现：不会立即执行, 会放入回调队列中将来执行，下面使用console.log('reject()改变状态之后')来辅助说明情况】== **
**所以先执行完exutor里面的函数【此时状态也同时改变了，例如：reject(2)，代表p已经成功了。==此时才能将p.then指定的回调立马放入微队列中==】，然后再去根据resolve或者reject去触发对应的onResolved或者onRejected**

```html
  <script src="./lib/Promise.js"></script>
  <script>
    const p = new Promise((resolve, reject) => {
      setTimeout(() => {
        // 先指定的回调，此时promise状态还是pending，先将回调函数保存起来；[放入到callbacks中]等待resolve(1)去触发onResolved回调函数
        // 定时器时间一到，状态改变是立即改变的，但是回调函数是异步执行的，【异步执行的体现：不会立即执行, 会放入回调队列中将来执行，下面使用console.log('reject()改变状态之后')来说明情况】 
          
        // 补充：这里的- reject()和resolve() 是采用的 直接调用，所以在 手写promise代码的时候 Promise构造函数里面的reject函数【if (this.status !== PENDING)】里面的this指向为window

        // resolve(1)
        reject(2) // 这一处状态是立即变成了失败。从而立即将p.then()中的onRejected放入微队列，【异步执行回调，是放在回调队列中执行的，所以即使这里写在 console.log('reject()改变状态之后') 语句的前面，也并没有比这个console.log() 初始的语句执行得快】，
        console.log('reject()改变状态之后')  // 1. 输出“reject()改变状态之后”，
        /**
         * 这里的console.log('reject()改变状态之后')不管是放在 reject(2) 的上面还是下面，都会输出一样的结果，
         * 【因为reject(2) 只是立马放入微队列(不是立马执行)，这种情况并没有初始化的语句执行快（初始化语句不需要放入队列之后取出执行，而是直接执行）】
         */
      }, 100);  
      // 这里设置了延时器，所以先指定回调【这种情况需要把then中的回调函数先保存起来】，然后再等定时器时间一到，在定时器中执行reject或者resolve，从而分别将onResolved或者onRejected放入微队列
    })
    p.then(
      value => {
        console.log('onResolved1()', value)
      },
      reason => {
        console.log('onRejected1()', reason)  // 2. onRejected1() 2
        // return undefined ;  ==> resolve --- undefined
      }
    )
    p.then(
      value => {
        console.log('onResolved2()', value)  // 3. onResolved2() undefined
      },
      reason => {
        console.log('onRejected2()', reason)
      }
    )
    
  </script>
```





# 面试题3

```html
  <script>
    // 不去除resolve(1)
    // 3 7 4 1 2 5

    // 去除resolve(1)
    /* 
    宏: [5]
    微: [first]
    */

    // 3 7 4 2 5 6
    const first = () => (new Promise((resolve, reject) => {
      console.log(3)
      let p = new Promise((resolve, reject) => {
        console.log(7)
        setTimeout(() => {
          // console.log(5)
          resolve(6)  // 要先等定时器开始执行，才能执行resolve(6),从而让P能够成功，然后将p.then指定的回调立马放入微队列中
          console.log(5) 
          // 这里的console.log(5)不管是放在resolve(6)的上面还是下面，都会输出一样的结果，
          // 【因为resolve(6)只是立马放入微队列，还是没有初始化的语句（不需要放入队列之后取出执行，而是直接执行）执行快】
        }, 0)
        // resolve(1)
      })
      resolve(2)  // 这里的resolve(2),让最外面的promise立马成功，所以first().then()指定的回调函数立马放入微队列中
      p.then((arg) => {  
        // p没有立即放入微队列是因为，【去掉了resolve(1),从而让P不能立马成功】因此这里没有做到立马改变状态，所以p.then指定的回调不应该立马放入微队列中
        console.log(arg)
      })

    }))

    first().then((arg) => {
      console.log(arg)
    })
    console.log(4)
  </script>
```



# 面试题4

```html
  <script>
    /*  1 7 2 3 8 4 6 5 0
    1,7 是同步回调newPromise，直接执行输出
    （13,30行）是并列的微队列，
    宏: []
    微: [2,8]
    */
    setTimeout(() => {  //遇到定时器setTimeout，放入宏队列（宏任务1
      console.log("0")
    }, 0)

    new Promise((resolve, reject) => {
      console.log("1")   // 遇到同步回调newPromise，直接执行输出 1
      resolve()  // 让外层的promise立即成功，将外层promise指定的回调函数立即放入微队列中
    }).then(() => { //遇到.then 【主要是resolve()或者reject()也要有，让外层promise立即成功/失败才行】将该部分放入微队列（微任务1）== 打印2
      console.log("2")
      new Promise((resolve, reject) => {
        console.log("3")
        resolve()  // 相当于return undefined，resolve()让内部指定的promise立即成功，将.then()中 内层promise指定的回调函数onResolved立即放入微队列中
      }).then(() => {  // （微任务3）== 打印4
        console.log("4")  //相当于resolve() ，让这次产生的promise为立即成功，
      }).then(() => {   // 这个then依赖于前面的（21行）微任务 ，要等微任务3执行完，也就是从微队列中取出之后，微任务5才能放入微队列 // （微任务5）== 打印5
        console.log("5")  //相当于resolve() 
      })
    }).then(() => {     // （微任务4）== 打印6
      console.log("6")
    })

    new Promise((resolve, reject) => {
      console.log("7")  // 遇到同步回调newPromise，直接执行输出 7
      resolve()
    }).then(() => {  //遇到.then 将该部分放入微队列（微任务2）== 打印8
      console.log("8")
    })

// 下面的代码验证了与传入的参数无关，主要是前后顺序，上面的默认是onResolved,而下面的默认是onRejected
  // }).then(   
  //   (value) => {  //遇到.then 将该部分放入微队列（微任务2）== 打印8
  //     console.log("8",value)
  //   },
  //   (reason) => {  //遇到.then 将该部分放入微队列（微任务2）== 打印8
  //     console.log("xxx",reason)
  //   } )
  </script>
```

先找到同步任务，然后再去找异步任务，异步任务里面分为宏队列和微队列，微队列优先级高于宏队列。

遇到.then，需要判断是否依赖于前面的微任务：

- 如果不依赖前面的结果，直接将该部分放入微队列

- 如果依赖前面的结果，暂时不能将该部分放入微队列，应该等待它依赖的微任务执行完毕之后，将其放入

  

---

---

---

**先找到同步任务：**

== == == == =》1 7 



---

**按顺序执行 找异步任务：**

执行完【15行】的**resolve**()，//遇到.then 将该部分【16-26行是一个整体】放入微队列（微任务1）

执行完【32行】的**resolve**()，//遇到.then 将该部分【33-35行是一个整体】放入微队列（微任务2）

- 【宏队列（0），微队列（2 , 8）】



---

【将2从微队列拿出去，意味着里面的 都要执行完，然后才能接着执行下面的微队列8】

- 【宏队列（0），微队列（8）】 （队列先进先出）

== == == == =》1 7 2

 **微任务1——微队列中的代号2 的执行过程：**

1. 先输出 2，

2. 然后因为这个微任务2内部又newPromise，属于同步回调，直接输出3，

   == == == == =》1 7 2 3

   

   ---

   

3. 然后执行完【20行】的**resolve**()，会遇到一个新的 .then, 放入微队列（微任务3，代号4）

- 【宏队列（0），微队列（8，4）】 （队列先进先出）

  - 此时【23】遇到.then ，暂时不会将该部分放入微队列，因为该任务依赖于微任务3，微任务3还没有执行完。（等后面微任务3——也就是微队列中的代号4，被拿出队列的时候，此时代号5才能进入微队列

    

4. **==【26】因为微任务1执行完毕，所以遇到.then 将该部分放入微队列（微任务4）==**

​		==1走，6上==（代号1执行完，代号6会立即放到待执行队列里面）

- 【宏队列（0），微队列（8，4，6）】 （队列先进先出）（微任务4，代号6）

  

---

【将8从微队列拿出去，意味着里面的 都要执行完，然后才能接着执行下面的微队列4】

- 【宏队列（0），微队列（4 , 6）】 （队列先进先出）

== == == == =》1 7 2 3 8

 **微任务2——微队列中的代号8 的执行过程：**

1. 先输出8，后续没有操作，即进行微队列中代号4的操作

   

----

【将4从微队列拿出去，意味着里面的 都要执行完，然后才能接着执行下面的微队列6】

- 【宏队列（0），微队列（6 , 5）】 （队列先进先出）

== == == == =》1 7 2 3 8 4

 **微任务3——微队列中的代号4 的执行过程：**

> 此时【23】遇到.then ，暂时不会将该部分放入微队列，因为该任务依赖于微任务3，微任务3还没有执行完。（等后面微任务3——也就是微队列中的代号4，被拿出队列的时候，此时代号5才能进入微队列

执行微任务3的过程中，终于能把代号5 放入微队列（微任务5，代号5）

==4走，5上==（代号4执行完，代号5会立即放到待执行队列里面）







![image-20220513100052353](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220513100052353.png)





# 综合理解

![image-20220513213409822](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220513213409822.png)

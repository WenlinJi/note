> **尚硅谷**
>
> > https://www.bilibili.com/video/BV1YW411T7GX
>
> 
>
> - **第一种github笔记**： https://github.com/chuyueZhang/frontEndLearning 
>   我学习过的所有前端视频的知识点我都做了整理
>   练习案例大部分可以直接运行，不过路径下有package.json文件的需要使用npm下载依赖哦(｀・ω・´)
>   对笔记中有问题想提出的朋友可以直接私信我或者从github中提出
>   笔记持续更新中~~~
>- **第二种博客笔记：**https://blog.csdn.net/weixin_44949135/article/details/113242327
> - **JavaScript中原型对象的彻底理解：**https://blog.csdn.net/u012468376/article/details/53121081
>- **对象原型 - 学习 Web 开发 MDN：**https://developer.mozilla.org/zh-CN/docs/Learn/JavaScript/Objects/Object_prototypes#%E5%9F%BA%E4%BA%8E%E5%8E%9F%E5%9E%8B%E7%9A%84%E8%AF%AD%E8%A8%80%EF%BC%9F



# 部分总结

## this指向

（P11）this的不同的情况：
\1. 以函数的形式调用时，this永远都是window
\2. 以方法的形式调用时，this就是调用方法的对象
\3. 以构造函数的形式调用时，this就是新创建的对象
\4. 使用call和apply调用时，this就是指定的那个对象
\5. 在全局作用域中this代表window

## 作用域链与原型链

**==A.B==**

==A为对象——沿着**作用域链**往上找。==

==找到A以后，确保A是一个对象，接着去对象中找对应的属性B==

==B（对象的属性）方法——沿着A对象所在的**原型链**往上找==

==找不到就返回undefined==



> 如果没有定义全局变量a：
>
> 然后去找 **window.a** ——返回undefined
>
> 如果直接去找 **a** ——报错
>
> 虽然有时候 直接写 a 就相当于 window.a 但是有细小区别，就看找不到之后，它如何处理 



执行上下文与作用域：

作用域在

执行上下文是动态创建的，尤其是函数执行上下文，他不会一直存在，调用函数的时候产生，函数执行完就死亡

# 高级JavaScript

![img](https://img-blog.csdnimg.cn/20210127160113480.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDk0OTEzNQ==,size_16,color_FFFFFF,t_70)

![JavaScript高级day01总结图](C:\Users\051129\Desktop\JavaScript高级day01总结图.png)

## ==数据==类型相关知识点

> https://blog.csdn.net/rogerjava/article/details/6982460?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_baidulandingword~default-5.pc_relevant_default&spm=1001.2101.3001.4242.4&utm_relevant_index=8

> https://blog.csdn.net/qq_34629352/article/details/79051207?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_baidulandingword~default-0.pc_relevant_default&spm=1001.2101.3001.4242.1&utm_relevant_index=3

在 JS  中，除了原始类型那么其他的都是对象类型了。对象类型和原始类型不同的是，原始类型存储的是值，对象类型存储的是地址（指针）。当你创建了一个对象类型的时候，计算机会在内存中帮我们开辟一个空间来存放值，但是我们需要找到这个空间，这个空间会拥有一个地址（指针）。



>     什么是函数？
>     
>     JavaScript 函数是通过 function 关键词定义的。您可以使用函数声明或函数表达式。
>     
>     什么是对象？
>     
>     在 JavaScript 中，对象是王。如果您理解了对象，就理解了 JavaScript。
>     在 JavaScript 中，几乎“所有事物”都是对象。
>     布尔是对象（如果用 new 关键词定义）
>     数字是对象（如果用 new 关键词定义）
>     字符串是对象（如果用 new 关键词定义）
>     日期永远都是对象
>     算术永远都是对象
>     正则表达式永远都是对象
>     数组永远都是对象
>     函数永远都是对象
>     对象永远都是对象
>     所有 JavaScript 值，除了原始值，都是对象。
> ————————————————
> 版权声明：本文为CSDN博主「慕尼黑、」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
> 原文链接：https://blog.csdn.net/qq_44192588/article/details/105269968

### 基本类型（值类型）

String ——任意的字符串

Number——任意的数字

Boolean——true/false

undefined——undefined

null——null（使用 typeof 时返回object，这是因为在null可作为约定俗成的占位符——让对象成为垃圾对象）



### ==对象==类型（引用类型）

Object  任意对象

Function 一种特殊的对象——能够执行（内部包含可运行的代码）

Array 一种特殊的对象——key为数值下标属性，内部数据是有序的（使用typeof时返回object）





## 数据,变量, 内存的理解

### 严格区分数据类型和变量类型

> 数据类型
>
> - 基本类型
>
> - 对象类型（引用类型）



> 变量类型（**根据变量内 存值的类型划分**）
>
> - 基本类型——存储的是基本类型的数据本身
>
> - 引用类型——存储的是地址值（有时也叫对象类型）



### Ⅰ-什么是数据?

**一切皆数据**

存储在内存中代表特定的信息的东西，本质上是01010...

内存中所有操作的目标：数据



### Ⅱ-什么是变量?

==**变量**==

**全局变量和局部变量  一般存放在内存的 栈 部分**

变量的本质就是在==内存==中申请一个**存储单元**，由于该存储单元中的==数据==内容可以发生变化，因此得名为变量。

作为内存的标识

可变化的量, 由变量名和变量值组成

- 每个变量都对应的一块小内存, 

- - 变量名（obj）用来查找对应的内存, 

- - 变量值（xx——name）就是内存中保存的数据

    > **存储的数据类型不同导致会产生两种变量类型：**
    >
    > 基本类型——存储的是基本类型的数据本身
    >
    > 引用类型——存储的是地址值（有时也叫对象类型）

- ==ps:变量`obj.xx`-->`.`相当于拿着 xx的地址 找到 xx对应的内存,所以只有当我变量中存的是地址,才可以用`.`==

### Ⅲ-什么是内存?

1. 内存条通电后产生的可储存数据的空间(临时的)

2. 通电——开辟一部分内存空间——存储数据——处理数据——断电——内存空间和数据消失



3. 一块内存中存放2个数据：

- 内部存储的数据                                    —— {name:'Tom'} 
- （这一块内存空间==自身的==）地址值     —— 0x123



4. 内存分类：

   - 栈：全局变量，局部变量
   - 堆：对象

   ![img](https://gitee.com/hongjilin/hongs-study-notes/raw/master/%E7%BC%96%E7%A8%8B_%E5%89%8D%E7%AB%AF%E5%BC%80%E5%8F%91%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0/HTML+CSS+JS%E5%9F%BA%E7%A1%80%E7%AC%94%E8%AE%B0/JavaScript%E7%AC%94%E8%AE%B0/JavaScript%E7%AC%94%E8%AE%B0%E4%B8%AD%E7%9A%84%E5%9B%BE%E7%89%87/image-20210630192130518.png)

> 内存的 **栈** 中存放着全局变量，局部变量（每个变量都占用一小块内存）
>
> 这个局部变量（全局变量）由 变量名 和 变量值 构成
>
> - 变量名：查找对应的内存
> - 变量值：内存中保存的数据   （基本类型的数据 ， 或者是所在内存***地址值***）
>
> 
>
> obj 是变量名 
>
> 0x123是变量值==（是对象所在内存的***地址值***，而不是obj自身所在内存的地址值）==
>
> - obj自身也有一个***地址值***，但是不需要，所以不涉及
>
> 
>
> 变量名obj（以及变量名a）对应的变量值 都是（ 对象 {name:'Tom'} 的 ）地址值 0x123
>
> 

### Ⅳ-内存,数据, 变量三者之间的关系

> - 内存用来存储数据的空间。 内存是一个容器，用来存储程序运行需要操作的数
> - 变量是内存的标识，我们通过变量找到对应的内存，进而操作（读/写）内存的数据



### Ⅴ-相关问题引出

#### ① *关于赋值和内存的问题*

> let a = xxx, a内存中到底保存的是什么?
>
> - xxx是基本数据, 保存的就是这个数据
> - xxx是对象, 保存的是对象的地址值
> - xxx是一个变量, 保存的xxx的内存内容(可能是基本数据, 也可能是地址值)

#### ② *关于引用变量赋值问题*

> - 2个引用变量指向同一个对象, 通过一个变量修改对象内部数据, 另一个变量看到的是修改之后的数据
> - 2个引用变量指向同一个对象, 让其中一个引用变量指向另一个对象, 另一引用变量依然指向前一个对象
> - 代码示例:
>
> ```
>   let a = {age: 12}
> //此时是将a指向的地址值赋值给B,所以B此时也指向{age:12}这个内存
>   let b = a
> //此时重新创建了一个内存并让a指向它,所以此处a指向的是{name:'hong'},而b指向仍是刚开始的指向{age:12}
>   a = {name: 'hong'}
> //此时a与b指向的内存已经不一样了,所以修改互不影响
>   b.age = 14
>   console.log(b.age, a.name, a.age) // 14 hong undefined
>   //此时其实已经重新创建了一个内存{age:15},并且将其地址赋值覆盖给a
> //实际上传进来的obj也是拿着其key对应的地址值找内存,此时
>   const fn2=(obj) => obj = {age: 15}
>   fn2(a)
>   console.log(a.age) //15
> ```

#### ③ *在js调用函数时传递变量参数时, 是值传递还是引用传递*

> - 理解1: 都是值(基本/地址值)传递
> - 所以实际上传进function中的参数也是拿着其存着的地址值找内存
>
> ```
> //传进来的obj存储的是a中存的地址值,所以obj==a(因为他们地址值一致,指向一致)
> //2个引用变量指向同一个对象, 通过一个变量修改对象内部数据, 另一个变量看到的是修改之后的数据  -->所以被进行了修改
>   let a = {name: 'hong'}
>   const fn2=(obj) => obj.age= 15
>   fn2(a)
>   console.log(a.age) //15
> ```
>
> - 理解2: 可能是值传递, 也可能是引用传递(地址值)

#### ④ *JS引擎如何管理内存?*

> 1. 内存生命周期
>
> - 分配小内存空间, 得到它的使用权
> - 存储数据, 可以反复进行操作
> - 释放小内存空间
>
> 1. 释放内存
>
> - 局部变量: 函数执行完自动释放
> - 对象: 成为垃圾对象==>垃圾回收器回收
>
> ```
>  var a = 3
>  var obj = {name:"hong"}
>  obj = undefined ||null  //此时,obj没有被释放,但是之前声明的`{name:"hong"}`由于没有人指向它,会在后面你某个时刻被垃圾回收器回收
> 
> function fn () { var b = {}}
>  fn() // b是自动释放, b所指向的对象是在后面的某个时刻由垃圾回收器回收
> ```



## 🔥==变量、属性、函数、方法总结==

- **变量**：变量的本质就是在==内存==中申请一个**存储单元**，由于该存储单元中的==数据==内容可以发生变化，因此得名为变量。单独声明赋值，单独存在

- **函数**：（具有特定功能的n条语句的封装体，**函数也是对象**）单独存在的，通过==“函数名()”==的方式就可以调用

  > - 内存用来存储数据的空间。 内存是一个容器，用来存储程序运行需要操作的数据
  > - 变量是内存的标识，我们通过变量找到对应的内存，进而操作（读/写）内存的数据
  > - - ==内存用来存数据，变量可以用来找数据（在内存中）==

- 对象：（对象是多个数据的集合体，用于保存多个数据的容器）

- - 属性：不需要声明，用来描述该对象的特征

  - > 由属性名（字符串类型）和属性值（任意类型）组成

- - 方法：方法不需要声明，使用==“对象.方法名()”==的方式就可以调用，方法用来描述该对象的行为和功能。

  - > 有一种特别的的属性，它的属性值是函数（所以，这种属性被称为方法）

```
对象里的变量——属性（其中有一种特别的属性——方法）
——对象是多个数据的集合体，因为变量可以用来在内存中找数据，所以可以把变量（/属性）理解为是一种内存的标识
==内存用来存数据，变量可以用来找数据（在内存中）==

属性:（状态数据）
属性名——字符串类型 ; 属性值——任意数据类型（如果是函数，就是特殊的属性——方法）

方法:（行为数据）
属性名——字符串类型 ; 属性值——函数（对象类型的一种——Function）

函数也是对象（分为Object,Array,Function）的一种，对象类型是数据类型（分为基本，对象）的一种
```

> 对象的概念:一组"键值对"(key-value)的集合,无序的数据集合.(键值对是指"键名:键值"这种一对对的形式,其中键名(又称属性,成员)要遵守一定的命名和书写规则;键值可以是js的任何一种数据类型,这包括原始值primitive如number,string,boolean等,也包括一般对象object,函数Function,数组Array)

**对象属性**

==可以说 "JavaScript 对象是变量的容器"。==

==但是，我们通常认为 "JavaScript 对象是键值对的容器"。==

==键值对通常写法为 **name : value** (键与值以冒号分割)。==

==键值对在 JavaScript 对象通常称为 **对象属性**。==



| ![Note](https://www.runoob.com/images/lamp.jpg) | JavaScript 对象是属性变量的容器。           |
| ----------------------------------------------- | ------------------------------------------- |
|                                                 | https://www.runoob.com/js/js-obj-intro.html |





在 JS  中，除了原始类型那么其他的都是对象类型了。对象类型和原始类型不同的是，原始类型存储的是值，对象类型存储的是地址（指针）。当你创建了一个对象类型的时候，计算机会在内存中帮我们开辟一个空间来存放值，但是我们需要找到这个空间，这个空间会拥有一个地址（指针）。

```js
// 利用字面量创建对象 
var obj = {
 	// 属性名 ：属性值    
         name: '秦sir',
         age: 18,
         sex: '男',
         fn:function() {};
};
```



> https://blog.csdn.net/Augenstern_QXL/article/details/119250137  
>
> **关于如何创建对象：**
>
> - 利用字面量创建对象
>
> ```js
> var star = {
>     name : 'pink',
>     age : 18,
>     sex : '男',
>     sayHi : function(){
>         alert('大家好啊~');
>     }
> };
> // 多个属性或者方法中间用逗号隔开
> // 方法冒号后面跟的是一个匿名函数
> 
> ```
>
> - 利用 new Object创建对象
>
>   跟之前的 `new Array()` 原理一致：`var 对象名 = new Object();`
>
>   使用的格式：对象.属性 = 值
>
> ```js
> var obj = new Object(); //创建了一个空的对象
> obj.name = '张三丰';
> obj.age = 18;
> obj.sex = '男';
> obj.sayHi = function() {
>     console.log('hi~');
> }
> ```
>
> - 利用构造函数创建对象
>
> ```js
> //构造函数的语法格式
> function 构造函数名() {
>     this.属性 = 值;
>     this.方法 = function() {}
> }
> new 构造函数名();
> 
> //1. 构造函数名字首字母要大写
> //2. 构造函数不需要return就可以返回结果
> //3. 调用构造函数必须使用 new
> //4. 我们只要new Star() 调用函数就创建了一个对象
> //5. 我们的属性和方法前面必须加this
> ```
>

## 原型链

![原型链自画](C:\Users\051129\Desktop\前端图\原型链自画.png)



![前端稿图-7](C:\Users\051129\Desktop\前端图\前端稿图-7.jpg)



![原型链总结](C:\Users\051129\Desktop\前端图\原型链总结.png)





## 变量提升与函数提升

> https://www.bilibili.com/video/BV14s411E7qf?p=25&spm_id_from=pageDriver

==变量声明提升的优先级比函数声明提升的优先级高一些，且不会被同名的变量声明覆盖，但是变量赋值之后会覆盖==



函数声明的优先级高于变量声明，但是不高于变量赋值

优先级：变量声明提升<函数声明提升<变量赋值

![image-20220331190210816](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220331190210816.png)

```js
// 报错，因为在调用 c(2) 之前，变量赋值导致c = 2;将C变成了numbei类型
     var c=2; 
     function c(c){
         console.log(c);
     }
     c(2);

// 1. var c;    // 首先被赋值为c=undefined
// 2. function c(c){ }
// 3. c=2;   // 函数声明提升被变量赋值覆盖


// 下面的不报错，输出2，因为是在变量赋值之前调用了函数
    c(2);
    var c=2;
    function c(c){
        console.log(c);
    }

// var c
// function c
// c(2)
// c=2
```



```js
// 报错
    var c=2;
    c(2)
    function c(c){
        console.log(c);
    }

// 因为 c = 2 和 c(2) 的固定顺序是不会改变的，先赋值就会覆盖同名的函数声明提升
```



### 函数

#### 如何定义函数

> https://www.jianshu.com/p/24973b9db51a

![image-20220331195146157](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220331195146157.png)

具名函数的声明有两种方式：1. 函数声明式    2. 函数字面量式（变量形式声明 / 表达式）

```jsx
//函数声明式
function bar () {}
//变量形式声明； 
var foo = function () {}
```

#### 函数提升

函数——声明式的提升现象和变量提升略有不同，函数声明式会提升到作用域最前边，并且将声明内容一起提升到最上边，即进行了执行过程。

```jsx
bar()
function bar() {
  console.log(1);
}
//输出结果1
```

函数——变量形式声明 和普通变量一样 提升的 只是一个没有值的变量。

```jsx
bar()

var bar = function() {
  console.log(1);
}
// 报错：TypeError: bar is not a function

// 初始进行函数提升的时候，只是一个没有内容的函数声明（类似于变量提升的时候首先被定义为undefined，最后才会被赋值），没有进行调用

```





> 补充：

> - **变量提升**
>
> ```jsx
>     console.log(a);  //undefined
>     var a = 123; 
> ```
>
> 因为变量a的声明被提到了作用域顶端。上面代码编译后应该是下面这个样子
>
> ```jsx
>     var a;
>     console.log(a)
>     a = 123
>     //所以输出内容为 undeifend
> ```



## 闭包

![image-20220401095324712](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220401095324712.png)

![image-20220401095059903](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220401095059903.png)

![image-20220401100337077](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220401100337077.png)

两个题目里面的内部函数，会执行是因为加了括号，所以变成立即执行函数，没有谁去调用内部函数，他说自己执行的，所以他指向的是window，

两个题目里面的外层函数，因为调用的时候写法是 object.getNameFunc() ,所以是object调用的外部函数。

下面的一题，使用 var that = this; 使得此时的 that 记录了this—>谁调用了外层函数 getNameFunc ，即为object2，

# 对象高级

## 对象创建模式

### 方式一：Object构造函数

![image-20220401114558518](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220401114558518.png)



### 方式二：对象字面量

![image-20220401114613958](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220401114613958.png)



### 方式三：工厂模式

![image-20220401114620907](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220401114620907.png)

![image-20220401114916496](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220401114916496.png)



### 方式四：自定义构造函数

为了解决工厂模式对象没有一个具体的类型，**都是Object类型**。

自定义构造函数可以创建**多个类型**的对象，比如Student,Person。

> 注意：构造函数与普通函数不同，要用new去创建对象

![image-20220401114626678](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220401114626678.png)



![image-20220401115403788](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220401115403788.png)

**这里的属性age和name合理，但是setName方法是完全相同的，但是每个都处于不同的对象中，完全可以聚合地放在__ proto __ 中，从而继承调用**



### 方式五：构造函数+原型的组合

**将属性放在构造函数中，将方法放在原型中，使得方法能够复用，而不是分别创建完全相同的方法，减少内存占用**

![image-20220401115141357](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220401115141357.png)



## 原型链继承

**==A.B==**

==A为对象——沿着作用域链往上找。==

==找到A以后，确保A是一个对象，接着去对象中找对应的属性B==

==B（对象的属性）方法——沿着A对象所在的原型链往上找==

==找不到就返回undefined==



> 如果没有定义全局变量a：
>
> 然后去找 **window.a** ——返回undefined
>
> 如果直接去找 **a** ——报错
>
> 虽然有时候 直接写 a 就相当于 window.a 但是有细小区别，就看找不到之后，它如何处理 

![image-20220401125732687](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220401125732687.png)

![image-20220401130151612](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220401130151612.png)![image-20220401145104524](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220401145104524.png)





**画图理解**

![QQ图片20220401140053](C:\Users\051129\Desktop\前端图\QQ图片20220401140053.jpg)

![前端稿图-12](C:\Users\051129\Desktop\前端图\前端稿图-12.jpg)

![前端稿图13](C:\Users\051129\Desktop\前端图\前端稿图13.jpg)

## 继承模式

### 原型链继承

![image-20220401151526196](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220401151526196.png)

![image-20220401151532892](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220401151532892.png)

![image-20220401151538231](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220401151538231.png)

### 借用构造函数继承

![image-20220401151112831](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220401151112831.png)

### 组合继承

将属性放在构造函数中，将方法放在原型中，

![image-20220401151305694](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220401151305694.png)

![image-20220401151227133](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220401151227133.png)

**组合的总结：**

![image-20220401162357261](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220401162357261.png)





## 浏览器内核

![image-20220401170848371](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220401170848371.png)
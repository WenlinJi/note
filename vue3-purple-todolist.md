# 练习

## 练习一【todo-app】

> https://www.bilibili.com/video/BV1wy4y1k7Lr?p=2&spm_id_from=pageDriver

### 安装最新版的vue-cli【不需要每次都执行】

```
npm install -g @vue/cli
```

### 创建一个vue项目

```
vue create todo-app
```

这里选择创建一个vue3项目

### 打开图形化管理界面

```
vue ui
```

- 插件
- 依赖
- 配置
- 启动或者构建项目等

图形化界面也可以开启项目，但是较为麻烦，还是采取下面的命令行操作

### 运行项目

```
cd todo-app
```

```
yarn serve 或者 npm serve
```





### 关闭语法检查

在vue.config.js中：

```
//关闭eslint
lintOnSave: false
```



### HTML设计

![image-20220505171653231](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220505171653231.png)



### 拆分静态组件

![image-20220505212109750](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220505212109750.png)





### 处理事件和数据

- vue2和vue3

![image-20220505213703679](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220505213703679.png)



![image-20220505214042056](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220505214042056.png)

![image-20220505214114638](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220505214114638.png)

![image-20220505214123913](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220505214123913.png)







vue3统一在setup(){}写：

**用ref和reactive包装后的数据就可以在修改之后引起组件的刷新，**

- ref: 适合包装基础类型的或者简单类型的数据

- reactive: 包装复杂的对象数据

  

---

==**App.vue :**==

用ref包装一个空的数组，作为默认的todo列表的数据

```
const todos = ref([]);
```

定义一个添加todo的函数，通过事件接收一个todo参数，保存了todo的信息，然后把他追加到todo列表中

```
const addTodo = (todo)=> todos.value.push(todo)
```



**为了在`template`中使用数据和函数，我们需要在`setup()`中以对象的形式返回它们**



使用ref包装的数据，需要访问.value属性才能得到数据`const addTodo = (todo)=> todos.value.push(todo)`，

但是在template标签中，vue会自动拆解出value属性，所以直接把setup中返回的todos使用`:todos="todos"`把todo列表传递给todo-list组件



然后通过@add-todo监听todo-add组件的事件，使用addTodo这个函数处理事件

给todo-add组件传递一个tid属性，用于生成新的todo的ID





==**TodoAdd.vue :**==

给输入框双向绑定一个属性todoContent : 用于同步用户输入的todo内容

```
v-model= "todoContent"

const todoContent = ref("")
```

给按钮和回车键添加事件处理

```
@keyup.enter = "emitAddTodo"
```





### 抽离composables

![image-20220506083935859](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220506083935859.png)

![image-20220506084313927](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220506084313927.png)



![image-20220506161459888](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220506161459888.png)

### CSS知识点：

#### min-height: 100vh;

/* 使得不仅是当前的页面撑满整个高度，即使是继续往下添加清单项超出屏幕，背景也是会填充 */



#### 网格布局【display:grid】中 justify-items 和 align-litems

https://blog.csdn.net/u013565133/article/details/102919041



#### box-shadow详解

https://blog.csdn.net/qq_47443027/article/details/116042399



#### padding简写顺序

```
padding-top:20px;上内边距
padding-right:30px;右内边距
padding-bottom:30px;下内边距
padding-left:20px;左内边距

padding:1px                        四边统一内边距
padding:1px1px                  上下,左右内边距
padding:1px1px1px            上,左右,下内边距
padding:1px1px1px1px      上,右,下,左内边距
```



### vue相关

#### 数据绑定

![image-20220506131707036](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220506131707036.png)
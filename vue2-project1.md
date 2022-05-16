# 尚硅谷—Vue项目实战

> ==**尚品汇项目笔记：https://blog.csdn.net/weixin_43424325/article/details/121684101**==

## 项目开发准备工作

### 使用Vue CLI 3(脚手架)搭建项目

\1)    Vue CLI是vue官方提供的用于搭建基于vue+webpack+es6项目的脚手架工具

\2)    在线文档: [https://cli.vuejs.org/zh/](https://github.com/vuejs/vue-cli)

\3)    操作:

> **#** **使用vue-cli3**
>
> npm install -g @vue/cli
>
> vue create shop-client
>
> cd shop-client
>
> npm run serve
>
> **#** **降级到vue-cli2**
>
> npm install -g @vue/cli-init
>
> vue init webpack gshop-client2
>
> cd shop-client
>
> npm run dev



### 编码测试与打包发布项目

\1)    编码测试

```
npm run serve 
```

访问: http://localhost:8080

编码, 自动编译打包(HMR), 查看效果

\2)    打包发布

```
npm run build

npm install -g serve

serve dist -p 5000
```

访问: [http://localhost:5000](http://localhost:9000)



------



## 项目目录设计💙💙

```
# 入口文件 —— main.js

import Vue from 'vue'
import App from './App.vue'
import router from './router'

Vue.config.productionTip = false

new Vue({
  render: h => h(App),  // 把根组件挂载到挂载点上
  router, // 注册路由器
}).$mount('#app')
```

shop-client
	   |-- node_modules 【项目依赖文件夹】
	   |-- public【一般放置一些静态资源（图片），需要注意，放在public文件夹中的静态资源，webpack进行打包的时候会原封不动的打包到dist文件夹中】
            |-- **index.html:  主页面文件**（是一个模板文件，作用是生成项目的入口文件，webpack打包的js,css也会自动注入到该页面中。我们浏览器访问项目的时候就会默认打开生成好的index.html。）
       |-- src【程序员源代码文件夹】
            |-- api :  ajax相关请求

​				 |-- request.js  封装axios（配置请求拦截器，响应拦截器）

​				 |-- index.js  请求接口统一封装（**将每个请求封装为一个函数，并暴露出去，组件只需要调用相应函数即可，这样当我们的接口比较多时，如果需要修改只需要修改该文件即可。**，使用请求的时候，在main.js导入相关函数）

​			|-- ==assets==：（一般放多个组件公用的静态资源，需要注意，放置在assets文件夹中的静态资源，webpack进行打包的时候会把静态资源当作一个模板，打包在JS文件里面 ）

​            |-- ==components== :  非路由组件(全局组件)
​                  |-- Header/index.vue --放在App.vue中的<Header/>
​                  |-- Footer/index.vue --放在App.vue中的<Footer/>

​            |-- mock : 模拟数据

​            |-- ==pages== ：路由组件--放在App.vue中的<router-view></router-view>
​                  |-- Home/index.vue
​                  |-- Search/index.vue
​                  |-- Register/index.vue
​                  |-- Login/index.vue

​			|-- plugins：

​            |-- router：路由器
​                  |-- routes.js     所有静态路由配置的数组
​                  |-- index.js     声明使用插件,向外默认暴露路由器对象

​            |-- store：vuex相关

​            |-- utils：工具函数模块

​            |-- **App.vue：应用组件**【唯一的根组件，存放Vue当中的组件（.vue），然后全部放到**index.html**中】

​            |-- **main.js: 应用入口js**【程序入口文件，也是整个程序中最先执行的文件】

​       |-- .gitignore: 【git版本管制忽略的配置】

​       |-- babel.config.js: 【配置文件（babel相关）：翻译官—可以把ES6翻译为ES5语法，兼容性更好】

​       |-- jsconfig.json：【文件指定根目录和JavaScript服务提供的功能选项。如果不使用JavaScript，就不需要配置jsconfig.json】

​       |-- package.json: 应用包配置文件 【 项目的详细信息记录，认为是项目的’身份证‘。记录项目叫做什么，项目当中有哪些依赖**（安装完依赖之后，最好及时去检查是否安装成功）**，项目怎么运行】

​	   |-- package-lock.json:  【缓存性文件（各种包的来源）】

​       |-- README.md: 【应用描述说明的readme文件】

​       |-- vue.config.js: 【vue的配置文件，例如：proxy为通过代理解决跨域问题】



## 项目的其他配置



1. 项目运行起来的时候，让浏览器自动打开

   ```js
   package.json
       "scripts": {
       "serve": "vue-cli-service serve --open",
       "build": "vue-cli-service build",
       "lint": "vue-cli-service lint"
       },
   ```

   - **IDEA使用vue-cli-service serve --open命令打开vue项目出现http://0.0.0.0:8080/无法打开**

     > https://blog.csdn.net/tang__yuan/article/details/123600253【直接找到这个目录去修改】
     >
     > ![在这里插入图片描述](https://img-blog.csdnimg.cn/bcfb0abf7c5247c0b0cc95caf04ef3b1.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAdGFuZ19feXVhbg==,size_20,color_FFFFFF,t_70,g_se,x_16)

2. eslint校验功能关闭（不关闭会有各种规范，不按照规范就会报错）

   - 根目录下创建vue.config.js,进行配置

   ```js
   module.exports = {
     //关闭eslint
     lintOnSave: false
     }
   ```

   

3. src文件夹简写方法，jsconfig.json配置别名@提示

   创建jsconfig.json，用@/代替src/，exclude表示不可以使用该别名的文件

   ```js
    {
       "compilerOptions": {
           "baseUrl": "./",
               "paths": {
               "@/*": [
                   "src/*"
               ]
           }
       },
   
       "exclude": [
           "node_modules",
           "dist"
       ]
    }
   
   ```

   


## 项目的路由分析

（区分路由组件pages 和 非路由组件components）





## 完成非路由组件Header和Footer创建的业务

###  开发一个前端模块可以概括为以下几个步骤：

  （1）写静态页面、拆分为静态组件；

  （2）发请求（API）；

  （3）vuex（actions、mutations、state三连操作）；

  （4）组件获取仓库数据，动态展示；



###   注意一：

创建组件的时候，组件结构 + 组件样式 + 图片资源

###   注意二：

项目采用less样式，浏览器不支持，需要安装【尝试安装的是六版本】，把less样式变成css样式，浏览器才能识别。组件页面样式

组件页面的样式使用的是less样式，浏览器不识别该样式，需要下载相关依赖
 `npm install --save less less-loader@56
 如果想让组件识别less样式，则在组件中设置
 `<script scoped lang="less">`

###   注意三：

vue是单页面开发，我们只需要修改public下的index.html文件，目的是清除vue页面默认的样式

```
<link rel="stylesheet" href="reset.css">
```



## pages文件夹

创建pages文件夹，并创建路由组件

### 配置路由

创建router文件夹，并创建index.js进行路由配置，最终在main.js中引入注册

###  总结

路由组件和非路由组件区别：

- 非路由组件放在components中，路由组件放在pages或views中
- 非路由组件通过标签使用，路由组件通过路由使用
- 在main.js注册玩路由，所有的路由和非路由组件身上都会拥有$router $route属性
- $router：一般进行编程式导航进行路由跳转（push,replace等）
  $
- route： 一般获取路由信息（name path params等）



### 路由跳转方式

- 声明式导航router-link标签==（务必要有to属性）== ,可以把router-link理解为一个a标签，它 也可以加class修饰
- 编程式导航 ：声明式导航能做的编程式都能做，而且还可以处理一些业务



## 路由元信息的使用

### footer组件显示与隐藏：

- footer在登录注册页面是不存在的，所以要隐藏，v-if 或者 v-show
- 这里使用v-show，因为v-if会频繁的操作dom元素消耗性能，v-show只是通过样式将元素显示或隐藏
-  配置路由的时候，可以给路由配置元信息meta,
-  在路由的原信息中定义show属性，用来给v-show赋值，判断是否显示footer组件



## 路由传参

### 路由跳转有几种方式？

- 声明式导航：router-link标签==（务必要有to属性）== ,可以把router-link理解为一个a标签，它 也可以加class修饰

  > ![image-20220425181018009](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220425181018009.png)

- 编程式导航 ：利用的是组件实例的$router.push/replace方法，可以实现路由的跳转。声明式导航能做的编程式都能做，而且还可以处理一些业务

  > ![image-20220425180849293](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220425180849293.png)
  >
  > ![image-20220425180920069](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220425180920069.png)



### 路由传参：参数有几种写法？

- params参数：属于路径当中的一部分，需要注意，在配置路由的时候，需要**占位** ,地址栏表现为 /search/v1/v2
  - params参数对应的路由信息要修改为==`path: "/search/:keyword"`== 这里的/:keyword就是一个params参数的**占位符**

- query参数：不属于路径当中的一部分（类似于get请求），类似于ajax中的queryString  地址栏表现为/search?k1=v1&k2=v2 ,不需要占位
  - query参数对应的路由信息 ==`path: "/search"`==



**以下是采用编程式导航，传递参数 的实例：**

![image-20220425183337989](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220425183337989.png)

![image-20220425185042491](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220425185042491.png)

![image-20220425183521702](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220425183521702.png)

```js
 methods: {
      goSearch () {
        // 路由传递参数：
        // 第一种：字符串形式（先要在search处占位）
        // this.$router.push('/search/' + this.keyword + '?k=' + this.keyword.toUpperCase())
        // 第二种：模板字符串（先要在search处占位）
        // this.$router.push(`/search/${this.keyword}?k=${this.keyword.toUpperCase()}`)
        // 第三种【常用】：对象(先要给路由起一个名字)
        this.$router.push({name:"search",params:{keyword:this.keyword},query:{k:this.keyword.toUpperCase()}})
          
        // 不能直接使用path,下面的面试题有说
        //  this.$router.push({path:"/search",params:{keyword:this.keyword},query:{k:this.keyword.toUpperCase()}})
      }
    }
```

#### 总结：传参方法

- 字符串形式
  this.$router.push("/search/"+this.params传参+"?k="+this.query传参)

- 模板字符串

  this.$router.push(``/search/+{this.params传参}?k=${this.query传参}` `)
  注意： 上面字符串的传参方法可以看出params参数和’/'结合，query参数和？结合
  http://localhost:8080/#/search/asd?keyword=asd上面url中asd为params的值，keyword=asd为query传递的值。

- 对象（常用）
   this.$router.push({name:“路由名字”,params:{传参},query:{传参})。
   以对象方式传参时，如果我们传参中使用了params，只能使用name，不能使用path，如果只是使用query传参，可以使用path 。



### params传参问题

> 视频点：https://www.bilibili.com/video/BV1Vf4y1T7bw?p=9【面试题】

**路由传参相关的面试题：**

（1）路由传递参数（对象写法）path是否可以结合params参数一起使用？

​		答：路由跳转传参的时候，对象的写法可以是name,path 形式，但是需要注意的是，path这种写法不能与params参数一起使用

```
 path: "/search/:keyword",   //  Search路由项的path已经指定要传一个keyword的params参数
 
this.$router.push({path:"/search",params:{keyword:this.keyword},query:{k:this.keyword.toUpperCase()}})

地址栏输出：【http://localhost:8080/home?k=222】
出现错误，search已经不显示了。


如果使用his.$router.push({name:"search",params:{keyword:this.keyword},query:{k:this.keyword.toUpperCase()}})
结果为正确的：【http://localhost:8080/search/222?keyword=222】
```



（2）、如何指定params参数可传可不传

  如果路由path要求传递params参数,但是没有传递,会发现地址栏URL有问题，详情如下：
  Search路由项的path已经指定要传一个keyword的params参数，如下所示：
  path: "/search/:keyword",
  执行下面进行路由跳转的代码：
  this.$router.push({name:"Search",query:{keyword:this.keyword}})
  当前跳转代码没有传递params参数
  地址栏信息：http://localhost:8080/#/?keyword=asd
  此时的地址信息少了/search
  正常的地址栏信息: http://localhost:8080/#/search?keyword=asd
  解决方法：可以通过改变path来指定params参数可传可不传 
  path: "/search/:keyword?",?表示该参数可传可不传



> 参考连接：https://blog.csdn.net/weixin_44867717/article/details/109773945



（3）由（2）可知params可传可不传，但是如果传递的时空串，如何解决 。

```
 this.$router.push({name:"Search",query:{keyword:this.keyword},params:{keyword:''}})
 出现的问题和1中的问题相同,地址信息少了/search
 解决方法： 加入||undefined，当我们传递的参数为空串时地址栏url也可以保持正常
 this.$router.push({name:"Search",query:{keyword:this.keyword},params:{keyword:''||undefined}})

```

（4） 路由组件能不能传递props数据？
 可以，但是只能传递params参数,具体知识为props属性 。



## ==多次执行相同的push问题==

多次执行相同的push问题，控制台会出现警告
例如：使用this.$router.push({name:‘Search’,params:{keyword:"…"||undefined}})时，如果多次执行相同的push，控制台会出现警告。



```
let result = this.$router.push({name:"Search",query:{keyword:this.keyword}})
console.log(result)
```

执行一次上面代码：

![在这里插入图片描述](https://img-blog.csdnimg.cn/d7b3e04b2986474d8009fe970b7b2e63.png)

多次执行出现警告：

![在这里插入图片描述](https://img-blog.csdnimg.cn/308f41adccfe4268a6a2e0b4b2d2cfd0.png)

原因：push是一个promise，promise需要传递成功和失败两个参数，我们的push中没有传递。
方法：this.$router.push({name:‘Search’,params:{keyword:"…"||undefined}},()=>{},()=>{})后面两项分别代表执行成功和失败的回调函数。
这种写法治标不治本，将来在别的组件中push|replace,编程式导航还是会有类似错误
push是VueRouter.prototype的一个方法，在router中的index重写该方法即可(看不懂也没关系，这是前端面试题)

```
//1、先把VueRouter原型对象的push，保存一份
let originPush = VueRouter.prototype.push;
//2、重写push|replace
//第一个参数：告诉原来的push，跳转的目标位置和传递了哪些参数
VueRouter.prototype.push = function (location,resolve,reject){
    if(resolve && reject){
        originPush.call(this,location,resolve,reject)
    }else{
        originPush.call(this,location,() => {},() => {})
    }
}

```



## 定义全局组件

我们的三级联动组件是全局组件，全局的配置都需要在main.js中配置

```
//将三级联动组件注册为全局组件
import TypeNav from '@/pages/Home/TypeNav';
//第一个参数：全局组件名字，第二个参数：全局组件
Vue.component(TypeNav.name,TypeNav);

```

在Home组件中使用该全局组件

```js
<template>
<div>
<!--  三级联动全局组件已经注册为全局组件，因此不需要引入-->
  <TypeNav/>
</div>
</template>
```



---

---



## ==postman测试接口是否可用==

```
http://39.98.123.211/api/product/getBaseCategoryList
```



## 封装axios

> **axios中文文档，包含详细信息。**
> **https://www.kancloud.cn/yunye/axios/234845**

### 为什么需要二次封装axios?

- 请求拦截器：可以在发送请求之前处理一些业务，
- 响应拦截器：当服务器数据返回以后，可以处理一些事情

### 安装axios

```
cnpm install --save axios
```

安装完成后去package.json下面看是否安装成功

![image-20220425220605296](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220425220605296.png)



### 在项目中经常用api文件夹【axios】


 在根目录下创建api文件夹，创建request.js文件。
 内容如下，当前文件代码还比较少，后续有需求可以增添内容。

```js
import axios from "axios";

//1、对axios二次封装
// 利用axios对象的方法create，去创建一个axios实例
// requests 就是axios ，只不过稍微配置一下
const requests = axios.create({
    //基础路径，发请求的时候，路径当中会出现api。requests发出的请求在端口号后面会更改baseURl
    baseURL:'/api',
    // 代表请求超时时间5s
    timeout: 5000,
})

//2、配置请求拦截器(interceptors.request)
// 在发请求之前，请求拦截器可以检测到，可以在请求发出去之前做一些事情
requests.interceptors.request.use((config) => {
    //config内主要是对请求头Header配置
    //比如添加token
    return config;
})

//3、配置响应拦截器(interceptors.response)
//（成功和失败的回调）requests.interceptors.response.use(( ) => { },( ) => { })
requests.interceptors.response.use((res) => {
    //成功的回调函数:服务器响应数据回来以后，响应拦截器可以检测到，
    return  res.data;
},(error) => {
    //失败的回调函数
    console.log("响应失败"+error)
    // 终止promise链
    return Promise.reject(new Error('fail'))
})

//4、对外暴露
export default requests;

```



## 前端通过代理解决跨域问题

![image-20220425223711418](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220425223711418.png)

在根目录下的vue.config.js中配置,proxy为通过代理解决跨域问题。
我们在封装axios的时候已经设置了baseURL为api,所以所有的请求都会携带/api，这里我们就将/api进行了转换。如果你的项目没有封装axios，或者没有配置baseURL，建议进行配置。要保证baseURL和这里的代理映射相同，此处都为’/api’。

```js
module.exports = {
    //关闭eslint
    lintOnSave: false,
    devServer: {
        // true 则热更新，false 则手动刷新，默认值为 true
        inline: false,
        // development server port 8000
        // port: 8001,
        //代理服务器解决跨域
        proxy: {
            //会把请求路径中的/api换为后面的代理服务器
            '/api': {
                //提供数据的服务器地址
                target: 'http://39.98.123.211',

            }
        },
    }
}
```

[webpack官网相关知识解读](https://webpack.docschina.org/configuration/dev-server/#devserverproxy)
 网站中的webpack.config.js就是vue.config.js文件。



## ==请求接口统一封装（1.16也用到）==

在文件夹api中创建index.js文件，用于封装所有请求
 **将每个请求封装为一个函数，并暴露出去，组件只需要调用相应函数即可，这样当我们的接口比较多时，如果需要修改只需要修改该文件即可。**

如下所示：

```js
api/index.js里面

//当前模块，API进行统一管理，即对请求接口统一管理
import requests from "@/api/request";

//首页三级分类接口
export const reqCateGoryList = () => {
    return  requests({
        url: '/product/getBaseCategoryList',
        method: 'GET'
    })
}
```

当组件想要使用相关请求时，只需要导入相关函数即可，以上图的reqCateGoryList 为例:

```js
main.js里面

import {reqCateGoryList} from '@/api'
//发起请求
reqCateGoryList();
```





## nprogress进度条插件

打开一个页面时，往往会伴随一些请求，并且会在页面上方出现进度条。它的原理时，在我们发起请求的时候开启进度条，在请求成功后关闭进度条，所以只需要在request.js中进行配置。
 如下图所示，我们页面加载时发起了一个请求，此时页面上方出现蓝色进度条
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/f0df5bccfaee4274b45755b52bf40b60.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5q-b5q-b6Jmr5ZGc5ZGc,size_20,color_FFFFFF,t_70,g_se,x_16)



---



安装

```
cnpm install --save nprogress
```

引入（在响应拦截器处使用）使用之前要先引用

```js
import axios from "axios";

//引入进度条
import nprogress from 'nprogress';
// start:进度条开始   done:进度条结束
//引入进度条样式
import "nprogress/nprogress.css";


//1、对axios二次封装
// 利用axios对象的方法create，去创建一个axios实例
// requests 就是axios ，只不过稍微配置一下
const requests = axios.create({
    //基础路径，发请求是时候，路径当中会出现api。requests发出的请求在端口号后面会更改baseURl
    baseURL:'/api',
    // 代表请求超时时间5s
    timeout: 5000,
})

//2、配置请求拦截器(interceptors.request)
// 在发请求之前，请求拦截器可以检测到，可以在请求发出去之前做一些事情
requests.interceptors.request.use((config) => {
    //config：内主要是对请求头Header配置
    //比如添加token

    //开启进度条，进度条开始动
    nprogress.start();

    return config;
})

//3、配置响应拦截器(interceptors.response)
//（成功和失败的回调）requests.interceptors.response.use(( ) => { },( ) => { })
requests.interceptors.response.use((res) => {
    //成功的回调函数:服务器响应数据回来以后，响应拦截器可以检测到，

    //进度条结束
    nprogress.done();

    return  res.data;
},(error) => {
    //失败的回调函数
    console.log("响应失败"+error)
    // 终止promise链
    return Promise.reject(new Error('fail'))
})

//4、对外暴露
export default requests;

```

可以通过修改nprogress.css文件的background来修改进度条颜色。

![在这里插入图片描述](https://img-blog.csdnimg.cn/e66d5f5d851a4839810c34ad234f7c0a.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5q-b5q-b6Jmr5ZGc5ZGc,size_11,color_FFFFFF,t_70,g_se,x_16)





## ==手动引入vuex==

vuex是官方提供的一个插件，状态管理库。集中式管理项目中组件共用的数据。（ 并不是全部的项目都需要vuex，如果项目小，不需要使用；适用于项目大，数据多，组件多。数据维护困难的情况）

![image-20220426130536583](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220426130536583.png)



- modules
  - state   仓库存储数据的地方
  - mutations   修改state的唯一手段
  - actions   处理action,可以书写自己的业务逻辑，也可以处理异步
  - getters   理解为计算属性，用于简化仓库数据，让组件获取仓库的数据更加方便

---

> 视频源：https://www.bilibili.com/video/BV1Vf4y1T7bw?p=18

(类似 router 过程)

### 安装vuex

```
cnpm install --save vuex@3
```

### 首先在 package.json 中确保安装了vuex, 然后在根目录创建store文件夹，文件夹下创建index.js，内容如下：

```js
import Vue from 'vue'
import Vuex from 'vuex'

// 需要使用插件一次
Vue.use(Vuex)
// - state   仓库存储数据的地方
const state = {}
// - mutations   修改state的唯一手段
const mutations = {}
// - actions   处理action,可以书写自己的业务逻辑，也可以处理异步
const actions = {}
// - getters   理解为计算属性，用于简化仓库数据，让组件获取仓库的数据更加方便
const getters = {}

//对外暴露store的一个实例
export default new Vuex.Store({
    state,
    mutations,
    actions,
    getters
})

```

或者使用下面的这种（不推荐）

```js
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

//对外暴露store的一个实例
export default new Vuex.Store({
    state:{},
    mutations:{},
    actions:{},
    
})
```

### 如果想要使用vuex，还要再main.js中引入

 main.js:
 (1) 引入文件    import store from '@/store'
 (2) 注册store   store

 **但凡是在main.js中的Vue实例中注册的实体，在所有的组件中都会有（this.$.实体名）属性**

```js
import store from '@/store'
new Vue({
  render: h => h(App),
  //注册路由，此时组件中都会拥有$router $route属性
  router,
  //注册store,此时组件中都会拥有$store
  store
}).$mount('#app')
```



> 类似的是 router:
>
> 如果想要使用router，还要再main.js中引入
>  main.js:
>  (1) 引入文件    import router from '@/router'
>  (2) 注册store   router
>
> ```js
> // 应用入口js【程序入口文件，也是整个程序中最先执行的文件】
> import Vue from 'vue'
> import App from './App.vue'
> 
> // 引入注册的路由
> import router from '@/router'   
> 
> new Vue({
>   // el:'#app'
>   render: h => h(App),
>   // 注册路由器
>   // 注册路由信息：当这里书写router的时候，组件身上都拥有$route,$router属性
>   router ,
> }).$mount('#app')
> ```
>
> 







### **大仓库分模块开发——小仓库：**

在store下面分别建立多个小仓库文件夹(例如：home)：（小文件夹home下面建立index.js）存放以下代码：

```js
// - state   仓库存储数据的地方
const state = {}
// - mutations   修改state的唯一手段
const mutations = {}
// - actions   处理action,可以书写自己的业务逻辑，也可以处理异步
const actions = {}
// - getters   理解为计算属性，用于简化仓库数据，让组件获取仓库的数据更加方便
const getters = {}

//对外暴露store的一个实例
export default{
    state,
    mutations,
    actions,
    getters
}
```



store下面的主 index.js 中内容如下：

```js
import Vue from 'vue'
import Vuex from 'vuex'
// 需要使用插件一次
Vue.use(Vuex)

// 引入小仓库
import home from './home'

//对外暴露store的一个实例
export default new Vuex.Store({
	//实现Vuex仓库模块化开发存储数据
	modules:{
		home
	}
})
```



## async await使用（1.18的前置知识）

如果我们没有封装请求api，而是直接调用axios，就不需要使用async await。
 案例：我们将一个axios请求封装为了函数，我们在下面代码中调用了该函数：

```js
import {reqCateGoryList} from '@/api'
export default {
    actions:{
        categoryList(){
            let result =  reqCateGoryList()
            console.log(result)
        }
    }
}
```

浏览器结果

![在这里插入图片描述](https://img-blog.csdnimg.cn/d2ba586e3edd494b9bf517cb4ee86580.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5q-b5q-b6Jmr5ZGc5ZGc,size_20,color_FFFFFF,t_70,g_se,x_16)

返回了一个promise,证明这是一个promise请求，但是我们想要的是图片中的data数据。
 没有将函数封装前我们都会通过then()回调函数拿到服务器返回的数据，现在我们将其封装了，依然可以使用then获取数据，代码如下

```js
actions:{
        categoryList(){
            let result =  reqCateGoryList().then(
                res=>{
                console.log("res")
                console.log(res)
                return res
                }
            )
            console.log("result")
            console.log(result)
        }
    }

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/ccf35a9aa6c442c7a799e474c0293afa.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5q-b5q-b6Jmr5ZGc5ZGc,size_15,color_FFFFFF,t_70,g_se,x_16)

由于我们的promise是异步请求，我们发现请求需要花费时间，但是它是异步的，所有后面的console.log(“result”)；console.log(result)会先执行，等我们的请求得到响应后，才执行console.log(“res”)；console.log(res)，这也符合异步的原则，但是我们如果在请求下面啊执行的是将那个请求的结果赋值给某个变量，这样就会导致被赋值的变量先执行，并且赋值为undefine，因为此时promise还没有完成。

![在这里插入图片描述](https://img-blog.csdnimg.cn/afe1c716352248009e7289151e933391.png)

所以我们引入了async await,async写在函数名前，await卸载api函数前面。await含义是async标识的函数体内的并且在await标识代码后面的代码先等待await标识的异步请求执行完，再执行。这也使得只有reqCateGoryList执行完，result 得到返回值后，才会执行后面的输出操作。

```js
   async categoryList(){
            let result = await reqCateGoryList()
            console.log("result")
            console.log(result)
        }

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/160a7e87520d494787915f3fe9fa4640.png)

![image-20220426171601692](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220426171601692.png)





## Vuex使用回顾💚💚💚

> vue实战笔记：https://blog.csdn.net/weixin_43424325/article/details/121684101

state、actions、mutations、getters的辅助函数使用，当多次访问store中的上述属性时，要使用各个属性的辅助函数，可以减少代码量。

**在使用上面的函数时，如果需要传递多个参数，需要把多个参数组合为一个对象传入(vuex是不允许多个参数分开传递的)**。

```js
src\store\home\index.js中

async addOrUpdateShopCart({commit},{skuId,skuNum}){
        let result = await reqAddOrUpdateShopCart(skuId,skuNum)
        console.log(result)
        if(result.data ===  200){

        }
```

[==**辅助函数官网链接**==](https://vuex.vuejs.org/zh/guide/state.html#在-vue-组件中获得-vuex-状态)
 ==**注意**：**使用action时，函数的第一个参数，必须是{commit}**，==即使不涉及到mutations操作，也必须加上该参数，否则会报错。



> 辅助，补充——**Vuex的回顾**（vue视频学习教程的配套笔记）：https://www.yuque.com/cessstudy/kak11d/dkrrce
>
> ![image-20220426190803108](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220426190803108.png)

- **\src\store\index.js**

  ![image-20220426171807448](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220426171807448.png)

- **\src\main.js**

  将store注入到vue实例对象中去，就不需要在每个获取vuex状态的组件中都引入 import store from 'store';

  ![image-20220426172136402](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220426172136402.png)

- **\src\components\TypeNav\index.vue**

  ![image-20220426170116183](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220426170116183.png)

- **\src\store\ ==home== \index.js**

  （Home是作为大仓库的一个模块，上面要先有大仓库的引用）

  categoryList 在第P30d 视频修改了名字：getCategoryList💥💥💥

  ![image-20220426171601692](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220426171601692.png)

  - **src\api\index.js(这是1.14的内容，还要完成1.12的axios二次封装，和1.13的跨域请求问题)**

    ![image-20220426172953026](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220426172953026.png)

  

- **\src\components\TypeNav\index.vue -- (关于三级联动如何显示)**

![image-20220426132539258](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220426132539258.png)



## 完成三级联动的动态背景颜色

![image-20220426184255150](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220426184255150.png)



## 防抖节流

在进行窗口的resize、scroll，输入框内容校验等操作时，如果事件处理函数调用的频率无限制，会加重浏览器的负担，导致用户体验非常糟糕。此时我们可以采用debounce（防抖）和throttle（节流）的方式来减少调用频率，同时又不影响实际效果。
安装lodash插件，该插件提供了防抖和节流的函数，我们可以引入js文件，直接调用。当然也可以自己写防抖和节流的函数
[lodash官网](https://www.lodashjs.com/)
 [防抖函数](https://www.lodashjs.com/docs/lodash.debounce)
 [节流函数](https://www.lodashjs.com/docs/lodash.throttle)

- 防抖：用户操作很频繁，但是只执行一次，减少业务负担。

- 节流：用户操作很频繁，但是把频繁的操作变为少量的操作，使浏览器有充分时间解析代码

[防抖和节流简述](https://www.jianshu.com/p/c8b86b09daf0)
例如：下面代码就是将changeIndex设置了节流，如果操作很频繁，限制50ms执行一次。这里函数定义采用的键值对形式。throttle的返回值就是一个函数，所以直接键值对赋值就可以，函数的参数在function中传入即可。

```js
三级联动快速滑过一级分类的时候，使用节流操作

import {throttle} from 'lodash'

 methods: {
    //鼠标进入修改响应元素的背景颜色
    //采用键值对形式创建函数，将changeIndex定义为节流函数，该函数触发很频繁时，设置50ms才会执行一次
    changeIndex: throttle(function (index){
      this.currentIndex = index
    },50),
    //鼠标移除触发时间
    leaveIndex(){
      this.currentIndex = -1
    }
  }

```

![image-20220426200752574](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220426200752574.png)



## 编程式导航+事件委托实现路由跳转

![img](https://img-blog.csdnimg.cn/5e9580e64f6f4b6c9f6f24837470d966.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5q-b5q-b6Jmr5ZGc5ZGc,size_20,color_FFFFFF,t_70,g_se,x_16)

如上图所示，三级标签列表有很多，每一个标签都是一个页面链接，我们要实现通过点击表现进行路由跳转。
 路由跳转的两种方法：导航式路由，编程式路由。

> 对于导航式路由，我们有多少个a标签就会生成多少个router-link标签，这样当我们频繁操作时会出现卡顿现象。
>  对于编程式路由，我们是通过触发点击事件实现路由跳转。同理有多少个a标签就会有多少个触发函数。虽然不会出现卡顿，但是也会影响性能。

上面两种方法无论采用哪一种，都会影响性能。我们提出一种：编程时导航+事件委派 的方式实现路由跳转。事件委派即把子节点的触发事件都委托给父节点。这样只需要一个回调函数goSearch就可以解决。

**事件委派问题：**
（1）如何确定我们点击的一定是a标签呢？如何保证我们只能通过点击a标签才跳转呢？
（2）如何获取子节点标签的商品名称和商品id**(我们是通过商品名称【categoryName】和商品id 【category1Id,category2Id,category3Id】进行页面跳转的)**



- 地址栏应该是对应下面的格式：

  ![image-20220426204231681](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220426204231681.png)

  ![image-20220426204227182](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220426204227182.png)

- 地址栏形式为：/search ? categoryName = xxxx & categoryXId = xxxx

- 按照这个样式：this.$router.push({name:"search",query:{categoryName:'xxxxx',categoryXId:'xxxx'}})

- 对应于dataset：this.$router.push({name:"search",query:{category**Name**:category**name**,categoryX**Id**:categoryX**id**}})

  -   html中会把 **自定义的:data-categoryName** 大写转为小写category**name**
  - 所以获取 category**Name **，就是 获取目前鼠标点击标签的categoryname,category1id,category2id,category3id，

  



**解决方法：**
对于问题1：为三个等级的**a标签添加自定义属性**date-categoryName绑定商品标签名称来标识a标签（其余的标签是没有该属性的）。

对于问题2：为三个等级的a标签再添加自定义属性data-category1Id、data-category2Id、data-category3Id来获取三个等级a标签的商品id，用于路由跳转。

==我们可以通过在函数中传入**event**参数，获取当前的点击事件，==

==通过**event.target**属性获取当前点击节点，==

```
 let element = event.target
```

==再通过**dataset**属性获取节点的属性信息。==

```
let {categoryname,category1id,category2id,category3id} = element.dataset
```



---



**在\src\components\TypeNav\index.vue 中编码：**

给a标签加上自定义的属性：

```js
 <div class="all-sort-list2" @click="goSearch" @mouseleave="leaveIndex">
          <div class="item"  v-for="(c1,index) in categoryList" v-show="index!==16" :key="c1.categoryId" :class="{cur:currentIndex===index}">
            <h3 @mouseenter="changeIndex(index)"  >
              <a :data-categoryName="c1.categoryName" :data-category1Id="c1.categoryId" >{{c1.categoryName}}</a>
            </h3>
            <div class="item-list clearfix" :style="{display:currentIndex===index?'block':'none'}">
              <div class="subitem" v-for="(c2,index) in c1.categoryChild" :key="c2.categoryId">
                <dl class="fore">
                  <dt>
                    <a :data-categoryName="c2.categoryName" :data-category2Id="c2.categoryId">{{c2.categoryName}}</a>
                  </dt>
                  <dd>
                    <em v-for="(c3,index) in c2.categoryChild"  :key="c3.categoryId">
                      <a :data-categoryName="c2.categoryName" :data-category3Id="c3.categoryId">{{c3.categoryName}}</a>
                    </em>
</dd></dl></div></div></div></div>

```

**注意：**event是系统属性，所以我们只需要在函数定义的时候作为参数传入，在函数使用的时候不需要传入该参数。

```js
//函数使用
<div class="all-sort-list2" @click="goSearch" @mouseleave="leaveIndex">
//函数定义
goSearch(event){
      console.log(event.target)
    }

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/4406011f40ab4b4db06e32974408ec1e.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5q-b5q-b6Jmr5ZGc5ZGc,size_12,color_FFFFFF,t_70,g_se,x_16)

对应的goSearrch函数:

```js
    // 编程式导航+事件委托实现路由跳转
    goSearch(event) {
      // 获取当前点击的节点 = 事件对象  因为：@click="goSearch(event)
      // event是系统属性，所以我们只需要在函数定义的时候作为参数传入，在函数使用的时候不需要传入该参数。
      let element = event.target;

      // html中会把大写转为小写
      // 获取目前鼠标点击标签的categoryname,category1id,category2id,category3id，
      // 通过四个属性是否存在来判断是否为a标签，以及属于哪一个等级的a标签
      // 节点有一个dataset属性，通过dataset属性获取节点的属性信息
      let { categoryname, category1id, category2id, category3id } = element.dataset;

      // 按照这个样式：this.$router.push({name:"search",query:{categoryName:'xxxxx',categoryXId:'xxxx'}})
      // 地址栏形式为：/search ? categoryName = xxxx & categoryXId = xxxx
      let location = { name: "search" };
      let query = { categoryName: categoryname };
      if (categoryname) {
        if (category1id) {
          //category1id一级a标签
          query.category1Id = category1id;
        } else if (category2id) {
          //category2id二级a标签
          query.category2Id = category2id;
        } else if (category3id) {
          //category3id三级a标签
          query.category3Id = category3id;
        }
      //整理完参数
      location.query = query;
      //路由跳转
        this.$router.push(location)
      }

    },
```

## ==阶段复习小结==

![image-20220426212934966](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220426212934966.png)

![image-20220426230656472](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220426230656472.png)

## Search模块中的商品分类和过渡动画

**\src\components\TypeNav\index.vue**

### 用一个响应式的属性控制（Home和Search两种不同的）三级联动的显示与隐藏

```js
<!-- 三级联动 -->
<div class="sort" v-show="show">
    <!-- show不写死，不直接写成false或者true，而是根据具体的情况来判断 -->
```

要在data()中定义一个响应式的值**show**

```js
export default {
  name: "TypeNav",
  data() {
    return {
      // 存储用户鼠标移上哪一个一级分类
      currentIndex: -1, //代表初始值没有停留在一级分类上
      show:true     // 初始默认三级分类是显示的
    };
  },
  
```

根据项目要求：

Home路由组件，默认显示typeNav；

如果不是Home路由组件，将typeNav进行隐藏

```js
  mounted() {
    // 通知vuex发送请求，获取数据，存储在仓库之中
    this.$store.dispatch("categoryList");
    // this.$store.dispatch("action中的方法名"，数据);

    // 如果不是Home路由组件，将typeNav进行隐藏
    if(this.$route.path != '/home'){
      this.show = false;
    }
  },
```

为什么放在mouted里面？

由于Vue在路由切换的时候会销毁旧路由，当我们再次使用三级列表全局组件时还会发一次请求。
**当我们在包含三级列表全局组件的不同组件之间进行切换时，都会进行一次信息请求。**



### 对于Search里面点击导航栏控制显示与隐藏（默认是隐藏）-[Home中不应该进行这个改变，一直显示]

```js
  methods: {

    //鼠标移除触发事件
    leaveIndex() {
      this.currentIndex = -1;
      // 如果不是Home路由组件，才会执行，Home不进行商品列表的显示与隐藏，一直显示
      if(this.$route.path != '/home'){
        // 当鼠标离开的时候，让Search商品分类列表进行隐藏(Home页面不隐藏)
        this.show = false
      }
    },

    enterShow(){
        // 当鼠标移入的时候，让Search商品分类列表进行显示(Home页面一直显示)
      this.show = true
    }
  },
```



### 过渡动画

**前提条件：**

==元素务必要有v-if/v-show指令才可以进行过渡动画==

![image-20220426224230574](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220426224230574.png)

```js
        <h2 class="all">全部商品分类</h2>
        
        <!-- 过渡动画 -->
        <transition name="sort">
          <div class="sort" v-show="show">
          </div>
        </transition>
```



```js
    // 过渡动画的样式
    // 因为上面的<transition name="sort"> ，所以使用.sort-enter ，而不是 v-enter
    // 过渡动画的开始状态（进入）
    .sort-enter{
      height: 0px;
    }
    // 过渡动画的结束状态（进入）
    .sort-enter-to{
      height: 461px;
    }
    // 定义动画的时间和速率
    .sort-enter-active{
      transition: all .5s linear;
    }
```



### 商品分类三级列表的优化

![image-20220426224804520](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220426224804520.png)

**Vue在路由切换的时候会销毁旧路由。**
我们在三级列表全局组件**TypeNav中的mounted进行了请求一次商品分类列表数据。**
由于Vue在路由切换的时候会销毁旧路由，当我们再次使用三级列表全局组件时还会发一次请求。
如下图所示：**当我们在包含三级列表全局组件的不同组件之间进行切换时，都会进行一次信息请求。**

#### **问题**💥💥💥💥💥💥

**\src\store\home\index.js 中：修改名称**

![image-20220426232453064](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220426232453064.png)

![image-20220426231254173](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220426231254173.png)

```js
  把\src\components\TypeNav\index.vue 中的信息请求放在 App.vue文件中
  
  mounted() {
    // 派发一个action 获取商品分类的三级列表的数据
      this.$store.dispatch("getCategoryList");
   
  },
```

【Home.vue和Search.vue都引用了TypeNav，所以每次会摧毁旧路由】

【App.vue是最先执行的，TypeNav放在App.vue的mounted中，后面的Home.vue和Search.vue都已经可以使用TypeNav，不会多次进行信息请求】

由于信息都是一样的，出于性能的考虑我们希望该数据只请求一次，所以我们把这次请求放在App.vue的mounted中。（根组件App.vue的mounted只会执行一次）
**注意：虽然main.js也是只执行一次，但是不可以放在main.js中。==因为只有组件的身上才会有$store属性。==**



![在这里插入图片描述](https://img-blog.csdnimg.cn/ea8ece30280d452b920c25ecbf1ed211.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5q-b5q-b6Jmr5ZGc5ZGc,size_20,color_FFFFFF,t_70,g_se,x_16)



## 合并参数

![image-20220427100309003](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220427100309003.png)

![image-20220427100925419](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220427100925419.png)







## Mock/模拟数据接口

把mock数据需要的图片放到public文件夹下面

![image-20220427140348482](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220427140348482.png)

###  下载依赖包

```
npm install -S mockjs
```

### mock插件的使用

mock用来拦截前端ajax请求，返回我么们自定义的数据用于测试前端接口。
 将不同的数据类型封装为不同的json文件，创建mockServer.js文件
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/8e20660af0b14a6396937a4fb10818f1.png)
 banner、floor分别为轮播图和页面底部的假数据。
 mockServer.js文件

```js
import Mock  from 'mockjs'
// 把JSON数据格式引入进来【json数据格式根本没有对外暴露，但是可以引入】
// 因为：webpack默认对外暴露：json、图片
import banner from './banner.json'
import floor from './floor.json'

// mock数据：第一个参数请求地址、第二个参：请求数据
Mock.mock("/mock/banner",{code:200,data:banner}) // 提供广告位轮播数据的接口
Mock.mock("/mock/floor",{code:200,data:floor}) // 提供所有楼层数据的接口

//记得要在main.js中引入一下
//import '@/mock/mockServer'

```







## 利用Mock接口实现动态的Home

### 获取Banner轮播图数据

![获取轮播图Banner数据](C:\Users\051129\Desktop\前端图\vue\获取轮播图Banner数据.png)



==第四个图需要添加下面的部分，才能使得<ListContainer>组件里面带入数据==（在组件中获取仓库中的数组）

![image-20220427200730439](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220427200730439.png)

![image-20220427180329763](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220427180329763.png)



### 使用swiper实现静态页面轮播

#### 下载依赖包:

(视频是这种)

```
cnpm install --save swiper@5
```

（配套笔记是这种）

```
npm install -S swiper
```



#### 第一步：引包（相应 JS / CSS ）

注意需要在main.js中进行全局注册

```
import 'swiper/css/swiper.min.css'  // 在入口js中引入
```

#### 第二步：页面结构务必要有

- 大轮播图

>   // 第一次书写首页大轮播图Swiper的时候:在mounted但总是书写是不可以的，因为但是挂载完毕并没有收到数据
>     // 第一次的大轮播图：是在当前组件内发请求，动态渲染结构【前台至少服务器数据需要回来】

- floor部分的小轮播图

>     /* 
>       floor这个组件：自己在组件内部是没有发请求的，数据是父组件给的，
>       所以做轮播图的时候，floor内部的mounted的时候已经有数据了，可以new Swiper
>       Home的index.vue 中 <Floor v-for="(floor,index) in floorList" :key="floor.id" :list="floor"></Floor>
>     */
>    // 因为：请求是父组件发的，父组件通过props传递过来，而且结构都已经有了的情况下才执行的mounted
>    // 所以这里不需要像第一次那样再使用 watch监视 以及 nextTick 回调

#### 第三步：new Swiper 实例【静态轮播图添加动态效果】

- P35——先是直接在mounted中创建new Swiper 实例，此时页面结构还没形成【使用定时器（大概设置一个等待时间，这会导致页面一开始没有轮播图的小圆点）勉强完成，让数据更新成功，形成页面结构后再new Swiper 实例】

- P36——（监听bannerList数据的变化，因为这条数据发生过变化————由空数组变为数组里面有四个元素）现在通过watch监听bannerList属性的属性值的变化。 

  **注意：**如果执行这个handler方法,代表组件实例身上这个属性的属性值已经有了【数组：四个元素】当前这个函数执行：只能保证bannerList数据已经有了，但是你没办法保证v-for已经执行结束了。【v-for执行完毕，才有结构，在watch当中没办法保证，所以要使用nextTick辅助完成】

- P36——**最后使用watch配合nextTick** 

  // nextTick：在下次DOM更新 ==循环结束之后==（v-for已经执行完毕）执行延迟回调。在 修改数据之后 立即使用这个方法，获取更新后的DOM【可以保证页面的结构一定是有的，经常和很多插件一起使用，因为有些插件是直接操作DOM元素的，需要DOM已经存在才能操作】

![image-20220428145549155](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220428145549155.png)



#### 获取ID不使用document, 换成ref

```js
 // document.querySelector(".swiper-container"),   // <div class="swiper-container" id="mySwiper">
 
 this.$refs.mySwiper,   // <div class="swiper-container" ref="mySwiper">
```





## 开发Floor组件

- 切记：仓库当中的state不能瞎写，数据格式取决于服务器返回的数据（floor是使用mock模拟出来的，mock---floor.json里面返回的格式是数组）

- getFloorList这个action在哪里使用dispatch触发，是需要在Home路由组件中触发的，不能在floor组件内触发action,因为：我们需要v-for遍历floor组件

- v-for也可以在自定义标签当中使用

  ```css
  // 路由组件——主页页面
  <template>
    <div>
      <!-- 使用三级联动的全局组件，需要注意，不需要再次引用，已经是全局组件 -->
      <TypeNav></TypeNav>
      <ListContainer></ListContainer>
      <TodayRecommend></TodayRecommend>
      <Rank></Rank>
      <Like></Like>
      <Floor v-for="(floor,index) in floorList" :key="floor.id"></Floor>
      <Brand></Brand>
    </div>
  </template>
  ```

- 组件通信的方式有哪些？==**面试频率极高**==

  props：用于父子组件通信

  自定义事件：@on,@emit可以实现子给父通信

  全局事件总线：$bus全能

  pubsub-js: vue当中几乎不用 全能

  插槽

  vuex

  

### 动态展示floor组件，把里面写死的内容换成动态接口获取的内容（这里是mock模拟的数据）

参考P38视频





## 封装swiper轮播图组件

将两个轮播图写成类似的结构，便于提取出组件





### 小轮播图的修改：\src\pages\Home\Floor\index.vue

> 本身可以直接使用mounted，但是为了和大轮播图抽离出相同的组件，也要使用监听器watch和nextTick

```vue
<template>
  <!--楼层-->
  <div class="floor">
    <div class="py-container">
      <div class="title clearfix">
        <h3 class="fl">{{list.name}}</h3>
        <div class="fr">
          <ul class="nav-tabs clearfix">
            <li class="active" v-for="(nav,index) in list.navList" :key="index">
              <a href="#tab1" data-toggle="tab">{{nav.text}}</a>
            </li>
          </ul>
        </div>
      </div>
      <div class="tab-content">
        <div class="tab-pane">
          <div class="floor-1">
            <div class="blockgary">
              <ul class="jd-list">
                <li v-for="(keyword,index) in list.keywords" :key="index">{{keyword}}</li>
              </ul>
              <img :src="list.imgUrl" />
            </div>
            <div class="floorBanner">
              <!-- 轮播图的地方 -->
              <div class="swiper-container" ref="cur">
                <div class="swiper-wrapper">
                  <div class="swiper-slide" v-for="(carousel,index) in list.carouselList" :key="carousel.id">
                    <img :src="carousel.imgUrl" />
                  </div>
                </div>
                <!-- 如果需要分页器 -->
                <div class="swiper-pagination"></div>

                <!-- 如果需要导航按钮 -->
                <div class="swiper-button-prev"></div>
                <div class="swiper-button-next"></div>
              </div>
            </div>
            <div class="split">
              <span class="floor-x-line"></span>
              <div class="floor-conver-pit">
                <img :src="list.recommendList[0]" />
              </div>
              <div class="floor-conver-pit">
                <img :src="list.recommendList[1]" />
              </div>
            </div>
            <div class="split center">
              <img :src="list.bigImg" />
            </div>
            <div class="split">
              <span class="floor-x-line"></span>
              <div class="floor-conver-pit">
                <img :src="list.recommendList[2]" />
              </div>
              <div class="floor-conver-pit">
                <img :src="list.recommendList[3]" />
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>


<script>
  // 引入swiper
  import Swiper from "swiper"
  export default {
  name: "",
  //  与props相搭配使用，实现父子间通信 ：<Floor v-for="(floor,index) in floorList" :key="floor.id" :list="floor"></Floor>
  props:['list'], 
  watch:{
    list:{
      // 为什么watch监听不到list：因为这个数据没有发生过变化，（数据是父亲给的，父亲给的时候是一个对象，对象里面该有的数据都有）
      // 所以要使用立即监听：不管你数据有没有变化，上来就立即监听一次
      immediate:true,
      handler(){
        // watch只能监听到数据已经有了，但是v-for动态渲染结构我们还是没有办法确定的，因此还是需要用nextTick
        this.$nextTick(()=>{
              // 第一次书写首页大轮播图Swiper的时候:在mounted但总是书写是不可以的，因为但是挂载完毕并没有收到数据
          // 第一次的大轮播图：是在当前组件内发请求，动态渲染结构【前台至少服务器数据需要回来】
          /* 
            floor这个组件：自己在组件内部是没有发请求的，数据是父组件给的，
            所以做轮播图的时候，floor内部的mounted的时候已经有数据了，可以new Swiper
            Home的index.vue 中 <Floor v-for="(floor,index) in floorList" :key="floor.id" :list="floor"></Floor>
          */
        // 因为：请求是父组件发的，父组件通过props传递过来，而且结构都已经有了的情况下才执行的mounted
        // 所以这里不需要像第一次那样再使用 watch监视 以及 nextTick 回调
          var mySwiper = new Swiper(
            // document.querySelector(".swiper-container"),   
            this.$refs.cur,   // <div class="swiper-container" ref="cur">
            {
              // direction: 'vertical', // 垂直切换选项   默认是水平轮播
              loop: true, // 循环模式

              // 分页器
              pagination: {
                el: ".swiper-pagination",
              },

              // 前进后退按钮
              navigation: {
                nextEl: ".swiper-button-next",
                prevEl: ".swiper-button-prev",
              },
            }
          );
        })
      }
    }
  }
  };
</script>


<style lang="less" scoped>
.floor {
  margin-top: 15px;

  .py-container {
    width: 1200px;
    margin: 0 auto;

    .title {
      .fl {
        float: left;
        color: #c81623;
        font-size: 20px;
        line-height: 30px;
        margin: 9px 0;
        font-weight: 700;
      }

      .fr {
        float: right;

        .nav-tabs {
          margin: 10px 0 0;
          display: inline-block;

          li {
            float: left;
            line-height: 18px;

            a {
              padding-top: 1px;
              font-weight: 400;
              background-color: #fff;

              &::after {
                content: "|";
                padding: 0 10px;
              }
            }

            &:nth-child(7) {
              a {
                &::after {
                  content: "";
                }
              }
            }

            &.active {
              a {
                color: #e1251b;
              }
            }
          }
        }
      }
    }

    .tab-content {
      border-top: 2px solid #c81623;
      border-bottom: 1px solid #e4e4e4;

      .tab-pane {
        .floor-1 {
          height: 360px;
          display: flex;

          .blockgary {
            width: 210px;
            height: 100%;
            background: #f7f7f7;

            .jd-list {
              padding: 15px 0;
              overflow: hidden;

              li {
                list-style-type: none;
                float: left;
                width: 40%;
                margin: 0 10px;
                border-bottom: 1px solid #e4e4e4;
                text-align: center;
                line-height: 26px;
              }
            }

            img {
              width: 100%;
            }
          }

          .floorBanner {
            width: 330px;
            height: 100%;
          }

          .split {
            width: 220px;
            height: 100%;
            position: relative;

            .floor-x-line {
              position: absolute;
              background: #e4e4e4;
              width: 220px;
              height: 1px;
              top: 180px;
            }

            .floor-conver-pit {
              width: 100%;
              height: 50%;

              img {
                width: 100%;
                height: 100%;
                transition: all 400ms;

                &:hover {
                  opacity: 0.8;
                }
              }
            }
          }

          .center {
            border: 1px solid #e4e4e4;
          }
        }
      }
    }
  }
}
</style>
```



### 大轮播图的修改\src\pages\Home\ListContainer\index.vue

> 几乎没有修改：只是设置一个立即监听：immediate:true,  —— 保证能够和上面的小轮播图有相似的结构



```vue
<template>
  <!--列表-->
  <div class="list-container">
    <div class="sortList clearfix">
      <div class="center">
        <!--banner轮播-->
        <div class="swiper-container" ref="mySwiper">
          <div class="swiper-wrapper">
            <!-- <div class="swiper-slide"> -->
            <div
              class="swiper-slide"
              v-for="(carousel, index) in bannerList"
              :key="carousel.id"
            >
              <!-- <img src="./images/banner1.jpg"/> -->
              <img :src="carousel.imgUrl" />
            </div>
          </div>
          <!-- 如果需要分页器 -->
          <div class="swiper-pagination"></div>

          <!-- 如果需要导航按钮 -->
          <div class="swiper-button-prev"></div>
          <div class="swiper-button-next"></div>
        </div>
      </div>
      <div class="right">
        <div class="news">
          <h4>
            <em class="fl">尚品汇快报</em>
            <span class="fr tip">更多 ></span>
          </h4>
          <div class="clearix"></div>
          <ul class="news-list unstyled">
            <li><span class="bold">[特惠]</span>备战开学季 全民半价购数码</li>
            <li><span class="bold">[公告]</span>备战开学季 全民半价购数码</li>
            <li><span class="bold">[特惠]</span>备战开学季 全民半价购数码</li>
            <li><span class="bold">[公告]</span>备战开学季 全民半价购数码</li>
            <li><span class="bold">[特惠]</span>备战开学季 全民半价购数码</li>
          </ul>
        </div>
        <ul class="lifeservices">
          <li class="life-item">
            <i class="list-item"></i>
            <span class="service-intro">话费</span>
          </li>
          <li class="life-item">
            <i class="list-item"></i>
            <span class="service-intro">机票</span>
          </li>
          <li class="life-item">
            <i class="list-item"></i>
            <span class="service-intro">电影票</span>
          </li>
          <li class="life-item">
            <i class="list-item"></i>
            <span class="service-intro">游戏</span>
          </li>
          <li class="life-item">
            <i class="list-item"></i>
            <span class="service-intro">彩票</span>
          </li>
          <li class="life-item">
            <i class="list-item"></i>
            <span class="service-intro">加油站</span>
          </li>
          <li class="life-item">
            <i class="list-item"></i>
            <span class="service-intro">酒店</span>
          </li>
          <li class="life-item">
            <i class="list-item"></i>
            <span class="service-intro">火车票</span>
          </li>
          <li class="life-item">
            <i class="list-item"></i>
            <span class="service-intro">众筹</span>
          </li>
          <li class="life-item">
            <i class="list-item"></i>
            <span class="service-intro">理财</span>
          </li>
          <li class="life-item">
            <i class="list-item"></i>
            <span class="service-intro">礼品卡</span>
          </li>
          <li class="life-item">
            <i class="list-item"></i>
            <span class="service-intro">白条</span>
          </li>
        </ul>
        <div class="ads">
          <img src="./images/ad1.png" />
        </div>
      </div>
    </div>
  </div>
</template>


<script>
import { mapState } from "vuex";
// 引入包
import Swiper from "swiper";

export default {
  name: "",
  data() {
    return {};
  },
  mounted() {
    // 为什么swiper实例在mouted当中直接书写不可以，因为结构还没完整
    console.log("我是mounted");
    // 派发action: 通过vuex发送ajax请求，将数据存储在仓库当中
    this.$store.dispatch("getBannerList");
  },
  computed: {
    ...mapState({
      bannerList: (state) => state.home.bannerList,
    }),
  },
  watch: {
    // 监听bannerList数据的变化，因为这条数据发生过变化————由空数组变为数组里面有四个元素
    bannerList: {
      handler(newValue, oldValue) {
        // 现在通过watch监听bannerList属性的属性值的变化
        // 如果执行这个handler方法,代表组件实例身上这个属性的属性值已经有了【数组：四个元素】
        // 当前这个函数执行：只能保证bannerList数据已经有了，但是你没办法保证v-for已经执行结束了
        //【v-for执行完毕，才有结构，在watch当中没办法保证，所以要使用nextTick辅助完成】

        // nextTick：在下次DOM更新 循环结束之后（v-for已经执行完毕）执行延迟回调。在 修改数据之后 立即使用这个方法，获取更新后的DOM
        this.$nextTick(() => {
          // 当你执行这个回调的时候：保证服务器数据回来了，v-for执行完毕了【轮播图的结构一定有了】
          var mySwiper = new Swiper(
            // document.querySelector(".swiper-container"),   // <div class="swiper-container" id="mySwiper">
            this.$refs.mySwiper,   // <div class="swiper-container" ref="mySwiper">
            {
              // direction: 'vertical', // 垂直切换选项   默认是水平轮播
              loop: true, // 循环模式

              // 分页器
              pagination: {
                el: ".swiper-pagination",
              },

              // 前进后退按钮
              navigation: {
                nextEl: ".swiper-button-next",
                prevEl: ".swiper-button-prev",
              },
            }
          );
        });
      },
    },
  },
};
</script>


<style lang="less" scoped>
.list-container {
  width: 1200px;
  margin: 0 auto;

  .sortList {
    height: 464px;
    padding-left: 210px;

    .center {
      box-sizing: border-box;
      width: 740px;
      height: 100%;
      padding: 5px;
      float: left;
    }

    .right {
      float: left;
      width: 250px;

      .news {
        border: 1px solid #e4e4e4;
        margin-top: 5px;

        h4 {
          border-bottom: 1px solid #e4e4e4;
          padding: 5px 10px;
          margin: 5px 5px 0;
          line-height: 22px;
          overflow: hidden;
          font-size: 14px;

          .fl {
            float: left;
          }

          .fr {
            float: right;
            font-size: 12px;
            font-weight: 400;
          }
        }

        .news-list {
          padding: 5px 15px;
          line-height: 26px;

          .bold {
            font-weight: 700;
          }
        }
      }

      .lifeservices {
        border-right: 1px solid #e4e4e4;
        overflow: hidden;
        display: flex;
        flex-wrap: wrap;

        .life-item {
          border-left: 1px solid #e4e4e4;
          border-bottom: 1px solid #e4e4e4;
          margin-right: -1px;
          height: 64px;
          text-align: center;
          position: relative;
          cursor: pointer;
          width: 25%;

          .list-item {
            background-image: url(./images/icons.png);
            width: 61px;
            height: 40px;
            display: block;
          }

          .service-intro {
            line-height: 22px;
            width: 60px;
            display: block;
          }

          &:nth-child(1) {
            .list-item {
              background-position: 0px -5px;
            }
          }

          &:nth-child(2) {
            .list-item {
              background-position: -62px -5px;
            }
          }

          &:nth-child(3) {
            .list-item {
              background-position: -126px -5px;
            }
          }

          &:nth-child(4) {
            .list-item {
              background-position: -190px -5px;
            }
          }

          &:nth-child(5) {
            .list-item {
              background-position: 0px -76px;
            }
          }

          &:nth-child(6) {
            .list-item {
              background-position: -62px -76px;
            }
          }

          &:nth-child(7) {
            .list-item {
              background-position: -126px -76px;
            }
          }

          &:nth-child(8) {
            .list-item {
              background-position: -190px -76px;
            }
          }

          &:nth-child(9) {
            .list-item {
              background-position: 0px -146px;
            }
          }

          &:nth-child(10) {
            .list-item {
              background-position: -62px -146px;
            }
          }

          &:nth-child(11) {
            .list-item {
              background-position: -126px -146px;
            }
          }

          &:nth-child(12) {
            .list-item {
              background-position: -190px -146px;
            }
          }
        }
      }

      .ads {
        margin-top: 5px;

        img {
          opacity: 0.8;
          transition: all 400ms;

          &:hover {
            opacity: 1;
          }
        }
      }
    }
  }
}
</style>

```





### 抽离出来的结构

#### 新建一个全局组件Carousel

>  v-for="(carousel, index) in list" 这里的list应该由使用他的组件传递数据过来【使用  props: ['list'],进行父子组件数据传递】，这个数据形式不能乱传，应该是数组

![image-20220428233549051](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220428233549051.png)

```vue
<template>
  <!-- 轮播图的地方 -->
  <div class="swiper-container" ref="cur">
    <div class="swiper-wrapper" >
      <div
        class="swiper-slide"
        v-for="(carousel, index) in list"
        :key="carousel.id"
      >
        <img :src="carousel.imgUrl" />
      </div>
    </div>
    <!-- 如果需要分页器 -->
    <div class="swiper-pagination"></div>

    <!-- 如果需要导航按钮 -->
    <div class="swiper-button-prev"></div>
    <div class="swiper-button-next"></div>
  </div>
</template>

<script>
// 引入swiper
import Swiper from "swiper";

export default {
  name: 'Carousel',
  props: ['list'],
  watch: {
    list: {
      // 为什么watch监听不到list：因为这个数据没有发生过变化，（数据是父亲给的，父亲给的时候是一个对象，对象里面该有的数据都有）
      // 所以要使用立即监听：不管你数据有没有变化，上来就立即监听一次
      immediate: true,
      handler() {
        // watch只能监听到数据已经有了，但是v-for动态渲染结构我们还是没有办法确定的，因此还是需要用nextTick
        this.$nextTick(() => {
          // 当你执行这个回调的时候：保证服务器数据回来了，v-for执行完毕了【轮播图的结构一定有了】
          var mySwiper = new Swiper(
            // document.querySelector(".swiper-container"),   // <div class="swiper-container" id="cur">
            this.$refs.cur, // <div class="swiper-container" ref="cur">
            {
              // direction: 'vertical', // 垂直切换选项   默认是水平轮播
              loop: true, // 循环模式

              // 分页器
              pagination: {
                el: ".swiper-pagination",
              },

              // 前进后退按钮
              navigation: {
                nextEl: ".swiper-button-next",
                prevEl: ".swiper-button-prev",
              },
            }
          );
        });
      },
    },
  },
};
</script>

<style lang="less" scoped>

</style>
```



#### 在main.js中引用注册Carousel组件

> 操作类似与注册三级联动的全局组件

```vue
// 提取出来的轮播图组件
import Carousel from '@/components/Carousel'

// 注册轮播图
Vue.component(Carousel.name,Carousel)
```



#### 在需要轮播图的地方使用<Carousel>

> 在下面的两个文件中删除与轮播图有关的独立设置，只需要使用全局组件<Carousel>，
>
> 然后【使用  props: ['list'],进行父子组件数据传递】传入数据即可

大轮播图：\src\pages\Home\ListContainer\index.vue

```vue
      <div class="center">
        <!-- 轮播图的地方 -->
        <Carousel :list="bannerList"></Carousel>
      </div>
```

小轮播图：\src\pages\Home\Floor\index.vue

```vue
            <div class="floorBanner">
              <!-- 轮播图的地方 -->
              <Carousel :list="list.carouselList"></Carousel>
            </div>
```



#### 小总结

![image-20220428234742487](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220428234742487.png)





## Search界面的开发

![image-20220429174020069](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220429174020069.png)

### 使用静态组件

- 视频P40



#### \src\api\index.js

  ==export const reqSearchInfo = (params)=>requests({url:"/list",method:"POST",data:params})==

```js
  // 当前这个函数需不需要接受外部传递参数
  // 当前这个接口（获取搜索模块的数据）给服务器传递一个默认参数params，至少是一个空对象
  export const reqSearchInfo = (params)=>requests({url:"/list",method:"POST",data:params})
```

#### \src\store\search.js

```js
// search模块小仓库
import { reqSearchInfo } from "@/api"

// - state   仓库存储数据的地方
const state = {
    // ！！！注意：这边要先使用dispatch判断是一个数组[] 还是一个对象{}
    // mounted() {
    //     // 先测试接口返回的数据格式
    //     this.$store.dispatch("getSearchList",{})
    //   },
    
    // 仓库初始状态
    searchList:{}
}
// - mutations   修改state的唯一手段
const mutations = {
    GETSEARCHLIST(state,search){
        state.searchList = search
    }
}
// - actions   处理action,可以书写自己的业务逻辑，也可以处理异步
const actions = {
    // 获取search模块数据
    async getSearchList({commit},params={}){
        // 当前reqSearchInfo这个函数在调用获取服务器数据的时候，至少传递一个参数（空对象）
        // params形参：是当用户派发action的时候，第二个参数传递过来的，至少是一个空对象  【没有传递就默认为{} —— params={}】
        let result = await reqSearchInfo(params)
        if(result.code == 200){
            commit("GETSEARCHLIST",result.data)
        }
    }
}
// - getters   理解为计算属性，用于简化仓库数据，让组件获取仓库的数据更加方便
const getters = {
    //   ...mapState({
    //     goodsList:state => state.search.searchList.goodsList // 这样的仓库数据获取过于复杂
    //   })

    // 当前形参state，是当前仓库search中的state，并不是大仓库的 state
    goodsList(state){
        // 这样书写是有问题的，因为返回的可能有两种情况，undefined【断网接收不到数据的时候】和数组
        // state.searchList.goodsList：如果服务器数据回来了，可以正常接受一个数据
        // 如果网络不行，没有网络的情况下，state.searchList.goodsList返回的是undefined，
        // 遍历undefined会出现错误, 所以：使用 ||[] ，如果是undefined 返回一个空数组，防止遍历undefined
        return state.searchList.goodsList||[]
    },
    trademarkList(state){
        return state.searchList.trademarkList
    },
    attrsList(state){
        return state.searchList.attrsList
    }
}

//对外暴露store的一个实例
export default{
    state,
    mutations,
    actions,
    getters
}
```

#### \src\pages\Search\index.vue

```vue
    mounted() {
      // 要想使用三连环：state中定义的数据格式不能错，要先用dispatch测试：判断是一个数组[ ] 还是一个对象{ }
      // 先测试接口返回的数据格式
      this.$store.dispatch("getSearchList",{})
    },
```

 

### 优化部分：getters  理解为计算属性，用于简化仓库数据

【视频P42】

不在 \src\store\search.js使用getters的的写法：

\src\pages\Search\index.vue   

```vue
      import { mapState } from 'vuex'
    
    // 使用三连环界面的getters简化仓库数据
    computed:{
       ...mapState({
         goodsList:state => state.search.searchList.goodsList
       })
     }
```

使用getters：

```
   import { mapGetters } from 'vuex'
   
   computed:{
      // mapGetters里面的写法更加简洁：传递的数组，因为getters计算是没有划分模块的【home.search】
      ...mapGetters(['goodsList'])
      // ...mapGetters(['goodsList','trademarkList','attrsList'])
    }
```



## Search根据不同的参数获取数据展示

【视频P43】

因为要在这个界面可能出现多次搜索，所以会发多次请求，仅仅靠mounted 组件挂载完毕，执行一次，是不能满足要求 的，与之前的组件形成对比

把请求封装到函数中，

发一次请求，调用一次函数

```vue
   data(){
      return {
        // 带给服务器的参数
        searchParams:{
          // 一级分类ID
          category1Id: "", 
          // 二级分类ID
          category2Id: "", 
          // 三级分类ID
          category3Id: "",  
          // ————分类名称 
          categoryName: "",  
          // ————搜索关键字
          keyword: "",  
          // —————排序方式 1: 综合,2: 价格 asc: 升序,desc: 降序  
          order: "",  
          // ————页码，代表当前是第几页
          pageNo: 1,  
          // ————每页数量，代表的每一个页面展示的数据个数
          pageSize: 10,  
          //  ————商品属性的数组，平台售卖属性操作带的参数
          props: [], 
          // ————品牌
          trademark: ""  
        }
      }
    },

    // 在mounted发请求之前，带给服务器参数【searchParams参数发生变化，有数值带给服务器】
    // 当组件挂载完毕之前【先于mounted之前】
    beforeMount() {
      // 复杂的写法
      // this.searchParams.category1Id = this.$route.query.category1Id
      // this.searchParams.category1Id = this.$route.query.category2Id
      // this.searchParams.category1Id = this.$route.query.category3Id
      // this.searchParams.categoryName = this.$route.query.categoryName
      // this.searchParams.keyword = this.$route.params.keyword

      // 进阶的写法：
      // Object.assign ：ES6新增的语法，合并对象
      // this.$route.query 和 this.$route.params 拥有的相应的属性名和属性值会合并赋值给this.searchParams
      Object.assign(this.searchParams,this.$route.query,this.$route.params)
    },


    // 组件挂载完毕，执行一次，【仅仅执行一次】
    mounted() {
      // 要想使用三连环：state中定义的数据格式不能错，要先用dispatch测试：判断是一个数组[] 还是一个对象{}
      // 先测试接口返回的数据格式
      // this.$store.dispatch("getSearchList",{})

      // 在发请求之前，带给服务器参数【searchParams参数发生变化，有数值带给服务器】
      this.getData()
    },

    // 函数声明一次，可以多次调用
    methods: {
      // 向服务器发请求，获取search模块数据，（根据参数不同返回不同的数据进行展示）
      // 把这次请求封装为一个函数：当你需要再调用的时候调用即可
      getData(){
        // this.$store.dispatch("getSearchList",{})   // {} ——》searchParam
        this.$store.dispatch("getSearchList",searchParam)
      }
    },
```



### Object.assign ：ES6新增的语法，合并对象

![image-20220429172457331](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220429172457331.png)



## 面包屑相关操作

### 当分类属性（query）删除时删除面包屑同时修改路由信息。

```
<template>
  <div>
    <!-- 商品分类三级列表 组件 -->
    <TypeNav />
    <div class="main">
      <div class="py-container">
        <!--bread 面包屑-->
        <div class="bread">
          <ul class="fl sui-breadcrumb">
            <li>
              <a href="#">全部结果</a>
            </li>
          </ul>
          <ul class="fl sui-tag">
            <li class="with-x" v-if="searchParams.categoryName">{{searchParams.categoryName}}
              <i @click="removeCategoryName">×</i>
            </li>
            <!-- <li class="with-x">iphone<i>×</i></li>
            <li class="with-x">华为<i>×</i></li>
            <li class="with-x">OPPO<i>×</i></li> -->
          </ul>
        </div>

        <!--selector 选择子组件-->
        <SearchSelector />

        <!--details-->
        <div class="details clearfix">
          <div class="sui-navbar">
            <div class="navbar-inner filter">
              <!-- 分类搜索栏 -->
              <ul class="sui-nav">
                <li class="active">
                  <a href="#">综合</a>
                </li>
                <li>
                  <a href="#">销量</a>
                </li>
                <li>
                  <a href="#">新品</a>
                </li>
                <li>
                  <a href="#">评价</a>
                </li>
                <li>
                  <a href="#">价格⬆</a>
                </li>
                <li>
                  <a href="#">价格⬇</a>
                </li>
              </ul>
            </div>
          </div>
          <!-- 销售的产品列表 -->
          <div class="goods-list">
            <ul class="yui3-g">
              <li class="yui3-u-1-5"  v-for="(good,index) in goodsList" :key="good.id">
                <div class="list-wrap">
                  <div class="p-img">
                    <a href="item.html" target="_blank">
                      <img :src="good.defaultImg" />
                    </a>
                  </div>
                  <div class="price">
                    <strong>
                      <em>¥</em>
                      <i>{{good.price}}.00</i>
                    </strong>
                  </div>
                  <div class="attr">
                    <a target="_blank" href="item.html" title="促销信息，下单即赠送三个月CIBN视频会员卡！【小米电视新品4A 58 火爆预约中】">{{good.title}}</a>
                  </div>
                  <div class="commit">
                    <i class="command">已有<span>2000</span>人评价</i>
                  </div>
                  <div class="operate">
                    <a href="success-cart.html" target="_blank" class="sui-btn btn-bordered btn-danger">加入购物车</a>
                    <a href="javascript:void(0);" class="sui-btn btn-bordered">收藏</a>
                  </div>
                </div>
              </li>
            </ul>
          </div>
          <!-- 分页器 -->
          <div class="fr page">
            <div class="sui-pagination clearfix">
              <ul>
                <li class="prev disabled">
                  <a href="#">«上一页</a>
                </li>
                <li class="active">
                  <a href="#">1</a>
                </li>
                <li>
                  <a href="#">2</a>
                </li>
                <li>
                  <a href="#">3</a>
                </li>
                <li>
                  <a href="#">4</a>
                </li>
                <li>
                  <a href="#">5</a>
                </li>
                <li class="dotted"><span>...</span></li>
                <li class="next">
                  <a href="#">下一页»</a>
                </li>
              </ul>
              <div><span>共10页&nbsp;</span></div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import { mapGetters } from 'vuex'
  import SearchSelector from './SearchSelector/SearchSelector'
  export default {
    name: 'Search',

    components: {
      SearchSelector
    },

    data(){
      return {
        // 带给服务器的参数
        searchParams:{
          // 一级分类ID
          category1Id: "", 
          // 二级分类ID
          category2Id: "", 
          // 三级分类ID
          category3Id: "",  
          // ————分类名称 
          categoryName: "",  
          // ————搜索关键字
          keyword: "",  
          // —————排序方式 1: 综合,2: 价格 asc: 升序,desc: 降序  
          order: "",  
          // ————页码，代表当前是第几页
          pageNo: 1,  
          // ————每页数量，代表的每一个页面展示的数据个数
          pageSize: 10,  
          //  ————商品属性的数组，平台售卖属性操作带的参数
          props: [], 
          // ————品牌
          trademark: ""  
        }
      }
    },

    // 在mounted发请求之前，带给服务器参数【searchParams参数发生变化，有数值带给服务器】
    // 当组件挂载完毕之前【先于mounted之前】
    beforeMount() {
      // 复杂的写法
      // this.searchParams.category1Id = this.$route.query.category1Id
      // this.searchParams.category1Id = this.$route.query.category2Id
      // this.searchParams.category1Id = this.$route.query.category3Id
      // this.searchParams.categoryName = this.$route.query.categoryName
      // this.searchParams.keyword = this.$route.params.keyword

      // 进阶的写法：
      // Object.assign ：ES6新增的语法，合并对象
      // this.$route.query 和 this.$route.params 拥有的相应的属性名和属性值会合并赋值给this.searchParams
      Object.assign(this.searchParams,this.$route.query,this.$route.params)
    },

    // 组件挂载完毕，执行一次，【仅仅执行一次】
    mounted() {
      // 要想使用三连环：state中定义的数据格式不能错，要先用dispatch测试：判断是一个数组[] 还是一个对象{}
      // 先测试接口返回的数据格式
      // this.$store.dispatch("getSearchList",{})

      // 在发请求之前，带给服务器参数【searchParams参数发生变化，有数值带给服务器】
      this.getData()
    },

    // 函数声明一次，可以多次调用
    methods: {
      // 向服务器发请求，获取search模块数据，（根据参数不同返回不同的数据进行展示）
      // 把这次请求封装为一个函数：当你需要再调用的时候调用即可
      getData(){
        // this.$store.dispatch("getSearchList",{})   // {} ——》this.searchParams
        this.$store.dispatch("getSearchList",this.searchParams)
      },

      // 删除分类的名字【点击面包屑的叉号就删除所选的分类，如果地址栏已存在params，需要保留params】
      removeCategoryName(){
        // 把带给服务器的参数置空了，还需要向服务器发请求，让页面能够更新为新的分类数据
        // 带给服务器参数说明是可有可无的：如果属性值为空的字符串还是会把相应的字段带给服务器，
        // 【把不需要使用到的字段设置为undefined，就不会再次带给服务器】
        this.searchParams.category1Id = undefined
        this.searchParams.category2Id = undefined
        this.searchParams.category3Id = undefined
        this.searchParams.categoryName = undefined
        this.getData()
        // 地址栏此时还没有修改，也需要更新：在自己的路由组件跳自己，将页面地址栏刷新
        // 本意是删除query【三级分类产生】参数，如果路径中有params【搜索框关键字产生】参数，不应该删除，应该保留
        if(this.$route.params){
          this.$router.push({name:"search",params:this.$route.params})
        }

      }
    },

    // 使用三连环界面的getters简化仓库数据
    // computed:{
    //   ...mapState({
    //     goodsList:state => state.search.searchList.goodsList
    //   })
    // }

    // 仓库中的state是分模块的【里面除了需要的Search还涉及到Home模块】，
    // 而三连环部分简化仓库属性的getters是不分模块的，直接调用，不需要再考虑他是哪个模块的
    computed:{
      // mapGetters里面的写法更加简洁：传递的数组，因为getters计算是没有划分模块的【home.search】
      ...mapGetters(['goodsList'])
      // ...mapGetters(['goodsList','trademarkList','attrsList'])
    },

    // 数据监听：监听组件实例身上的属性的属性值变化
    watch:{
      // 监听路由的信息是否发生变化：如果发生变化，再次发送请求
      $route(newValue,oldValue){
        // 分类名字与关键字不用清理：因为每一次路由发生变化的时候，都会给它赋予新的数据
        // 每一次请求完毕，应该把相应的1.2.3级ID置空【清除上一次的对下一次的残留影响】，让他接受下一次的1.2.3级ID
        this.searchParams.category1Id = '';
        this.searchParams.category2Id = '';
        this.searchParams.category3Id = '';

        // 再次发请求之前，整理带给服务器的参数，否则不会发生变化，只是在beforeMount()整理了一次
        Object.assign(this.searchParams,this.$route.query,this.$route.params)
        // console.log(this.searchParams);
        // 再次发起Ajax请求【getData(再次调用，就需要再次发送请求)】
        this.getData()
    }
  }
}
</script>


```



### 当搜索关键字（params）删除时删除面包屑、修改路由信息、同时删除输入框内的关键字。

#### 数组去重







## 排序操作

在线链接：复制之后还需要在前面添加`https:`

```
  <!-- 导入阿里的图标 -->
    <link rel="stylesheet" href="https://at.alicdn.com/t/font_3369530_kdivirhoyy.css">
```

![image-20220430102103776](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220430102103776.png)

```vue
<template>
  <div>
    <!-- 商品分类三级列表 组件 -->
    <TypeNav />
    <div class="main">
      <div class="py-container">
        <!--bread 面包屑-->
        <div class="bread">
          <ul class="fl sui-breadcrumb">
            <li>
              <a href="#">全部结果</a>
            </li>
          </ul>
          <ul class="fl sui-tag">
            <!-- 上面的分类和关键字是在本页面使用三级分类[改变query]以及搜索框[改变params]触发事件，使用到的是this.$route.params和this.$route.query -->
            <!-- 分类的面包屑 -->
            <li class="with-x" v-if="searchParams.categoryName">{{searchParams.categoryName}}
              <i @click="removeCategoryName">×</i>
            </li>
            <!-- 关键字的面包屑 -->
            <li class="with-x" v-if="searchParams.keyword">{{searchParams.keyword}}
              <i @click="removeKeyword">×</i>
            </li>

            <!-- 下面的品牌和商品售卖属性需要通过子组件SearchSelector里面触发点击事件，然后子传父，让父组件接收到点击的（品牌名称，商品售卖属性）信息 -->
            <!-- 品牌信息的面包屑 -->
            <!-- {{ searchParams.trademark.split(":")[1] }} 只截取品牌名称的部分 -->
            <li class="with-x" v-if="searchParams.trademark">{{searchParams.trademark.split(":")[1]}}
              <i @click="removeTrademark">×</i>
            </li>
            <!-- 商品售卖属性值的面包屑 -->
            <!-- 因为要遍历数组，所以不再使用v-if，而是v-for -->
            <li class="with-x" v-for="(attrProp,index) in searchParams.props" :key="index">{{attrProp.split(":")[1]}}
              <i @click="removeAttr">×</i>
            </li>
          </ul>
        </div>

        <!--selector 选择子组件-->
        <!-- 自定义事件：实现子传父 -->
        <SearchSelector @trademarkInfo="trademarkInfo" @attrInfo="attrInfo"/>

        <!--details-->
        <div class="details clearfix">
          <div class="sui-navbar">
            <div class="navbar-inner filter">
              <!-- 分类搜索栏 -->
              <ul class="sui-nav">
                <!-- 谁被选中，谁的class就是active，表现为背景为红色【所以这个class要设置为动态的】 -->
                <!-- <li :class="{active : searchParams.order.indexOf('1') != -1}" > -->
                  <!-- 使用计算属性来简化这里的判断 【searchParams.order.indexOf('1') != -1】==>【isOne】 -->
                <li :class="{active : isOne}"  @click="changeOrder('1')" >
                  <!-- 这里的升序、降序是跟着综合、价格联动显示的，图标使用阿里的，需要在index.html中导入 -->
                  <a href="#">综合<span v-show="isOne" class="iconfont" :class="{'icon-xiangxiajiantoucuxiao':isDesc,'icon-xiangshangjiantoucuxiao':isAsc}"></span></a>
                </li>
                <li :class="{active : isTwo}"  @click="changeOrder('2')">
                  <a href="#">价格<span v-show="isTwo" class="iconfont" :class="{'icon-xiangxiajiantoucuxiao':isDesc,'icon-xiangshangjiantoucuxiao':isAsc}"></span></a>
                </li>
              </ul>
            </div>
          </div>
          <!-- 销售的产品列表 -->
          <div class="goods-list">
            <ul class="yui3-g">
              <li class="yui3-u-1-5"  v-for="(good,index) in goodsList" :key="good.id">
                <div class="list-wrap">
                  <div class="p-img">
                    <a href="item.html" target="_blank">
                      <img :src="good.defaultImg" />
                    </a>
                  </div>
                  <div class="price">
                    <strong>
                      <em>¥</em>
                      <i>{{good.price}}.00</i>
                    </strong>
                  </div>
                  <div class="attr">
                    <a target="_blank" href="item.html" title="促销信息，下单即赠送三个月CIBN视频会员卡！【小米电视新品4A 58 火爆预约中】">{{good.title}}</a>
                  </div>
                  <div class="commit">
                    <i class="command">已有<span>2000</span>人评价</i>
                  </div>
                  <div class="operate">
                    <a href="success-cart.html" target="_blank" class="sui-btn btn-bordered btn-danger">加入购物车</a>
                    <a href="javascript:void(0);" class="sui-btn btn-bordered">收藏</a>
                  </div>
                </div>
              </li>
            </ul>
          </div>
          <!-- 分页器 -->
          <div class="fr page">
            <div class="sui-pagination clearfix">
              <ul>
                <li class="prev disabled">
                  <a href="#">«上一页</a>
                </li>
                <li class="active">
                  <a href="#">1</a>
                </li>
                <li>
                  <a href="#">2</a>
                </li>
                <li>
                  <a href="#">3</a>
                </li>
                <li>
                  <a href="#">4</a>
                </li>
                <li>
                  <a href="#">5</a>
                </li>
                <li class="dotted"><span>...</span></li>
                <li class="next">
                  <a href="#">下一页»</a>
                </li>
              </ul>
              <div><span>共10页&nbsp;</span></div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import { mapGetters } from 'vuex'
  import SearchSelector from './SearchSelector/SearchSelector'
  export default {
    name: 'Search',

    components: {
      SearchSelector
    },

    data(){
      return {
        // 带给服务器的参数
        searchParams:{
          // 一级分类ID
          category1Id: "", 
          // 二级分类ID
          category2Id: "", 
          // 三级分类ID
          category3Id: "",  
          // ————分类名称 
          categoryName: "",  
          // ————搜索关键字
          keyword: "",  
          // —————排序方式 1: 综合,2: 价格 asc: 升序,desc: 降序 ==> 综合/价格:asc/desc
          // 初始状态是默认【1】且降序【desc】
          order: "1:desc",  
          // ————页码，代表当前是第几页
          pageNo: 1,  
          // ————每页数量，代表的每一个页面展示的数据个数
          pageSize: 10,  
          //  ————商品属性的数组，平台售卖属性操作带的参数
          props: [], 
          // ————品牌
          trademark: ""  
        }
      }
    },

    // 在mounted发请求之前，带给服务器参数【searchParams参数发生变化，有数值带给服务器】
    // 当组件挂载完毕之前【先于mounted之前】
    beforeMount() {
      // 复杂的写法
      // this.searchParams.category1Id = this.$route.query.category1Id
      // this.searchParams.category1Id = this.$route.query.category2Id
      // this.searchParams.category1Id = this.$route.query.category3Id
      // this.searchParams.categoryName = this.$route.query.categoryName
      // this.searchParams.keyword = this.$route.params.keyword

      // 进阶的写法：
      // Object.assign ：ES6新增的语法，合并对象
      // this.$route.query 和 this.$route.params 拥有的相应的属性名和属性值会合并赋值给this.searchParams
      Object.assign(this.searchParams,this.$route.query,this.$route.params)
    },

    // 组件挂载完毕，执行一次，【仅仅执行一次】
    mounted() {
      // 要想使用三连环：state中定义的数据格式不能错，要先用dispatch测试：判断是一个数组[] 还是一个对象{}
      // 先测试接口返回的数据格式
      // this.$store.dispatch("getSearchList",{})

      // 在发请求之前，带给服务器参数【searchParams参数发生变化，有数值带给服务器】
      this.getData()
    },

    // 函数声明一次，可以多次调用
    methods: {
      // 向服务器发请求，获取search模块数据，（根据参数不同返回不同的数据进行展示）
      // 把这次请求封装为一个函数：当你需要再调用的时候调用即可
      getData(){
        // this.$store.dispatch("getSearchList",{})   // {} ——》this.searchParams
        this.$store.dispatch("getSearchList",this.searchParams)
      },

      // 删除分类的名字【点击面包屑的叉号就删除所选的分类，如果地址栏已存在params，需要保留params】
      removeCategoryName(){
        // 把带给服务器的参数置空了，还需要向服务器发请求，让页面能够更新为新的分类数据
        // 带给服务器参数说明是可有可无的：如果属性值为空的字符串还是会把相应的字段带给服务器，
        // 【把不需要使用到的字段设置为undefined，就不会再次带给服务器】
        this.searchParams.category1Id = undefined
        this.searchParams.category2Id = undefined
        this.searchParams.category3Id = undefined
        this.searchParams.categoryName = undefined
        this.getData()
        // 地址栏此时还没有修改，也需要更新：在自己的路由组件跳自己，将页面地址栏刷新
        // 本意是删除query【三级分类产生】参数，如果路径中有params【搜索框关键字产生】参数，不应该删除，应该保留
        if(this.$route.params){
          this.$router.push({name:"search",params:this.$route.params})
        }
      },

      // 当搜索关键字（params）删除时删除面包屑、修改路由信息、同时删除输入框内的关键字。
      removeKeyword(){
        // 给服务器带的参数searchParams的keyword置空
        this.searchParams.keyword = undefined
        // 再次发送请求，让界面显示的数据是新的请求数据【但是此时地址栏还没变，下面需要进一步处理】
        this.getData()
        // 通知兄弟组件Header清除关键字【兄弟间通信，使用$bus，需要先在main.js中设置】  ——>    this.$bus.$on("clear",()=>{ this.keyword = ''  })
        this.$bus.$emit("clear")
        // 实现路由的跳转【在自己的路由跳自己，让地址栏更新】
        if(this.$route.query){
          this.$router.push({name:"search",query:this.$route.query})
        }
      },

//  子组件SearchSelector负责把点击的品牌信息trademark传递给给父组件的回调函数trademarkInfo，然后父组件Selector通过getData()里的searchParams传给服务器
      // 自定义事件回调 ：品牌字段 // 子组件中：this.$emit("trademarkInfo",trademark)
      trademarkInfo(trademark){
        // 1。整理品牌字段的参数：“ID：品牌名称” ——之后要使用里面的tmName——{{ searchParams.trademark.split(":")[1] }} 只截取品牌名称的部分
        this.searchParams.trademark = `${trademark.tmId}:${trademark.tmName}`
        // 2。再次发送请求【使得界面显示的数据更新】
        this.getData()
      },
      // 删除品牌分类的名字
      removeTrademark(){
        this.searchParams.trademark = undefined
        this.getData()
      },

      // 自定义事件回调：收集商品属性【这个比较特殊，是因为是数组形式 —— props[]】
      attrInfo(attr,attrValue){
        // 1.整理商品属性字段的参数 ["属性ID:属性值:属性名"]
        let props = `${attr.attrId}:${attrValue},${attr.attrName}`
        // 数组去重:当数组中没有这个新增的props,才能继续往里面添加
        if( this.searchParams.props.indexOf(props) == -1 ){
          this.searchParams.props.push(props)
        }
        // 再次发请求
        this.getData()
      },
      removeAttr(index){
        // 再次整理参数
        this.searchParams.props.splice(index,1)
        // 再次发请求
        this.getData()
      },

      // 点击综合和价格，实现切换
      changeOrder(flag){
        // flag形参：他是一个标记，代表用户点击的是综合【1】还是价格【2】，【用户点击的时候传递进来的】
        
        // 这里获取到的是最开始[没有点击之前的]的状态【分别获取综合、价格||升序、降序】
        let originOrder = this.searchParams.order
        let originFlag = this.searchParams.order.split(":")[0]
        let originSort = this.searchParams.order.split(":")[1]
        // 起始的flag——originFlag；用户点击的flag——flag【传进来的形参】

        // 准备一个新的order属性值
        let newOrder = ""
        // 1. 点击的还是原来的那一个方块【保留原来方块的originFlag,就把升序降序取反即可】
        if(originFlag == flag){
          newOrder = `${originFlag}:${originSort == "desc"?"asc":"desc"}`
        }
        // 2. 点击的是另一个方块【切换为另一个方块的flag,默认第一次点击方块都是按照降序排列的】
        else{
          newOrder = `${flag}:${"desc"}`
        }
        
        // 将新的order赋予searchParams
        this.searchParams.order = newOrder
        // 再次发送请求
        this.getData()

      }

    },

    // 使用三连环界面的getters简化仓库数据
    // computed:{
    //   ...mapState({
    //     goodsList:state => state.search.searchList.goodsList
    //   })
    // }

    // 仓库中的state是分模块的【里面除了需要的Search还涉及到Home模块】，
    // 而三连环部分简化仓库属性的getters是不分模块的，直接调用，不需要再考虑他是哪个模块的
    computed:{
      // mapGetters里面的写法更加简洁：传递的数组，因为getters计算是没有划分模块的【home.search】
      ...mapGetters(['goodsList']),
      // ...mapGetters(['goodsList','trademarkList','attrsList'])

      isOne(){
        return this.searchParams.order.indexOf('1') != -1
      },
      isTwo(){
        return this.searchParams.order.indexOf('2') != -1
      },

      isAsc(){
        return this.searchParams.order.indexOf('asc') != -1
      },
      isDesc(){
        return this.searchParams.order.indexOf('desc') != -1
      }

    },

    // 数据监听：监听组件实例身上的属性的属性值变化
    watch:{
      // 监听路由的信息是否发生变化：如果发生变化，再次发送请求
      $route(newValue,oldValue){
        // 分类名字与关键字不用清理：因为每一次路由发生变化的时候，都会给它赋予新的数据
        // 每一次请求完毕，应该把相应的1.2.3级ID置空【清除上一次的对下一次的残留影响】，让他接受下一次的1.2.3级ID
        this.searchParams.category1Id = '';
        this.searchParams.category2Id = '';
        this.searchParams.category3Id = '';

        // 再次发请求之前，整理带给服务器的参数，否则不会发生变化，只是在beforeMount()整理了一次
        Object.assign(this.searchParams,this.$route.query,this.$route.params)
        // console.log(this.searchParams);
        // 再次发起Ajax请求【getData(再次调用，就需要再次发送请求)】
        this.getData()
      }
  }
}
</script>

<style lang="less" scoped>
</style>
```





## 分页

【P52开始，P54再次总结】

![image-20220430142540810](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220430142540810.png)

**\src\pages\Search\index.vue【父组件使用props给子组件Pagination传数据】**

```vue
          <!-- 分页器 -->
          <!-- 测试分页器阶段，这里的数据将来是要替换的，由服务器提供过来 -->
          <Pagination :pageNo="2" :pageSize="5" :total="41" :continues="5"></Pagination>
```



**\src\components\Pagination\index.vue**

```vue
<template>
  <div class="pagination">
    <button>上一页</button>
    <button>1</button>
    <button>···</button>

    <button>3</button>
    <button>4</button>
    <button>5</button>
    <button>6</button>
    <button>7</button>
    
    <button>···</button>
    <button>{{totalPage}}</button>
    <button>下一页</button>
    
    <button style="margin-left: 30px">共 {{total}} 条</button>
    <h1>{{startNumAndEndNum}}-----{{pageNo}}</h1>
  </div>
</template>

<script>
  export default {
    name: "Pagination",
    // 接收父组件传过来的数据
    // 当前是第几页，一页有多少数据，一共有多少数据，分页连续页码数
    props: ['pageNo','pageSize','total','continues'],

    computed:{
      // 总共有多少页 ——>total/pageSize之后的数据是小数，所以需要向上取整
      totalPage(){
        // 向上取整
        return Math.ceil(this.total / this.pageSize)
      },

      // 计算出连续的页码的起始数字和结束数字【连续页码的数字至少是5.一般都是奇数，才能让他对称显示】
      startNumAndEndNum(){
        const { continues,pageNo,totalPage} = this
        // 先定义两个变量存储起始数字和结束数字
        let start = 0,
            end = 0;
        // 连续页码数字continues需要有五页，
        // 【不正常情况：总共都没有五页,总页数没有需要显示的连续页码多】
        if(continues > totalPage){
          start = 1
          end = totalPage
        }
        // 【总共是有五页的，足以显示五页的连续页码】
        else{
          // 起始数字
          start = pageNo - parseInt(continues/2)
          // 结束数字
          end = pageNo + parseInt(continues/2)
          // 【不正常现象：start数字出现0，负数】
          // 0 1 (2) 3 4  ==> 1 (2) 3 4 5
          if(start < 1){
            start = 1  // 页码最小也只能是1开头
            end = continues
          }
          // 【不正常现象：end数字大于总页码】
          // 一共9页:  7 8 (9) 10 11  ==> 5 6 7 8 (9) 
          else if(end > totalPage){
            end = totalPage  // 页码最大只能是总页数
            start = totalPage - continues + 1  // (9)-5【continues】+1=5
          }
        }

        return { start , end }
      }
    }
  }
</script>

<style lang="less" scoped>
</style>

```



## 分页器完成

\src\pages\Search\index.vue

```vue
 <!-- 分页器 -->
          <!-- 测试分页器阶段，这里的数据将来是要替换的，由服务器提供过来 -->
          <Pagination :pageNo="searchParams.pageNo" :pageSize="searchParams.pageSize" :total="total" :continues="5" @getPageNo="getPageNo"></Pagination>



methods:{
      getPageNo(pageNo){
        // 整理参数
        this.searchParams.pageNo = pageNo
        // 再次发送请求
        this.getData()
      }
}

// 这里的total,虽然存在于searchList，但是并没有通过searchParams传进来，所以要使用...mapState单独去获取
computed:{
      ...mapState({
        total:state => state.search.searchList.total
      })
}
```



\src\components\Pagination\index.vue

```vue
<template>
  <div class="pagination">
    <button :disabled="pageNo == 1" @click="$emit('getPageNo',pageNo - 1)" >上一页</button>
    <button v-if="startNumAndEndNum.start > 1" @click="$emit('getPageNo',1)" :class="{active:pageNo == 1}">1</button>
    <button v-if="startNumAndEndNum.start > 2">···</button>

    <button v-for="(page,index) in startNumAndEndNum.end" :key="index" v-if="page >= startNumAndEndNum.start" @click="$emit('getPageNo',page)" :class="{active:pageNo == page}">{{page}}</button>
    
    <button v-if="startNumAndEndNum.end < totalPage - 1">···</button>
    <button v-if="startNumAndEndNum.end < totalPage" @click="$emit('getPageNo',totalPage)" :class="{active:pageNo == totalPage}">{{totalPage}}</button>
    <button :disabled="pageNo == totalPage" @click="$emit('getPageNo',pageNo + 1)">下一页</button>
    
    <button style="margin-left: 30px">共 {{total}} 条</button>
    <h1>{{startNumAndEndNum}}-----当前的页码：{{pageNo}}</h1>
  </div>
</template>

<script>
  export default {
    name: "Pagination",
    // 接收父组件传过来的数据
    // 当前是第几页，一页有多少数据，一共有多少数据，分页连续页码数
    props: ['pageNo','pageSize','total','continues'],

    computed:{
      // 总共有多少页 ——>total/pageSize之后的数据是小数，所以需要向上取整
      totalPage(){
        // 向上取整
        return Math.ceil(this.total / this.pageSize)
      },

      // 计算出连续的页码的起始数字和结束数字【连续页码的数字至少是5.一般都是奇数，才能让他对称显示】
      startNumAndEndNum(){
        const { continues,pageNo,totalPage} = this
        // 先定义两个变量存储起始数字和结束数字
        let start = 0,
            end = 0;
        // 连续页码数字continues需要有五页，
        // 【不正常情况：总共都没有五页,总页数没有需要显示的连续页码多】
        if(continues > totalPage){
          start = 1
          end = totalPage
        }
        // 【总共是有五页的，足以显示五页的连续页码】
        else{
          // 起始数字
          start = pageNo - parseInt(continues/2)
          // 结束数字
          end = pageNo + parseInt(continues/2)
          // 【不正常现象：start数字出现0，负数】
          // 0 1 (2) 3 4  ==> 1 (2) 3 4 5
          if(start < 1){
            start = 1  // 页码最小也只能是1开头
            end = continues
          }
          // 【不正常现象：end数字大于总页码】
          // 一共9页:  7 8 (9) 10 11  ==> 5 6 7 8 (9) 
          else if(end > totalPage){
            end = totalPage  // 页码最大只能是总页数
            start = totalPage - continues + 1  // (9)-5【continues】+1=5
          }
        }

        return { start , end }
      }
    }
  }
</script>


<style lang="less" scoped>
  .pagination {
    text-align: center;
    button {
      margin: 0 5px;
      background-color: #f4f4f5;
      color: #606266;
      outline: none;
      border-radius: 2px;
      padding: 0 4px;
      vertical-align: top;
      display: inline-block;
      font-size: 13px;
      min-width: 35.5px;
      height: 28px;
      line-height: 28px;
      cursor: pointer;
      box-sizing: border-box;
      text-align: center;
      border: 0;

      &[disabled] {
        color: #c0c4cc;
        cursor: not-allowed;
      }

      &.active {
        cursor: not-allowed;
        background-color: #409eff;
        color: #fff;
      }
    }
  }
  .active{
    background-color: #409eff;
  }
</style>
```





## 详情组件【Detail】

![image-20220430221321885](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220430221321885.png)



### **路由跳转**

1. 先配置路由： **\src\router\routes.js**

   **要使用占位符 ==:skuid==**【因为传递过来的还有商品参数】

   **/detail/==:skuid== 才能搜索部分传递过来的商品参数接收 /detail/==${good.id}==**

   ```
   import Detail from '@/pages/Detail'
   
     {
       // 这边路径不能写错，否则只会跳转到首页【/:skuid一定要占位】
       path: '/detail/:skuid',
       component: Detail,
       meta:{show:true}
     },
   ```

   

2. 再设置点击搜索区域的商品图片能够跳转到详情页面，在路由跳转的时候不要忘记带id【params】参数给详情页面【详情页面使用占位符 ==/:skuid==接收】：

   **\src\pages\Search\index.vue**

   ```
   <div class="p-img">
       <!-- 在路由跳转的时候不要忘记带id【params】参数 -->
       <router-link :to="`/detail/${good.id}`">
           <img :src="good.defaultImg" />
       </router-link>
   </div>
   ```



### 请求参数

2. **\src\api\index.js**   ==> axios：【配置api接口】  ***reqGoodsInfo***

   ==url: **\` /item/${skuId}\ `**   不能写成   **url:"/item/{skuId}"**== 

   ==【要写成字符串匹配格式：否则导致收到的不是商品skuId，而是一串乱码】==

   ```js
     // 查询文档可知：商品详情 /api/item/{ skuId }   ——{skuId}在路由中使用skuid占位，所以存在skuid于params中 【dispatch 使用this.$route.params.skuid获取 】
     // url:`/item/${skuId}`   不能写成   url:"/item/{skuId}"
     export const reqGoodsInfo = (skuId) =>requests({ url:`/item/${skuId}`, method:"GET" })
   ```

   

3. 配置三连环的仓库  ***getGoodInfo   GETGOODINFO***

   ==**import {reqGoodsInfo} from "@/api"  别忘记引入**==

   **\src\store\detail.js**

   ```js
   import {reqGoodsInfo} from "@/api"
   
   const actions = {
     // 获取产品信息的action
     async getGoodInfo({commit},skuId){
       let result = await reqGoodsInfo(skuId)
       if(result.code == 200){
         commit("GETGOODINFO",result.data)
       }
     }
   }
   const mutations = {
     GETGOODINFO(state,good){
       state.goodInfo = good
     }
   }
   const state = {
     // 应该先查出这个是对象还是数组，才能写
     goodInfo:{}
   }
   
   const getters = {}
   
   export default {
     actions,
     mutations,
     state,
     getters
   }
   ```



### 派发请求

2. 派发请求：派发action获取产品详情的信息

   占位的是skuid，使用skuId 会收取不到

   **\src\pages\Detail\index.vue**

   ```vue
       mounted() {
         // 派发action获取产品详情的信息
         // console.log(this.$route.params);
         this.$store.dispatch("getGoodInfo",this.$route.params.skuid)
       },
   ```



### 滚动行为

2. 跳转到详情的时候，滚轮不在顶部，需要调整

   **\src\router\index.js**

   ```js
   // 向外默认暴露VueRouter路由实例，路由器对象
   export default new VueRouter({
     mode: 'history',  // 没有#的模式
     routes,  // 注册所有路由
     //滚动行为的设置
     scrollBehavior(to, from, savedPosition) {
       //设置Y轴的起点【y属性值没有负数】
       //当然滚动行为也可以设置x轴的
       // 这里的{ y: 0 }代表距离顶部为0
       return { y: 0 }
     }
   })
   ```

   

### 这里尤其要注意的点是

- \src\api\index.js   ==> axios：【配置api接口】

==url: **\` /item/${skuId}\ `**   不能写成   **url:"/item/{skuId}"**== 

==【要写成字符串匹配格式：否则导致收到的不是商品skuId，而是一串乱码】==

```

  // 商品详情 /api/item/{ skuId }   ——skuId在路由的params中 【dispatch 使用这个获取 this.$route.params.skuid】
  // url:`/item/${skuId}`   不能写成   url:"/item/{skuId}"
  export const reqGoodsInfo = (skuId) =>requests({ url:`/item/${skuId}`, method:"GET" })
```



- \src\router\routes.js ==> 配置路由

要使用占位符【因为传递过来的还有商品参数】

```
  {
    // 这边路径不能写错，否则只会跳转到首页【/:skuid一定要占位】
    path: '/detail/:skuid',
    component: Detail,
    meta:{show:true}
  },
```



### 修改动态数据

使用getters简化数据【商品名称，介绍，价格】

**\src\store\detail.js**

```
const getters = {
  categoryView(state){
    // state.goodInfo初始状态是空对象，空对象的categoryView的值为undefined【所以不写||{}会假报错】
    // 计算出来的categoryView至少是一个空对象{}
    return state.goodInfo.categoryView||{}
  },
  skuInfo(state){
    // state.goodInfo初始状态是空对象，空对象的skuInfo的值为undefined【所以不写||{}会假报错】
    // 计算出来的skuInfo至少是一个空对象{}
    return state.goodInfo.skuInfo||{}
  }
}

```



**\src\pages\Detail\index.vue**

```vue
<!-- 导航路径区域 -->
<div class="conPoin">
    <span v-show="categoryView.category1Name">{{categoryView.category1Name}}</span>
    <span v-show="categoryView.category2Name">{{categoryView.category2Name}}</span>
    <span v-show="categoryView.category3Name">{{categoryView.category3Name}}</span>
</div>
      
     
<h3 class="InfoName">{{skuInfo.skuName}}</h3>
<p class="news">{{skuInfo.skuDesc}}</p>

<em>{{skuInfo.price}}</em>
    
    
    computed:{
      ...mapGetters(['categoryView','skuInfo'])
    }
```



### 放大镜显示产品信息的数据

父组件给子组件传递数据,，使用props

> \src\store\detail.js      **skuInfo**
>
> ```js
> const getters = {
>   skuInfo(state){
>     // state.goodInfo初始状态是空对象，空对象的skuInfo的值为undefined【所以不写||{}会假报错】
>     // 计算出来的skuInfo至少是一个空对象{}
>     return state.goodInfo.skuInfo||{}
>   }
> }
> ```



父组件（详情页面）：\src\pages\Detail\index.vue   **skuInfo.skuImageList【这里要求上面的skuInfo至少是空对象 { } ，才不会让skuInfo.skuImageList是undefined】**

```vue
<!--放大镜效果-->
<Zoom :skuImageList="skuImageList"/>
          
          
    computed:{
      ...mapGetters(['categoryView','skuInfo']),
      // 给子组件的数据【放大镜的数据】
      skuImageList(){
        // 如果服务器的数据没有回来，skuInfo这个对象是空对象,此时skuInfo.skuImageList是undefined 【所以要让skuInfo.skuImageList至少是一个空数组，而不是undefined】
        return this.skuInfo.skuImageList || []
      }
    },
```



子组件（放大镜部分）：\src\pages\Detail\Zoom\Zoom.vue   **skuImageList [0]【这里要求上面的skuImageList至少是一个空数组 [ ]，才不会让第一项skuImageList [0]是undefined】**

**imgObj.imgUrl  ==>  skuImageList[0].imgUrl 【还要让 skuImageList[0] 至少是一个空对象 ，才不会让 skuImageList[0].imgUrl 是undefined】**

```vue
<template>
  <div class="spec-preview">
    <img :src="imgObj.imgUrl" />
    <div class="event"></div>
    <div class="big">
      <img :src="imgObj.imgUrl" />
    </div>
    <div class="mask"></div>
  </div>
</template>

<script>
  export default {
    name: "Zoom",
    props:['skuImageList'],

    computed:{
      imgObj(){
        // 如果skuImageList 这个数组是空数组，空数组的第一项skuImageList[0]就会是undefined，
        // 还要让 skuImageList[0] 至少是一个空对象  ==》|| {}
        return this.skuImageList[0] || {}
      }
    }
  }
</script>
```



src\pages\Detail\ImageList\ImageList.vue【放大镜的小轮播图部分】

```vue
<template>
  <div class="swiper-container">
    <div class="swiper-wrapper">
      <div class="swiper-slide" v-for="(slide,index) in skuImageList" :key="slide.id">
        <img :src="slide.imgUrl">
      </div>
    </div>
    <div class="swiper-button-next"></div>
    <div class="swiper-button-prev"></div>
  </div>
</template>

<script>

  import Swiper from 'swiper'
  export default {
    name: "ImageList",
    props:['skuImageList'],
  }
</script>
```

别忘了 src\pages\Detail\index.vue 【要不然小图不显示】

```
<!-- 小图列表 -->
<ImageList :skuImageList="skuImageList"/>
```



### 展示产品售卖属性的数据





## 购物车

![image-20220502132736086](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220502132736086.png)

### 加入购物车

![image-20220502145757048](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220502145757048.png)



> 在商品详情页面点击加入购物车按钮，
>
> - 成功进行路由跳转和参数传递
>
>   -  **先判断请求是否成功：**this.$store.dispatch("addOrUpdateShopCart",{skuId:this.$route.params.skuid, skuNum:this.skuNum})
>     上面的代码是：在调用vue仓库中的addOrUpdateShopCart函数，这个方法加上async,所以返回的一定是一个Promise[await这个参数的返回值，就能够判断是否成功请求]
>
>     
>
>   -  **在路由跳转【this.$router.push({ name: "addcartsuccess" });】的时候还需要将产品的信息带给下一级的路由组件：【detail->AddCartSuccess】**
>
>      一些简单的数据【如**skuNum**】,直接通过地址栏的query形式给路由组件传递过去
>
>     产品信息的数据【比较复杂：**skuInfo**】,通过会话存储sessionStorage（不持久化，会话结束后会消失），本地存储|会话存储。一般存储的是字符串，不是对象【先把字符串变成对象JSON.stringify();获取到时候再转化为对象JSON.parse()】
>
>     
>
>     **skuInfo：** ==sessionStorage==.**setItem**("SKUINFO",JSON.**stringify**(this.skuInfo))
>                        
>     **skuNum：**
>                        
>     this.$router.**push**({ name: "addcartsuccess",==query:{skuNum:this.skuNum}== });



#### 路由传递参数{skuNum}结合会话存储{skuInfo}

src\pages\Detail\index.vue

```vue
<div class="add" @click="addShopCar">
<a href="javascript:">加入购物车</a>
</div>


<script>
export default {
methods:{
 // 加入购物车的回调函数
    async addShopCar() {
      // 1. 【路由跳转之前发请求】在点击购物车这个按钮的时候，做的第一件事情，将参数带给服务器，
      // 发请求：将产品加入到数据库（通知服务器加入购物车的产品是谁）
      /*
        当前这里是派发了一个action，也向服务器发请求
        判断加入购物车是成功还是失败了
        this.$store.dispatch("addOrUpdateShopCart",{skuId:this.$route.params.skuid, skuNum:this.skuNum})
        上面的代码是：在调用vue仓库中的addOrUpdateShopCart函数，
        这个方法加上async,所以返回的一定是一个Promise[await这个参数的返回值，就能够判断是否成功请求]
      */
    //  2.你需要知道这次请求是成功还是失败，如果成功进行路由跳转，如果失败返回失败信息
      //  【成功：路由跳转与参数传递】
      try {
        await this.$store.dispatch("addOrUpdateShopCart", {
          skuId: this.$route.params.skuid,
          skuNum: this.skuNum,
        });
        // 3. 进行路由的跳转
        // this.$router.push({ name: "addcartsuccess" });
        // 4. 在路由跳转的时候还需要将产品的信息带给下一级的路由组件
        // 一些简单的数据【如skuNum】,直接通过地址栏的query形式给路由组件传递过去
        // 产品信息的数据【比较复杂：skuInfo】,通过会话存储sessionStorage（不持久化，会话结束后会消失）
        // 本地存储|会话存储。一般存储的是字符串，不是对象【先把字符串变成对象JSON.stringify();获取到时候再转化为对象JSON.parse()】
        sessionStorage.setItem("SKUINFO",JSON.stringify(this.skuInfo))
        this.$router.push({ name: "addcartsuccess",query:{skuNum:this.skuNum} });
      } catch (error) {
        //  【失败：提示失败信息】
        alert(error.message);
      }

      // 2.服务器存储成功：进行路由跳转传递参数
      // 3.失败给用户进行提示
    },
}
}
</script>
```



src\api\index.js    **reqAddOrUpdateShopCart**

```js
  // 将产品添加到购物车：/api/cart/addToCart/{ skuId }/{ skuNum }  
  // POST  (在请求头中需要加入UUID的标识;请求头的名称叫userTempId)
  export const reqAddOrUpdateShopCart = (skuId,skuNum) =>requests({ url:`/cart/addToCart/${skuId}/${skuNum}`, method:"POST" })
```



src\store\detail.js   **addOrUpdateShopCart**

```js
import {reqGoodsInfo,reqAddOrUpdateShopCart} from "@/api"


const actions = {
  // 获取产品信息的action
  async getGoodInfo({commit},skuId){
    let result = await reqGoodsInfo(skuId)
    if(result.code == 200){
      commit("GETGOODINFO",result.data)
    }
  },
  // 将产品添加到购物车中
  async addOrUpdateShopCart({commit},{skuId,skuNum}){
    // 加入购物车返回的结构
    // 加入购物车之后（发请求），前台将参数带给服务器
    // 服务器写入数据成功，并没有返回其他的数据，只是返回code=200，代表这次操作成功
    // 因为服务器没有返回其他数据，因此咱们不需要三连环存储数据
    // addOrUpdateShopCart这个方法加上async,所以返回的一定是一个Promise[能够判断是否成功请求]
    let result = await reqAddOrUpdateShopCart(skuId,skuNum)
    // 代表加入购物车成功
    if(result.code == 200){
      return "成功"
    }else{
      // 代表加入购物车失败
      return Promise.reject(new Error('fail'))
    }
  }
}
```



#### 购物车静态组件修改

因为【this.$router.push({ name: "addcartsuccess",query:{skuNum:this.skuNum} 】

src\router\routes.js  **addcartsuccess**

```js
import AddCartSuccess from '@/pages/AddCartSuccess'


// 购物车添加成功
  {
    path:'/addcartsuccess',
    name:"addcartsuccess",
    component: AddCartSuccess,
    meta:{show:true}
  },
```



src\pages\AddCartSuccess\index.vue

```vue
<template>
  <div class="cart-complete-wrap">
    <div class="cart-complete">
      <h3><i class="sui-icon icon-pc-right"></i>商品已成功加入购物车！</h3>
      <div class="goods">
        <div class="left-good">
          <div class="left-pic">
            <!-- <img src="good.skuDefaultImg"> -->
            <img :src="skuInfo.skuDefaultImg">
          </div>
          <div class="right-info">
            <!-- <p class="title">小米红米 Redmi note8 手机 梦幻蓝 全网通(4GB+64GB)</p> -->
            <p class="title">{{skuInfo.skuName}}</p>
            <!-- <p class="attr">颜色：WFZ5099IH/5L钛金釜内胆 数量：2</p> -->
            <p class="attr">{{skuInfo.skuDesc}} {{$route.query.skuName}}</p>
          </div>
        </div>
        <div class="right-gocart">
          <router-link class="sui-btn btn-xlarge" :to="`/detail/${skuInfo.id}`">查看商品详情</router-link>
          <!-- <a href="javascript:" >去购物车结算 > </a> -->
          <router-link to="/shopcart" >去购物车结算 > </router-link>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'AddCartSuccess',
    computed:{
      skuInfo(){
        return JSON.parse(sessionStorage.getItem("SKUINFO"))
      }
    }
  }
</script>
```



### 加入购物车页面点击查看购物车按钮

---

因为上面的添加到购物车页面中<router-link to="/shopcart" >去购物车结算 > </router-link>

src\router\routes.js    **component: ShopCart,**

```js
import AddCartSuccess from '@/pages/AddCartSuccess'


  // 购物车展示页面
  {
    path:'/shopcart',
    component: ShopCart,
    meta:{show:true}
  },
```



src\pages\ShopCart\index.vue   **this.$store.dispatch("getCartList")**

```vue
<script>
  export default {
    name: 'ShopCart',
    mounted() {
      // 防止请求多次
      this.getData()
    },
    methods: {
      getData(){
        // 获取个人购物车数据
        this.$store.dispatch("getCartList")
      }
    },
  }
</script>
```



src\api\index.js

```
  // 获取购物车列表数据接口：/api/cart/cartList  get
  export const reqCartList = ()=>requests({url:"/cart/cartList",method:"GET"})
```



src\store\shopcart.js   **由上面的dispatch引起下面的三连环存储数据**

```js
import {reqCartList} from '@/api'

const actions = {
  // 获取购物车列表的数组
  async getCartList({commit}){
    let result = await reqCartList()
    if(result.code == 200){
      commit("GETCARTLIST")
    }
  }
}
const mutations ={
  GETCARTLIST(state,cart){
    state.cartList = cart
  }
}
const state = {
  cartList:[]
}
const getters = {}

export default{
  actions,
  mutations,
  state,
  getters
}
```



### UUID游客身份获取购物车数据

src\store\detail.js【里面的uuid_token通过一个封装的工具类获取】

 **uuid_token** : **getUUID()**

```js
const state = 
  // 应该先查出这个是对象还是数组，才能写
  goodInfo:{},
  // 游客临时身份，要不然购物车页面不知道应该显示哪个用户的购物车数据
  // 这里 加入购物车的时候，发请求的时候只能带两个参数，所以需要在请求头中添加uuid
  uuid_token:getUUID()
}
```



src\utils\uuid_token.js【封装的UUID工具类需要有返回值uuid_token】



export const **getUUID** = ()=>{

。。。。。。。。。。。。

  // 没有返回值，返回undefined
  return **uuid_token**
}

```js
// 封装一个产生UUID的工具类。
// 返回的值在src\store\detail.js使用uuid_token:getUUID()获取到uuid_token

import {v4 as uuidv4} from "uuid"

// 要生成一个随机字符串，且每次执行不能发生变化，游客身份应该持久化存储
export const getUUID = ()=>{
  // 想从本地存储获取UUID【先看一下本地存储是否有】
  let uuid_token = localStorage.getItem("UUIDTOKEN")
  // 如果没有就新生成
  if(!uuid_token){
    // 生成游客临时身份
    uuid_token = uuidv4()
    // 本地存储一次
    localStorage.setItem("UUIDTOKEN",uuid_token)
  }
  // 没有返回值，返回undefined
  return uuid_token
}
```



src\api\request.js【因为加入购物车的时候，需要知道这个哪个用户的购物车信息，但是详情给给购物车传递参数的时候只传递skuInfo和skuNum，所以选择在请求头里面添加临时游客身份】



```js
//2、配置请求拦截器(interceptors.request)
// 在发请求之前，请求拦截器可以检测到，可以在请求发出去之前做一些事情
requests.interceptors.request.use((config) => {
    //config：内主要是对请求头Header配置
    //比如添加token
    // 因为加入购物车的时候，需要知道这个哪个用户的购物车信息，但是传递的时候只传递skuInfo和skuNum
    if(store.state.detail.uuid_token){
        // 请求头添加一个字段（userTempId）:[需要和后台协商]
        config.headers.userTempId = store.state.detail.uuid_token
    }

    //开启进度条，进度条开始动
    nprogress.start();

    return config;
})
```

### 购物车动态展示数据

src\store\shopcart.js

```
const getters = {
  cartList(state){
    return state.cartList[0]||{}
  },
}
```

src\pages\ShopCart\index.vue

```
   computed:{
      ...mapGetters(["cartList"]),
      // 购物车数据
      cartInfoList(){
        return this.cartList.cartInfoList || []
      },

      // 计算购买产品的总价
      totalPrice(){
        let sum = 0;
        this.cartInfoList.forEach(item =>{
          sum += item.skuNum * item.skuPrice
        })
        return sum
      },

      // 判断底部的复选框是否勾选【全部商品都选中，就勾选】
      isAllCheck(){
        // <input class="chooseAll" type="checkbox" :checked="isAllCheck">
        // 遍历数组里面的元素，只要全部元素isChecked属性都为1 ==》真
        // 只要有一个不是1 ==》 假
        return this.cartInfoList.every(item => item.isChecked == 1)
      }
    }
```

遍历数组里面的元素，只要全部元素isChecked属性都为1 ==》真
        // 只要有一个不是1 ==》 假
        return this.cartInfoList.every(item => item.isChecked == 1)

## 修改购物车产品数量

src\pages\ShopCart\index.vue

```vue
          <li class="cart-list-con5">
            <a href="javascript:void(0)" class="mins" @click="handler('minus',-1,cart)">-</a>
            <input autocomplete="off" type="text" minnum="1" class="itxt" :value="cart.skuNum" @change="handler('change',$event.target.value*1,cart)">
            <a href="javascript:void(0)" class="plus" @click="handler('add',1,cart)">+</a>
          </li>
          
          
<script>
  export default {
     methods: {
      async handler(type,disNum,cart){
        // type：为了区分这三个元素
        // disNum形参：+ 变化量（1）   -变化量（-1）   input 最终的个数 （并不是变化量）
        // cart ：操作的是哪一个产品【身上有ID】
        // 向服务器发请求，修改数量
        // console.log("派发action，通知服务器修改个数",type,disNum,cart);
        switch (type) {
          // 加号
          case "add":
            // 带给服务器变化的量 1
            disNum = 1
            break;
          case "minus":
            // 判断产品的个数大于 1，才可以带给服务器变化的量 -1
            // 如果产品的个数小于等于1，传递给服务器的值为 0【原封不动】
            disNum = cart.skuNum > 1 ? -1 : 0 
            break;
          case "change":
            // 如果用户输入的数字是非法的【出现非数字、负数】，传递给服务器的值为 0【原封不动】
            if( isNaN(disNum) || disNum < 1){
              disNum = 0
            }else{
              // 正常情况【小数要取整】，带给服务器变化的量，用户输入进来的数字-产品的起始数字
              disNum = parseInt(disNum) - cart.skuNum
            }
            // 简写：
            // disNum = (isNaN(disNum) || disNum < 1) ? 0 : parseInt(disNum) - cart.skuNum
            break;
        }
        
        try {
          // 派发action
          await this.$store.dispatch("addOrUpdateShopCart", {skuId: cart.skuId,skuNum: disNum});
          this.getData()
        } catch (error) {
          
        }
      },
    },
  }
</script>
```



**还要使用节流：【否则，如果点击减号速度过快，是会出现商品个数不合理的情况，比如：个数小于1】**

```vue
import {throttle} from 'lodash'


<script>
  export default {
     methods: {
 // 修改商品的个数【使用节流，否则：如果点击减号速度过快，是会出现商品个数不合理的情况，比如：个数小于1】
      handler:throttle(async function(type,disNum,cart){
        // type：为了区分这三个元素
        // disNum形参：+ 变化量（1）   -变化量（-1）   input 最终的个数 （并不是变化量）
        // cart ：操作的是哪一个产品【身上有ID】
        // 向服务器发请求，修改数量
        // console.log("派发action，通知服务器修改个数",type,disNum,cart);
        switch (type) {
          // 加号
          case "add":
            // 带给服务器变化的量 1
            disNum = 1
            break;
          case "minus":
            // 判断产品的个数大于 1，才可以带给服务器变化的量 -1
            // 如果产品的个数小于等于1，传递给服务器的值为 0【原封不动】
            disNum = cart.skuNum > 1 ? -1 : 0 
            break;
          case "change":
            // 如果用户输入的数字是非法的【出现非数字、负数】，传递给服务器的值为 0【原封不动】
            if( isNaN(disNum) || disNum < 1){
              disNum = 0
            }else{
              // 正常情况【小数要取整】，带给服务器变化的量，用户输入进来的数字-产品的起始数字
              disNum = parseInt(disNum) - cart.skuNum
            }
            // 简写：
            // disNum = (isNaN(disNum) || disNum < 1) ? 0 : parseInt(disNum) - cart.skuNum
            break;
        }
        
        try {
          // 派发action
          await this.$store.dispatch("addOrUpdateShopCart", {skuId: cart.skuId,skuNum: disNum});
          this.getData()
        } catch (error) {
          
        }
      },500), 
      
          },
  }
</script>
```



## 删除购物车中的一个产品

src\api\index.js

```js
  // 删除购物车中的商品:  /api/cart/deleteCart/{skuId}   delete
  export const reqDeleteCartById = (skuId)=>requests({url:`/cart/deleteCart/${skuId}`,method:"DELETE"})
```



src\store\shopcart.js

```js
  // 删除购物车中的商品
  async deleteCartListBySkuId({commit},skuId){
    let result = await reqDeleteCartById(skuId)
    if(result.code == 200){
      return "ok"
    }else{
      return Promise.reject(new Error('fail'))
    }
  }
```



src\pages\ShopCart\index.vue

```vue
<a href="#none" class="sindelet" @click="deleteCartById(cart)">删除</a>


<script>
    methods: {
      // 删除购物车中的商品
      async deleteCartById(cart){
        try {
          await this.$store.dispatch("deleteCartListBySkuId",cart.skuId)
          // 如果删除成功，再次发请求，获取新的数据进行展示，最后不要忘记 this.getData()
          this.getData()
        } catch (error) {
          //  【失败：提示失败信息】
          alert(error.message);
        }
      }
    },
 </script>
```



## 修改产品的状态

src\api\index.js

```js
  // 切换商品选中状态: /api/cart/checkCart/{skuId}/{isChecked}  get
  export const reqUpdateCheckedById = (skuId,isChecked)=>requests({url:`/cart/checkCart/${skuId}/${isChecked}`,method:"GET"})
```



src\store\shopcart.js

```js
import {reqCartList,reqDeleteCartById,reqUpdateCheckedById} from '@/api'

const actions = {
  // 修改商品的选中状态
  async updateCheckedBySkuId({commit},{skuId,isChecked}){
    let result = await reqUpdateCheckedById(skuId,isChecked)
    if(result.code == 200){
      return 'ok'
    }else{
      return Promise.reject(new Error('fail'))
    }
  }
}
```



src\pages\ShopCart\index.vue

```
          <li class="cart-list-con1">
            <input type="checkbox" name="chk_list"  :checked="cart.isChecked == 1" @change="updateChecked(cart,$event)">
          </li>
          
          
      // 修改某个产品的勾选状态
      async updateChecked(cart,event){
        try {
          // 带给服务器的数据isChecked,不是布尔值，而是0和1
          let isChecked = event.target.checked ? "1" : "0"
          // 如果修改商品的状态成功，再次获取服务器数据getData
          await this.$store.dispatch('updateCheckedBySkuId',{skuId:cart.skuId,isChecked:isChecked})
          this.getData()
        } catch (error) {
          alert(error.message)
        }
        
      }
```



## 删除选中的商品

src\store\shopcart.js

```
  // 删除全部勾选的产品【在这里面使用dispatch，多次遍历使用deleteCartListBySkuId函数】  deleteAllCheckedCart(context)
  // context:小仓库，commit【提交mutations修改state】；getters【计算属性】；dispatch【派发action】；state【当前仓库的数据】
  deleteAllCheckedCart({dispatch,getters}){
    let PromiseAll = []
    // 获取购物车中全部被选中的产品【购物车中所有的产品，构成一个数组】
    getters.cartList.cartInfoList.forEach(item => {
      // 如果遍历购物车的产品的时候：
      // 这个产品被选中 【item.isChecked == 1】，那么派发删除这个产品的action【deleteCartListBySkuId】 ==》dispatch('deleteCartListBySkuId',item.skuId)
      // 如果这个产品没有选中 【item.isChecked ！= 1】，那么不进行操作  ==》 ''
      let promise = item.isChecked == 1 ? dispatch('deleteCartListBySkuId',item.skuId) : ''
      // 将每一次根据ID删除的商品【也就是dispatch('deleteCartListBySkuId',item.skuId)】返回的promise添加到数组中
      PromiseAll.push(promise)
    });
    // Promise.all([p1,p2,p3...]) ==> 只要全部的p1|p2|....都成功，返回结果即为成功
    // p1|p2|p3... : 每一个都是Promise对象，如果有一个promise失败，都失败；如果每一个promise成功，都成功
    //             ==> 如果有一个失败，返回即为失败的结果
    // 如果每一次【promise】都能删除成功，表示这个删除全部勾选产品的操作也已经完成
    return Promise.all(PromiseAll)
  }
```

src\pages\ShopCart\index.vue

```
<a href="#none" @click="deleteAllCheckedCart">删除选中的商品</a>


      // 删除所有勾选的产品
      async deleteAllCheckedCart(){
        try {
          // 派发一个action
          await this.$store.dispatch("deleteAllCheckedCart")
          // 再次请求获取购物车列表
          this.getData()
        } catch (error) {
          alert(error.message)
        }
      }
```





## 修改全选状态

src\pages\ShopCart\index.vue

```
      <div class="select-all">
        <input class="chooseAll" type="checkbox" :checked="isAllCheck" @change="updateAllCartChecked">
        <span>全选</span>
      </div>


      // 修改全选的选中状态
      async updateAllCartChecked(event){
        try {
          let isChecked = event.target.checked ?"1":"0"
          // 派发action
          await this.$store.dispatch('updateAllCartIsChecked',isChecked)
          this.getData()
        } catch (error) {
          alert(error.message)
        }
      }
```

src\store\shopcart.js

**item.skuId这里当时写成了this.skuId ,导致不能成功删除**

```
  // 修改全选的选中状态
  updateAllCartIsChecked({dispatch,state},isChecked){
    let PromiseAll = []
    state.cartList[0].cartInfoList.forEach(item =>{
      let promise = dispatch('updateCheckedBySkuId',{skuId:item.skuId,isChecked})
      PromiseAll.push(promise)
    })
    // 最终的返回结果
    return Promise.all(PromiseAll)
  },
```



## 总结【P80】

![image-20220502215550687](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220502215550687.png)





## 登录注册静态组件

assets ==> 放置全部组件公用的静态资源

在样式【css】中也可以使用@符号 【src别名】，切记前面需要加上~

实例：下面两个都是用到了精灵图的地方，精灵图的位置：src/assets/images/icons.png

src\pages\Login\index.vue

src\pages\Home\ListContainer\index.vue

```
url(~@/assets/images/icons.png)
```





## 注册的逻辑【表单验证先不做，最后统一处理】

注意:要先输入手机号，才能获取验证码，否则报错，也不是代码原因【低级错误】

![image-20220503093731980](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220503093731980.png)







## 验证码+部分注册功能

src\api\index.js【先注册api接口】

```js
// 注册的时候，获取验证码: /api/user/passport/sendCode/{phone}   get
  export const reqGetCode = (phone)=>requests({url:`/user/passport/sendCode/${phone}`,method:"GET"})

  // 注册用户 ： /api/user/passport/register  post
  export const reqUserRegister = (data)=>requests({url:"/user/passport/register",data:data,method:"POST"})
```



新建一个users.js小仓库的时候，需要在大仓库中注册这个模块

src\store\index.js**【一定要注册，不注册不生效】**

```js
import Vue from 'vue'
import Vuex from 'vuex'
// 需要使用插件一次
Vue.use(Vuex)

// 引入小仓库
import home from './home'
import search from './search'
import detail from './detail'
import shopcart from './shopcart'
import user from './user'

//对外暴露store的一个实例
export default new Vuex.Store({
	//实现Vuex仓库模块化开发存储数据
	modules:{
		home,
    search,
		detail,
		shopcart,
		user
	}
})
```



src\pages\Register\index.vue

- 为了方便，这里采用自动填写验证码完成后续操作【正常情况是不需要前端对验证码进行操作的】，正常也是不需要三连环的，为了能够自动填写暂时采用了
- 注册部分不需要三连环，不需要三连环,只需要返回注册成功或者失败

```vue
<template>
  <div class="register-container">
    <!-- 注册内容 -->
    <div class="register">
      <h3>注册新用户
        <span class="go">我有账号，去 <a href="login.html" target="_blank">登陆</a>
        </span>
      </h3>
      <div class="content">
        <label>手机号:</label>
        <input type="text" placeholder="请输入你的手机号" v-model="phone">
        <span class="error-msg">错误提示信息</span>
      </div>
      <div class="content">
        <label>验证码:</label>
        <input type="text" placeholder="请输入验证码" v-model="code">
        <button style="width:100px;height:38px" @click="getCode">获取验证码</button>
        <!-- <img ref="code" src="http://182.92.128.115/api/user/passport/code" alt="code"> -->
        <span class="error-msg">错误提示信息</span>
      </div>
      <div class="content">
        <label>登录密码:</label>
        <input type="password" placeholder="请输入你的登录密码" v-model="password">
        <span class="error-msg">错误提示信息</span>
      </div>
      <div class="content">
        <label>确认密码:</label>
        <input type="password" placeholder="请输入确认密码" v-model="password1">
        <span class="error-msg">错误提示信息</span>
      </div>
      <div class="controls">
        <input name="m1" type="checkbox" :checked="agree">
        <span>同意协议并注册《尚品汇用户协议》</span>
        <span class="error-msg">错误提示信息</span>
      </div>
      <div class="btn">
        <button @click="userRegister">完成注册</button>
      </div>
    </div>

    <!-- 底部 -->
    <div class="copyright">
      <ul>
        <li>关于我们</li>
        <li>联系我们</li>
        <li>联系客服</li>
        <li>商家入驻</li>
        <li>营销中心</li>
        <li>手机尚品汇</li>
        <li>销售联盟</li>
        <li>尚品汇社区</li>
      </ul>
      <div class="address">地址：北京市昌平区宏福科技园综合楼6层</div>
      <div class="beian">京ICP备19006430号
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'Register',
    data() {
      return {
        // 收集表单数据，手机号
        phone:'',
        // 验证码
        code:'',
        // 密码
        password:'',
        // 重复密码
        password1:'',
        // 默认勾选
        agree: true
      }
    },

    methods: {
      async getCode(){
        // 简单判断一下，至少有手机号的输入数据
        try {
          const {phone} = this
          // 先判断有没有手机号输入，如果没有直接报错，不会进行后面的dispatch
          phone && (await this.$store.dispatch('getCode',phone))
          // 让组件中的code值直接变为仓库中的验证码【自己填写验证码】
          this.code = this.$store.state.user.code
          // console.log(this.$store)
        } catch (error) {
          alert(error.message)
        }
      },

      async userRegister(){
        try {
          const {phone,code,password,password1} = this;
          // 手机号和验证码至少得存在，两次输入的密码需要一致
          (phone&&code&&password == password1) && await this.$store.dispatch('userRegister',{phone,code,password})
          this.$router.push('/login')
        } catch (error) {
          alert(error.message)
        }
      }
    },
  }
</script>
```

src\store\user.js

```js
import { reqGetCode ,reqUserRegister } from '@/api'

const actions = {
  // 获取验证码
  async getCode({commit},phone){
    let result = await reqGetCode(phone)
    // console.log(result);
    if(result.code == 200){
      commit('GETCODE',result.data)
      return "ok"
    }else{
      return Promise.reject(new Error('fail'))
    }
  },

  // 注册用户  ==> this.$store.dispatch('userRegister',{phone,code,password})
  async userRegister({commit},user){
    let result = await reqUserRegister(user);
    // 不需要三连环,只需要返回注册成功或者失败
    console.log(result);
    // if(result.code == 200){
    //   return 'ok'
    // }else{
    //   return Promise.reject(new Error('fail'))
    // }
  },


}
const mutations = {
  GETCODE(state,code){
    state.code = code
  }
}
const state = {
  code:''
}
const getters = {}

export default {
  actions,
  mutations,
  state,
  getters
}
```





## 用户登录

**token:** 

注册：通过数据库存储用户信息【名字，密码】

登录：登陆成功的时候，后台为了区分这个用户是谁，服务器会下发一个独一无二的token【令牌：唯一的标识符】

这里的登录接口做的不完美，一般情况，登陆成功后服务器只会下发token【这里还下发了用户名和密码，是不需要的】，前台持久化存储token【带着token找服务器要用户信息进行展示】

vuex存储数据不是持久化的，一刷新会消失，



区别：

UUID是前台直接造的，token是服务器下发的





src\api\index.js

```
  // 用户登录： /api/user/passport/login   post
  export const reqUserLogin = (data)=>requests({url:"/user/passport/login",method:"POST",data})
```



点击登录的时候，需要去除表单的默认行为【@click**.prevent**="userLogin"】

**src\pages\Login\index.vue【后期发现这里的html部分没有完成，并没有进行数据绑定，所以后面获取不到登录的token】**(已做了修改)

```vue
<template>
  <div class="login-container">
    <!-- 登录 -->
    <div class="login-wrap">
      <div class="login">
        <div class="loginform">
          <ul class="tab clearFix">
            <li>
              <a href="##" style="border-right: 0;">扫描登录</a>
            </li>
            <li>
              <a href="##" class="current">账户登录</a>
            </li>
          </ul>

          <div class="content">
            <form>
              <div class="input-text clearFix">
                <span></span>
                <input type="text" placeholder="邮箱/用户名/手机号" v-model="phone">
              </div>
              <div class="input-text clearFix">
                <span class="pwd"></span>
                <input type="text" placeholder="请输入密码" v-model="password">
              </div>
              <div class="setting clearFix">
                <label class="checkbox inline">
                  <input name="m1" type="checkbox" value="2" checked="">
                  自动登录
                </label>
                <span class="forget">忘记密码？</span>
              </div>
              <!-- 组织表单默认的行为@click.prevent -->
              <button class="btn" @click.prevent="userLogin">登&nbsp;&nbsp;录</button>
            </form>

            <div class="call clearFix">
              <ul>
                <li><img src="./images/qq.png" alt=""></li>
                <li><img src="./images/sina.png" alt=""></li>
                <li><img src="./images/ali.png" alt=""></li>
                <li><img src="./images/weixin.png" alt=""></li>
              </ul>
              <router-link class="register" to="/register">立即注册</router-link>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- 底部 -->
    <div class="copyright">
      <ul>
        <li>关于我们</li>
        <li>联系我们</li>
        <li>联系客服</li>
        <li>商家入驻</li>
        <li>营销中心</li>
        <li>手机尚品汇</li>
        <li>销售联盟</li>
        <li>尚品汇社区</li>
      </ul>
      <div class="address">地址：北京市昌平区宏福科技园综合楼6层</div>
      <div class="beian">京ICP备19006430号
      </div>
    </div>
  </div>
</template>

<script>
// 测试用例：手机号99887766 密码：1
  export default {
    name: 'Login',
    data() {
      return {
        phone:'',
        password:''
      }
    },
    methods: {
      async userLogin(){
        try {
          // 登陆成功
          // 这一句话尾部的分号不能省略，否则会和下一行的括号连起来编译
          const {phone,password} = this;
          (phone&&password) && await this.$store.dispatch('userLogin',{phone,password})
          // 跳转到home首页
          this.$router.push('/home')
        } catch (error) {
          alert(error.message)
        }
      }
    },
  }
</script>

```



src\store\user.js

**commit('USERLOGIN',result.data.token)【需要写到.token】**

```
import { reqGetCode ,reqUserRegister ,reqUserLogin} from '@/api'

const actions = {
  // 用户登录
  async userLogin({commit},data){
    let result = await reqUserLogin(data)
    if(result == 200){
      commit('USERLOGIN',result.data.token)
    }else{
      return Promise.reject(new Error('fail'))
    }
  }
}

// 获取验证码
const mutations = {
// 用户登录
  USERLOGIN(state,token){
    state.token = token
  }
}
const state = {
  token:''
}
const getters = {}

export default {
  actions,
  mutations,
  state,
  getters
}
```



==**获取不到token ，是因为用户名和密码的输入框没有进行刷数据绑定【v-model】**==



## 首页获取用户（已登录）信息

先注册api

src\api\index.js

```
  // 获取用户信息【需要带着用户的token向服务器索要用户信息】 : /api/user/passport/auth/getUserInfo  get
  export const reqUserInfo = ()=>requests({url:"/user/passport/auth/getUserInfo",method:"GET"})
```

获取用户信息的三连环

src\store\user.js

```js
import { reqGetCode ,reqUserRegister ,reqUserLogin ,reqUserInfo} from '@/api'

const actions = {
  // 获取验证码
  async getCode({commit},phone){
    let result = await reqGetCode(phone)
    // console.log(result);
    if(result.code == 200){
      commit('GETCODE',result.data)
      return "ok"
    }else{
      return Promise.reject(new Error('fail'))
    }
  },

  // 注册用户  ==> this.$store.dispatch('userRegister',{phone,code,password})
  async userRegister({commit},user){
    let result = await reqUserRegister(user);
    // 不需要三连环,只需要返回注册成功或者失败
    // console.log(result);
    if(result.code == 200){
      return 'ok'
    }else{
      return Promise.reject(new Error('fail'))
    }
  },

  // 用户登录【token:唯一的标识符 —— 令牌】
  async userLogin({commit},data){
    let result = await reqUserLogin(data)
    // 服务器下发token，用户的唯一标识
    // 前台持久化存储token【带着token找服务器要用户信息进行展示】
    if(result.code == 200){
      commit('USERLOGIN',result.data.token)
      // console.log(result.data.token)
    }else{
      return Promise.reject(new Error('fail'))
    }
  },

  // 获取用户信息
  async getUserInfo({commit}){
    let result = await reqUserInfo()
    if(result.code == 200){
      commit('GETUSERINFO',result.data)
    }else{
      return Promise.reject(new Error('fail'))
    }
    // console.log(result);
  }
}

// 获取验证码
const mutations = {
  GETCODE(state,code){
    state.code = code
  },

// 用户登录
  USERLOGIN(state,token){
    state.token = token
  },

// 获取用户信息
  GETUSERINFO(state,data){
    state.userInfo = data
  }
}
const state = {
  code:'',
  token:'',
  userInfo:{}
}
const getters = {}

export default {
  actions,
  mutations,
  state,
  getters
}
```

src\pages\Home\index.vue【在首页的时候，使用dispatch获取服务器数据（如果登录，就会存在token，先在请求头中传递token,然后就能根据token获取用户信息）】

```
  mounted(){
    // 派发action ,获取floor组件的数据
    this.$store.dispatch("getFloorList")
    // 登陆成功的用户：获取用户信息在首页中展示【使用token获取用户信息，所以需要在请求头中获取到token】
    this.$store.dispatch('getUserInfo')
  },
```

src\api\request.js  【配置请求拦截器(interceptors.request)：**可以在这里获取到token**，类似的之前也在这里配置过UUID】

```
//2、配置请求拦截器(interceptors.request)
// 在发请求之前，请求拦截器可以检测到，可以在请求发出去之前做一些事情
requests.interceptors.request.use((config) => {
    //config：内主要是对请求头Header配置
    //比如添加token
    // 因为加入购物车的时候，需要知道这个哪个用户的购物车信息，但是传递的时候只传递skuInfo和skuNum
    if(store.state.detail.uuid_token){
        // 请求头添加一个字段（userTempId）:[需要和后台协商]
        config.headers.userTempId = store.state.detail.uuid_token
    }

    // 需要携带token带给服务器
    if(store.state.user.token){
        config.headers.token = store.state.user.token
    }

    //开启进度条，进度条开始动
    nprogress.start();

    return config;
})
```

src\components\Header\index.vue【修改上边栏的样式：如果能够成功登录（获取到用户的token），就显示用户名称；如果没有登录，就显示前往登录的内容】

```vue
        <div class="loginList">
          <p>尚品汇欢迎您！</p>
          <!-- 没有用户名 -->
          <p v-if="!userName">
            <span>请</span>
            <!-- 声明式导航：务必要有to属性 ,可以加class修饰-->
            <router-link to="/login">登录</router-link>
            <router-link to="/register" class="register">免费注册</router-link>
          </p>
          <!-- 有用户名 -->
          <p v-else>
            <a>{{userName}}</a>
            <a class="register">退出登录</a>
          </p>
        </div>
        
        
computed:{
      userName(){
        return this.$store.state.user.userInfo.name
      }
    },
        
```



## 当前存在的问题：用户的token是非持久化的【vuex非持久化】💥💥💥💥💥💥

src\store\user.js【在原来的非持久化基础上添加：localStorage.setItem('TOKEN',result.data.token)】

```

  // 用户登录【token:唯一的标识符 —— 令牌】
  async userLogin({commit},data){
    let result = await reqUserLogin(data)
    // 服务器下发token，用户的唯一标识
    // 前台持久化存储token【带着token找服务器要用户信息进行展示】
    if(result.code == 200){
      commit('USERLOGIN',result.data.token)
      // 直接持久化存储token
      // localStorage.setItem('TOKEN',result.data.token)
      // 引入封装好的token持久化工具
      setToken(result.data.token)
      // console.log(result.data.token)
    }else{
      return Promise.reject(new Error('fail'))
    }
  },
```



### 封装一个工具类token.js

==**// 这里没有使用return,导致不能获取到token**==
==**// 使得刷新一次页面就丢失用户信息**==💥💥💥💥

```
// 对外暴露一个函数
// 本地存储 持久化存储token
export const setToken = (token)=>{
  localStorage.setItem('TOKEN',token)
}

// 这里没有使用return,导致不能获取到token
// 使得刷新一次页面就丢失用户信息
export const getToken = ()=>{
  return localStorage.getItem('TOKEN')
}

export const removeToken = ()=>{
  localStorage.removeItem('TOKEN')
}
```

src\store\user.js【使用需要引入】

```
// 引入持久化token的工具类
import { setToken ,getToken } from '@/utils/token'


const state = {
  code:'',
 // token:localStorage.getItem('TOKEN'),  // 这里是获取token：如果直接写  token:' ' ,持久化不起作用
  token:getToken(),  // 这里需要封装的工具类里面有返回值才行，否则还是不会生效
  userInfo:{}
}

// 引入封装好的token持久化工具
setItem(result.data.token)
```



## 

![image-20220503180912046](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220503180912046.png)





![image-20220504140208005](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220504140208005.png)





## 组件通信6种方式

![00.组件通信6种方式](C:\Users\051129\Desktop\前端图\vue\00.组件通信6种方式.png)



## 组件间高级通信

![image-20220504180525633](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220504180525633.png)

### 【视频P114——自定义事件深入】

> https://www.bilibili.com/video/BV1Vf4y1T7bw?p=114&spm_id_from=pageDriver

![01.event自定义事件深入](C:\Users\051129\Desktop\前端图\vue\01.event自定义事件深入.png)

### v-model理解

![02.v-model原理](C:\Users\051129\Desktop\前端图\vue\02.v-model原理.png)



### sync

![03.sync原理](C:\Users\051129\Desktop\前端图\vue\03.sync原理.png)



### \$attrs 和 \$listeners

![04.$attrs 和 $listeners](C:\Users\051129\Desktop\前端图\vue\04.$attrs 和 $listeners.png)



### \$children 和 \$parent

![05.$children 和 $parent](C:\Users\051129\Desktop\前端图\vue\05.$children 和 $parent.png)





### 部分总结：

![06.部分总结](C:\Users\051129\Desktop\前端图\vue\06.部分总结.png)

### 插槽【slot】

两个参考讲解：[https://zhuanlan.zhihu.com/p/255241094]

> https://www.yuque.com/cessstudy/kak11d/fq1d6m#17e6a0b2

> ==**https://www.jianshu.com/p/0c9516a3be80**==
>
> 进入这三部分之前，先让还没接触过插槽的同学对什么是插槽有一个简单的概念：**插槽，也就是slot，是组件的一块HTML模板，这块模板显示不显示、以及怎样显示由父组件来决定。** 实际上，一个slot最核心的两个问题在这里就点出来了，是**显示不显示**和**怎样显示**。
>
> 由于插槽是一块模板，所以，对于任何一个组件，从模板种类的角度来分，其实都可以分为**非插槽模板**和**插槽模板**两大类。 非插槽模板指的是**html模板**，比如‘div、span、ul、table’这些，非插槽模板的显示与隐藏以及怎样显示由组件自身控制；
>
> 插槽模板是slot，它是一个空壳子，因为它的显示与隐藏以及最后用什么样的html模板显示由父组件控制。
>
> ```
> 上面一句话的意思是：如果父组件有没有在使用的子组件<child></child>里面写html,
> 【对于具名插槽来说，也就是在哪个标签里面写  slot = "子组件中定义的插槽name"】
> 【对于作用域插槽来说，也就是在<template>标签 { 注意：一定是<template>标签 } 里面写  （scope = "随便取一个名称sign"），父组件中使用的时候需要使用 （sign.子组件里面传递过来的数据名称）】
> 如果没有写，则是不会显示子组件的部分。【子组件自身可能有样式，比如slot之上还有一行<h3>这里是子组件</h3>】
> 
> <child>
>    html模板
> </child>
> ```
>
> **但是插槽显示的位置却由子组件自身决定，slot写在组件template的什么位置，父组件传过来的模板将来就显示在什么位置**。
>
> ```
> 上面的一句话的意思是：子组件内部的样式，slot之外的其余部分的样式，由子组件决定
> 
> <template>
>     <div class="child">
>         <h3>这里是子组件</h3>
>         <slot></slot>
>     </div>
> </template>
> ```
>
> 

#### 个人理解：

单个插槽、默认插槽、匿名插槽：

![image-20220505142757993](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220505142757993.png)







![image-20220505142744303](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220505142744303.png)





作用域插槽：
注意:关于样式,既可以写在父组件中,解析后放入子组件插槽;也可以放在子组件中,传给子组件再解析

![image-20220505142907796](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220505142907796.png)



# 报错修改

**谷歌和火狐的控制台显示有区别，**



**控制台报错：**自“http://localhost:8080/search/css/reset.css”的资源已被阻止,因为 MIME 类型（“text/html”）不匹配（X-Content-Type-Options: nosniff) 解决办法。

> 参考链接： https://blog.csdn.net/sttttttuttering/article/details/120586828
>
> ![在这里插入图片描述](https://img-blog.csdnimg.cn/9acb606ac9394aba9a0279280a6deff0.png)







<a href="javascript:void(0)" class="mins" @click="handler('minus',-1,cart)">-</a>

![image-20220502180228199](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220502180228199.png)





Vuex unknown action type 报错

> https://zhuanlan.zhihu.com/p/370292945

这是在注册store/users.js的时候。没有在大仓库中引用小仓库，导致找不到小仓库的模块







**_this2 xxx is not a function**

**做注册功能的时候【这边丢失一个分号，好像：会导致this和下一行连接】**

**刚开始写的是const {phone,code,password,password1} = this【末尾没有加上分号】**

**const {phone,code,password,password1} = this ==;== **

```
async userRegister(){
        try {
          const {phone,code,password,password1} = this;
          // 手机号和验证码至少得存在，两次输入的密码需要一致
          (phone&&code&&password == password1) && await this.$store.dispatch('userRegister',{phone,code,password})
          this.$router.push('/login')
        } catch (error) {
          alert(error.message)
        }
      }
```


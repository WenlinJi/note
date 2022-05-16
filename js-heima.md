![image-20220331095311921](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220331095311921.png)



# 补充的学习内容

- **JavaScript基础之对象与内置对象(三)：**https://blog.csdn.net/Augenstern_QXL/article/details/119250137

- **变量提升：**https://www.jianshu.com/p/24973b9db51a

- **JS中的arguments参数：**https://blog.csdn.net/zjy_android_blog/article/details/80934042

- **JavaScript中原型对象的彻底理解：**https://blog.csdn.net/u012468376/article/details/53121081

- **对象原型 - 学习 Web 开发 MDN：**https://developer.mozilla.org/zh-CN/docs/Learn/JavaScript/Objects/Object_prototypes#%E5%9F%BA%E4%BA%8E%E5%8E%9F%E5%9E%8B%E7%9A%84%E8%AF%AD%E8%A8%80%EF%BC%9F

  

# 黑马----原型链

> https://www.bilibili.com/video/BV1zz411q7j3?p=37&spm_id_from=pageDriver
>

P25实例成员和静态成员

实例成员：构造函数内部通过this添加的

静态成员：在构造函数本身上添加的

![image-20220329173427458](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220329173427458.png)

![image-20220329171032701](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220329171032701.png)



##   04.对象原型_ _ proto _ _.html

```html
    <script>
        function Star(name) {
            this.name = name;
        }
        Star.prototype.sing = function() {
            console.log(this.name + 'sing a song');
        }
        var adele = new Star("阿黛尔")
        var wf = new Star('王菲')
        console.log(adele);
        adele.sing()
        console.log(adele.__proto__ === Star.prototype);
        console.log(adele.__proto__ === wf.__proto__);
        // 系统会为每一个对象添加一个__proto__属性， 该属性指向的是构造函数的原型对象
        // 通过实例对象调用方法时的查找规则：
        // 1.先去对象本身查看是否存在该函数
        // 2.如果不存在则去__proto__属性上查找，即构造函数的原型对象身上

        // 对象原型与原型对象：
        // 原型对象是指 构造函数的原型对象Star.prototype
        // 对象原型是指 创建出来的每一个对象身上，都有一个__proto__属性，该属性被称为对象原型
    </script>
```



![image-20220329171047781](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220329171047781.png)



##   05.原型constructor.html

```html
    <script>
      function Star(name) {
        this.name = name;
      }
      // Star.prototype.sing = function() {
      //         console.log(this.name + 'sing a song');
      // }

      // 2.若为构造函数的原型对象赋值为一个新的对象，则会覆盖掉原来的constructor属性
      // 3.为了能查看到原型对象所依赖的构造函数，必须手动为原型对象添加constructor属性
      Star.prototype = {
        constructor: Star,
        sing: function () {
          console.log(this.name + "sing a song");
        },
      };
      var adele = new Star("阿黛尔");
      console.log(Star.prototype);
      // 1.默认情况下构造函数的原型对象上都有一个constructor属性，该属性指回了原构造函数
      console.log(adele.__proto__.constructor);

      // 总述：♥构造函数、原型对象、实例之间的三角关系
      // 1.构造函数通过prototype属性指向原型对象
      // 2.原型对象上的constructor属性又指回了构造函数
      // 3.实例对象通过__proto__属性指向了原型对象，还可以通过__prototype.constructor指向构造函数
    </script>
```



##   06.原型链.html



![image-20220329171039652](C:\Users\051129\AppData\Roaming\Typora\typora-user-images\image-20220329171039652.png)

```html
    <script>
        function Star(name) {
            this.name = name
        }
        Star.prototype = {
            constructor: Star,
            sing: function() {
                console.log(this.name + 'sing a song');
            }
        }
        var adele = new Star('阿黛尔')
        console.log(Star.prototype);
        // 构造函数的原型对象的__proto__指向了Object的原型对象
        console.log(Star.prototype.__proto__ === Object.prototype); //true
        console.log(Object.prototype);
        // Object的原型对象的__proto__指向为null
        console.log(Object.prototype.__proto__); //null


        // ♥每一个对象都有一个__proto__属性。
        // ♥原型链：(附件：原型链.jpg)
        // 1.实例对象的__proto__指向了构造函数的原型对象
        // 2.构造函数的原型对象的__proto__指向了Object的原型对象
        // 3.Object的原型对象的__proto__指向为null
    </script>
```



```html

```



```html
```



```html

```



- 

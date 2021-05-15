```js
    function A() {
        this.name = name
    }
    A.prototype.name = 'xiaoming'
    var a = new A()
    console.log(a.name)
```

上面例子的 A中在初始化的时候，获取不到 
```js
  this.name = name;
```
中的右侧的 name 没有定义，直接报错：
```js
   Uncaught ReferenceError: name is not defined
```  
如果想要使用 A.prototype.name = 'xiaoming';
让实例继承的话，需要改动 A 中的代码：
```js
  function A() {
    this.name = this.name ? this.name : "";
  }
```
+ 在实例化的时候获取原型链上的 **name** ，如果获取不到就赋值为空字符串

或者：
```js
    function A(name = '123'){
        this.name = name;
    }
```   
+ 设置**name**的默认值，让程序不报错，在实例化的时候传入 **name** 的参数
+  **a.name = '123'**


以上问题可以延伸出：**prototype** 与 **\_\_proto\_\_**
+ **prototype**: （显式原型 explicit prototype property：）
  + 每一个函数在创建之后都会拥有一个名为**prototype**的属性，这个属性指向函数的原型对象。



+ **\_\_proto\_\_**: (隐式原型 implicit prototype link：)
  + JavaScript中任意对象都有一个内置属性**prototype**，在ES5之前没有标准的方法访问这个内置属性，但是大多数浏览器都支持通过**\_\_proto\_\_**来访问。
  + ES5中有了对于这个内置属性标准的Get方法Object.getPrototypeOf().
  + 注意⚠️: Object.prototype 这个对象是个例外，它的**\_\_proto\_\_**值为null
    
+ 结合上述 A && a 的例子：
  + a.name = "123": 这个是a实例的时候A中name的默认值，找到了属性值，则停止了继续在原型链上继续寻找该属性值
  + 如果 A.**prototype**.test = "123"; 访问 a.test 的时候则会是 "123"，因为A中找不到该属性值继续在原型链上寻找，并找到了 a.**\_\_proto\_\_**.test = "123";则输出改属性值。


可以由以上的例子，引出 js 的**继承**的概念
> + 继承的概念
<font color=red>我是红色</font>

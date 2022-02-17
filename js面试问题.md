#### New 关键字执行过程
```js
    function Persion(name,age){
        this.name = name;
        this.age = age;
    }
    var p = new Persion('lixl',12);
    //{name:'lixl',age:12}
    // 4步
    // 创建obj对象
    var obj = new Object();
    // 吧obj的proto执行构造函数的prototype对象，实现继承
    obj.__proto__= Function.prototype;
    //将obj作为this上下文
    var result = Function.call(obj)
    //返回result
    if(typeof === 'object'){
        return result
    }else {
        return obj;
    }


// 自定义实现bind
    Function.prototype._bind = function(obj){
        /*首先存一个this 即以后要调用bind的func*/
        var fn = this;
        /*拿到参数，但是第一个参数是this的指向 所以需要截取*/  
        return function(){
            /*fn.apply(obj,args)*/
            /*args参数必须在前面  才能保证第一次传递的参数被保存起来*/
            fn.apply(obj)
        }
    }

```
#### 面试对象
- 继承：子继承父
- 封装：把相似的功能封装到一个方法里面实现封装
- 多态：重载（不同参数实现不同功能）、重写（重写父类的方法）
#### 原型原型链
1. 一句话：万物节对象，万物皆空（一切数据原型链尽头指向空）
2. 两个定义：
    - 原型：保存所有子对象共有属性和方法的父对象；
    - 原型链：由各级子对象的__proto__连续引用形成的结构
3. 三个属性：\__proto\__ constructor prototype
```js
    function Persion(name,age){
        this.name = name;
        this.age = age;
    }
    var p = new Persion('lixl',12);
    Persion.prototype.constructor === Persion
    // __proto_js 中所有对象都会携带 js 中内部属性
    p.__proto__ === Persion.prototype
    Persion.__proto__ === Function.prototype
    Function.prototype.__proto__ === Object.prototype
    Object.prototype.__proto__ === null;

    Function.__proto__ === Object.__proto__

    // Object.prototype === Function.prototype.__proto__
    /*
     * 
     * 挂载在函数内部的方法，实例化后会复制构造函数 的方法
     * 挂载的原型链上的不会被复制
     * 两个都可以通过实例访问
     * 一个需要访问构造函数内部的私有变量，可以定义在构造函数内部、其他都可以定义在原型链上
     * 
     * /
```
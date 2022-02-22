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

    
    Function.prototype == Function.__proto__ //true
    Object.__proto__ == Function.__proto__ //true
    Object.__proto__ == Function.prototype) //true__proto__
    /*
     * 
     * 挂载在函数内部的方法，实例化后会复制构造函数 的方法
     * 挂载的原型链上的不会被复制
     * 两个都可以通过实例访问
     * 一个需要访问构造函数内部的私有变量，可以定义在构造函数内部、其他都可以定义在原型链上
     * 
     * /
```
#### 深入浅出Object.defineProperty()
1. Object.defineProperty()的作用就是直接在一个对象上定义一个新属性，或者修改一个已经存在的属性
```js
Object.defineProperty(obj, prop, desc)
// obj 需要定义属性的当前对象
// prop 当前需要定义的属性名
// desc 属性描述符

let Person = {}
let temp = null
Object.defineProperty(Person, 'name', {
  get: function () {
    return temp
  },
  set: function (val) {
    temp = val
  }
})
```
- desc
    - configurable
        当且仅当该属性的 configurable 键值为 true 时，该属性的描述符才能够被改变，同时该属性也能从对应的对象上被删除。
        默认为 false。
    - enumerable
        当且仅当该属性的 enumerable 键值为 true 时，该属性才会出现在对象的枚举属性中。
        默认为 false。
        数据描述符还具有以下可选键值：

    - value
        该属性对应的值。可以是任何有效的 JavaScript 值（数值，对象，函数等）。
        默认为 undefined。
            - writable
        当且仅当该属性的 writable 键值为 true 时，属性的值，也就是上面的 value，才能被赋值运算符 (en-US)改变。
        默认为 false。
        存取描述符还具有以下可选键值：

    - get
        属性的 getter 函数，如果没有 getter，则为 undefined。当访问该属性时，会调用此函数。执行时不传入任何参数，但是会传入 this 对象（由于继承关系，这里的this并不一定是定义该属性的对象）。该函数的返回值会被用作属性的值。
        默认为 undefined。
    - set
        属性的 setter 函数，如果没有 setter，则为 undefined。当属性值被修改时，会调用此函数。该方法接受一个参数（也就是被赋予的新值），会传入赋值时的 this 对象。
        默认为 undefined。
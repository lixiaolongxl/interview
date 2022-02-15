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
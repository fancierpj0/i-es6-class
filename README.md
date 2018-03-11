## 源码
```
var Parent = function(){
  function Parent(){
    _classCallCheck(this,Parent);
    this.name = 'ahhh';
    return {a:100};
  };

  _createClass(Parent,[ // 第一个数组表示的是公共方法的描述
    {key:'getName',value:function(){
      return this.name;
    }}
  ],[ //描述静态的方法
    {key:'echo',value:function(){
      console.log('我是父类的静态方法');
    }}
  ]);

  return Parent;
}(); //此时var Parent已经接受到返回的Parent

var Child = function(Parent){ // 表示儿子继承Parent类 class Child extends Parent
  _inherits(Child,Parent); //表示继承 儿子继承父亲
  function Child(name){ 
    _classCallCheck(this,Child); // 类的调用检查
    let ret = this;
    let obj = Object.getPrototypeOf(Child).call(this);  //继承父类的私有方法 //Child.__proto___ //如果没有指向 则指向 fn(Fn的原型)
    if(typeof obj === 'object'){ //如果是对象，应把obj作为实例返回
      ret = obj;
      // 还可以在这里进行一些子类的其它私有属性和方法的挂载 ret.a  ret.b  ...
    }else{
      // 还可以在这里进行一些子类的其它私有属性和方法的挂载 ret.a  ret.b  ...
    }
    return ret;
  }
  return Child;
}(Parent); //此时var Child已经接受到返回的Child

function _classCallCheck(instance,constructor){ //检查当前类 有没有使用new
  if(!(instance instanceof constructor)) throw Error('Without new');
}

function _inherits(subCon,superCon){
  // 子类继承父类的公有方法
  subCon.prototype = Object.create(superCon.prototype,{constructor:{value:subCon}}); 
  // 也要让子类继承父类的静态方法
  subCon.__proto__ = superCon;
}

function defineProperties(target,properties){
	var conf = {configurable:true,writable:true,enumerable:true}
	for(var i=0;i<properties.length;++i){
    	conf.value = properties[i].value;
    	Object.defineProperty(target,properties[i].key,conf);
    }
}

function _createClass(con,protoProperty,staticProperty){
  if(protoProperty){
    defineProperties(con.prototype,protoProperty);
  }
  if(staticProperty){
    defineProperties(con,staticProperty);
  }
}



/**
 * 测试用例
 */

// Child(); //规定：类不能像函数一样执行
let child = new Child('ahhh');
// Child.a();
// console.log(child.getName())
console.log(child)
```

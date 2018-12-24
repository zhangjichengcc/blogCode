---
title: 'js构造函数'
date: 2018-10-09 16:53:48
categories: '笔记'
toc: true
banner: /blog/2018/10/09/js构造函数/banner.jpg
tags:
	- js
---


前言：上篇文章（发布在我的segmentfault上）介绍了js中通过构造函数来实例化对象的各种方法[js构造函数][1]，这篇文章主要介绍构造函数的继承（类的继承），同样包括 ES5 和 ES6 两部分的介绍，能力所限，文中难免有不合理或错误的地方，还望批评指正~

<!-- more -->

### 原型
首先简单介绍一下实例属性/方法 和 原型属性/方法，以便更好理解下文

``` js
function Persion(name){
  this.name = name;                         // 属性
  this.setName = function(nameName){        // 实例方法
    this.name = newName;
  }
}
Persion.prototype.sex = 'man';              // 向 Persion 原型中追加属性（原型方法）

var persion = new Persion('zhang');         // 此时我们实例化一个persion对象，看一下name和sex有什么区别
```

通过 prototype 添加的属性将出现在实例对象的原型链中，

>每个对象都会有一个内置 __proto__ 对象，当在当前对象中找不到属性的时候就会在其原型链中查找（即原型链）

我们再来看下面的例子

>**注意**：在构造函数中，一般很少有数组形式的引用属性，大部分情况都是：基本属性 + 方法。

``` js
function Animal(n) {                      // 声明一个构造函数
  this.name = n;             					    // 实例属性
  this.arr = [];                          // 实例属性（引用类型）
  this.say = function(){                  // 实例方法
    return 'hello world';
  }
}
  Animal.prototype.sing = function() {    // 追加原型方法  
  return '吹呀吹呀，我的骄傲放纵~~';
}
Animal.prototype.pArr = [];               // 追加原型属性（引用类型）
```

接下来我们看一下实例属性/方法 和 原型属性/方法的区别

>原型对象的用途是为每个实例对象存储共享的方法和属性，它仅仅是一个普通对象而已。并且所有的实例是共享同一个原型对象，因此有别于实例方法或属性，原型对象仅有一份。而实例有很多份，且实例属性和方法是独立的。


``` js
var cat = new Animal('cat');               // 实例化cat对象
var dog = new Animal('dog');	             // 实例化狗子对象

cat.say === dog.say                        // false 不同的实例拥有不同的实例属性/方法
cat.sing === dog.sing                      // true 不同的实例共享相同的原型属性/方法

cat.arr.push('zz');                        // 向cat实例对象的arr中追加元素；（私有）
cat.pArr.push('xx');                       // 向cat原型对象的pArr中追加元素；（共享）
console.log(dog.arr);                      // 打印出 []，因为cat只改变了其私有的arr
console.log(dog.pArr);                             // 打印出 ['xx'], 因为cat改变了与狗子（dog）共享的pArr
```

当然，原型属性为基本数据类型，则不会被共享
在构造函数中：为了属性(实例基本属性)的私有性、以及方法(实例引用属性)的复用、共享。我们提倡：
1、将属性封装在构造函数中
2、将方法定义在原型对象上

### ES5继承方式

首先，我们定义一个Animal父类

``` js
function Animal(n) {          					
  this.name = n;                            // 实例属性
  this.arr = [];                            // 实例属性（引用类型）
  this.say = function(){                    // 实例方法
    return 'hello world';
  }
}
Animal.prototype.sing = function() {        // 追加原型方法  
  return '吹呀吹呀，我的骄傲放纵~~';
}
Animal.prototype.pArr = [];                 // 追加原型属性（引用类型）
```

#### 原型链继承

``` js
function Cat(n) {
  this.cName = n;
}
Cat.prototype = new Animal();                // 父类的实例作为子类的原型对象

var tom = new Cat('tom');                    // 此时Tom拥有Cat和Animal的所有实例和原型方法/属性，实现了继承
var black = new Cat('black');

tom.arr.push('Im tom');
console.log(black.arr);                      // 打印出 ['Im tom'], 结果其方法变成了共享的，而不是每个实例所私有的，这是因为父类的实例方法/属性变成了子类的原型方法/属性了；
```

优点: 实现了子对象对父对象的实例 方法/属性 和 原型方法/属性 的继承；
缺点: 子类实例共享了父类构造函数的引用数据类型属性。

#### 借用构造函数

``` js
function Cat(n) {
  this.cName = n;                     
  Animal.call(this, this.cName);             // 核心，把父类的实例方法属性指向子类
}

var tom = new Cat('tom');                    // 此时Tom拥有Cat和Animal的所有实例和原型方法/属性，实现了继承
var black = new Cat('black');

tom.arr.push('Im tom');
console.log(black.arr);                      // 打印出 [], 其方法和属性是每个子类实例所私有的；
tom.sing();                                  // undefind 无法继承父类的原型属性及方法；
```

优点: 
1、实现了子对象对父对象的实例 方法/属性 的继承，每个子类实例所继承的父类实例方法和属性都是其私有的；
2、 创建子类实例，可以向父类构造函数传参数；
缺点: 子类实例不能继承父类的构造属性和方法；

#### 组合继承

``` js
function Cat(n) {
  this.cName = n;                     
  Animal.call(this, this.cName);              // 核心，把父类的实例方法属性指向子类
}
Cat.prototype = new Parent()                  // 核心, 父类的实例作为子类的原型对象
Cat.prototype.constructor = Cat;              // 修复子类Cat的构造器指向，防止原型链的混乱

tom.arr.push('Im tom');
console.log(black.arr);                       // 打印出 [], 其方法和属性是每个子类实例所私有的；
tom.sing();                                   // 打印出 '吹呀吹呀，我的骄傲放纵~~'; 子类继承了父类的原型方法及属性
```

优点: 
1、创建子类实例，可以向父类构造函数传参数；
2、父类的实例方法定义在父类的原型对象上，可以实现方法复用；
3、不共享父类的构造方法及属性；
缺点: 调用了2次父类的构造方法

#### 寄生组合继承

``` js
function Cat(n) {
  this.cName = n;                     
  Animal.call(this, this.cName);                       // 核心，把父类的实例方法属性指向子类
}
Cat.prototype = Parent.prototype;                      // 核心, 将父类原型赋值给子类原型（子类原型和父类原型，实质上是同一个）
Cat.prototype.constructor = Cat;                       // 修复子类Cat的构造器指向，防止原型链的混乱

tom.arr.push('Im tom');
console.log(black.arr);                                // 打印出 [], 其方法和属性是每个子类实例所私有的；
tom.sing();                                            // 打印出 '吹呀吹呀，我的骄傲放纵~~'; 子类继承了父类的原型方法及属性
tom.pArr.push('publish');                              // 修改继承于父类原型属性值 pArr;
console.log(black.pArr);                               // 打印出 ['publish'], 父类的原型属性/方法 依旧是共享的，
// 至此简直是完美呀~~~ 然鹅！
Cat.prototype.childrenProp = '我是子类的原型属性！';
var parent = new Animal('父类');
console.log(parent.childrenProp);                      // 打印出'我是子类的原型属性！' what? 父类实例化的对象拥有子类的原型属性/方法，这是因为父类和子类使用了同一个原型
```

优点: 
1、创建子类实例，可以向父类构造函数传参数；
2、子类的实例不共享父类的构造方法及属性；
3、只调用了1次父类的构造方法；
缺点: 父类和子类使用了同一个原型，导致子类的原型修改会影响父类；

#### 寄生组合继承（简直完美）

``` js
function Cat(n) {
  this.cName = n;                     
  Animal.call(this, this.cName);                        // 核心，把父类的实例方法属性指向子类；
}
var F = function(){};                                   // 核心，利用空对象作为中介；
F.prototype = Parent.prototype;                         // 核心，将父类的原型赋值给空对象F；
Cat.prototype = new F();                                // 核心，将F的实例赋值给子类；
Cat.prototype.constructor = Cat;                        // 修复子类Cat的构造器指向，防止原型链的混乱；
tom.arr.push('Im tom');
console.log(black.arr);                                 // 打印出 [], 其方法和属性是每个子类实例所私有的；
tom.sing();                                             // 打印出 '吹呀吹呀，我的骄傲放纵~~'; 子类继承了父类的原型方法及属性；
tom.pArr.push('publish');                               // 修改继承于父类原型属性值 pArr；
console.log(black.pArr);                                // 打印出 ['publish'], 父类的原型属性/方法 依旧是共享的；
Cat.prototype.childrenProp = '我是子类的原型属性！';
var parent = new Animal('父类');
console.log(parent.childrenProp);                       // undefind  父类实例化的对象不拥有子类的原型属性/方法；
```

优点: 完美实现继承；
缺点:实现相对复杂


#### 附YUI库实现继承

``` js
function extend(Child, Parent) {
  var F = function(){};
  F.prototype = Parent.prototype;
  hild.prototype = new F();
  Child.prototype.constructor = Child;
  Child.uber = Parent.prototype;                          
}
// 使用
extend(Cat,Animal);
```

>`Child.uber = Parent.prototype;` 的意思是为子对象设一个uber属性，这个属性直接指向父对象的`prototype`属性。（uber是一个德语词，意思是"向上"、"上一层"。）这等于在子对象上打开一条通道，可以直接调用父对象的方法。这一行放在这里，只是为了实现继承的完备性，纯属备用性质。

### ES6继承方式

``` js
class Animal{                             // 父类
  constructor(name){                      // 构造函数
    this.name=name;
  }
  eat(){                                  // 实例方法
    return 'hello world';
  }
}
class Cat extends Animal{                 // 子类
  constructor(name){
    super(name);                          // 调用实现父类的构造函数
    this.pName = name;            
  }
  sing(){
 	 return '吹呀吹呀，我的骄傲放纵~~';
  }
}
```

[1]: https://segmentfault.com/a/1190000015343232

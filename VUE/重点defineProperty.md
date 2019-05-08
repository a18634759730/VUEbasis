## Object.defineProperty 

    Object.defineProperty 方法会直接在一个对象上定义一个新属性，或者修改一个对象的现有属性， 并返回这个对象。

> *语法
     Object.defineProperty(obj, prop, descriptor)

> *参数
    1.obj 要在其上定义属性的对象。
    2.prop 要定义或修改的属性的名称。
    3.descriptor 将被定义或修改的属性描述符。
    4.返回值 被传递给函数的对象。

> *在ES6中，由于 Symbol类型的特殊性，用Symbol类型的值来做对象的key与常规的定义或修改不同，而Object.defineProperty 是定义key为Symbol的属性的方法之一

> *属性描述符

                            |--- 1.writable 该属性为true的时候 value才能被赋值运算符改变 默认为 false
                            |
                            |--- 2.configurable 该属性为true的 该属性描述function才能被改变同时该属性也能从对应的对象上被删除  默认为 false
                            |
    Object.defineProperty---|--- 3.enumerable 当该属性为true时 该属性才能够出现在对象的枚举属性中 默认为 false
                            |  
                            |--- 4.value 该属性对应的值可以是任何有效的JavaScript值(数值,对象,函数)默认为 undefined
                            |
                            |--- 5.setter/getter 


### getter 
    一个给属性提供 getter 的方法 如果没有 getter 则为 undefined 
    当访问该属性时，该方法会被执行，方法执行时没有参数传入，但是
    会传入this对象由于继承关系，这里的this并不一定是定义该属性的
    对象

### setter
    一个给属性提供 setter 的方法，如果没有 setter 则为 undefined
    当属性值修改时，触发执行该方法。该方法将接受唯一参数,即该属性
    新的参数值
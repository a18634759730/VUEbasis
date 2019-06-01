# 理解Vue深度响应原理

## 1.问题的引入

> 为什么点击下面的button界面会出现自增？

    <div id="example-2">
        <simple-counter></simple-counter>
    </div>
    Vue.component('simple-counter', {
        template: '<button v-on:click="counter += 1">{{ counter }}</button>',
        data: function () {
            return { counter: 0 }
        }
    })
    new Vue({
        el: '#example-2'
    })

    为什么数据发生变化之后，视图就发生变化？
    本文从三个方面来理解Vue处理深度响应的原理：
    数据定义；
    数据绑定；
    数据响应；

## 2.数据的定义
  
    1.组件中定义数据{{counter}}
    2.初始化过程中，会执行observe(data, this);
    3.在observe（）过程中会将data这个对象劫持，通过Object.defineProperty将data上所有的属性绑定上getter和setter函数；
    （这是针对对象，对于数组，Vue通过改写数组的原生方法来劫持）
    4.通俗的说就是只要谁获取了counter的值就会触发getter()；要是谁改变了counter的值就会触发setter();
    比如上述代码中的button绑定{{count}}的时候一定会触发getter();如果是count的值发生改变就一定会触发setter()

## 3.数据绑定

   > 1.在页面元素button中绑定{{counter}};

   > 2.在编译过程中，针对这个button会产生一个Watcher(vm, exp, cb(newValue,oldValue)),vm是Vue对象，exp是数据绑定的数据;cb（）的逻辑是用来更新页面。

  > 3.现在的问题是如何将数据的变化和Watcher关联起来

  > 4.在这里用到了一个重要的思想就是发布订阅模式；Watcher初始化的时候会将Dep.target设置为this,也就是Watcher自己，同时会触发count的getter方法，getter里面会调用Dep的depend方法， depend方法会调用Watcher的addDep方法，addDep方法就是将Watcher自己存放在Dep的事件池里面

    class Dep {
    constructor() {
        this.id = uid++;
        this.subs = [];
    }

    addSub(sub) {
        this.subs.push(sub)
    }

    depend() {
        if (Dep.target) {
            Dep.target.addDep(this)
        }
    }

    removeSub(sub) {
        let ind = this.subs.findIndex(sub);
        this.subs.splice(ind, 1)
    }

    notify() {
        this.subs.forEach(sub => sub.update())
    }
    }
    Dep.target = null;

## 4.数据响应

    当发生点击事件的时候，count的值改变，会触发setter里面的方法，这个方法会
    调用dep.notify()；它会告知Dep的事件池里的存放的Watcher去执行它的update
    （）方法；Watcher的update()方法；这个方法里面会获取count的新的值，给它
    的回调cb()，去更新视图


## 1.如何追踪VUE的变化
  
   当你把一个普通的JavaScript对象传入Vue实列作为data选项,Vue将遍历此对象
所有的属性，并使用Object.defineProperty把这些属性全部转为 getter/setter 

   Object.defineProperty是ES5中一个无法 shim(垫片)的特性，这也就是Vue不支
持IE8以及更低版本浏览器的原因
  
   getter/setter 对用户来说是不可见的，但是在内部它们人Vue能够追踪依赖，在
属性被访问和修改时通知变更，这里需要注意的是不同浏览器在控制台打印数据对象
时对getter/setter的格式化并不同，所以建议"vue-devtools"来获取对检查数据添
加友好的用户界面

每个组件实列都对应一个watcher实列，它会在组件渲染的过程中把"接触"过的数据属性记录为依赖。之后当依赖项的setter触发是，会通知watcher,从而使它关联的组件重新渲染

## 2.检测变化的注意事项
  
受现代JavaScript的限制(而且 Object.observe 也废弃)。Vue“无法检测到对象属性的添加或删除” 由于Vue会在初始化实列是对属性执行 getter/setter 转化，所以属性必须在data对象上存在才能让Vue将它转换为响应式的

    var vm = new Vue({
        data:{
            a:1
        }
    })
    vm.a      是响应式的
    vm.b = 2  是非响应式的
  
对于已经创建的实列，Vue不允许动态添加根级别的响应式属性，但是可以使用Vue.set(Object,propertyName,value)方法

    向嵌套对象添加响应式属性
    Vue.set(vm.someObject,'b',2)
 
还有vm.$set实列方法，这也是全局Vue.set方法的别名:

     this.$set(this.someObject,'b',2)

有时你可能需要为已有对象赋值多个新属性，比如使用Object.assign() 或 _.extend() 但是，这样添加到对象上的新属性不会触发更新。在这种情况下应该用原对象与要混合进去的对象属性一起创建一个新的对象

    this.someObject = Object.assign({},this.someObjct,{a:1,b:2})

     
    
## 一.对于MVVM的理解

> MVVM是Model-View-ViewModel的缩写

  	*Model代表数据模型，也可以在Model中定义数据修改和操作的业务逻辑
  
  	*View代表UI组件，它负责将数据模型转化成UI展现出来
  
  	*ViewModel监听模型数据的改变控制视图行为，处理用户交和互简单理解就是一个同步View Model 的对象，
   	连接Model和View

  	*在MVVM架构下Model和View是没有直接联系的，而是通过ViewModel进行交互，Model和ViewModel之间的交互是
  	双向的，因此View数据的变化会同步到Model中，而Model数据的变化也会立即反应到View上。
 
  	*ViewModel是通过双向数据绑定把View层和Model层连接起来，而View和Model之间的同步工作完全是自动的，无
  	需人为干涉，因此开发者只需要关注业务逻辑不需要手动，操作DOM,不需要关注数据状态的同步问题，复杂的数据
  	状态维护完全MVVM来统一管理


## 二.VUE的生命周期
  
  	1.beforeCreate(创建前) 在数据观测和初始化事件还未开始
	2.created (创建后) 完成数据观测，属性和方法的运算，初始化事件，$el属性还没有显示出来
    3.beforeMount(载入前)在挂载开始之前被调用，相关的render函数首次被调用。
    4.mounted(载入后) 在el被创建的VM.$el替换并挂载到实列上去之后调用。
    5.beforeUpdate(更新前)在数据更新之前调用，发生在虚拟DOM重新渲染和打补丁之前
    6.updated(更新后)在由于数据更改导致的虚拟DOM重新渲染和打补丁之后调用。调用是，组件DOM已经更新所以可执行依赖于DOM的操作
    7.beforeDestroy(销毁前)在实列销毁之前调用。实列仍然可以完全可用。
    8.destroyed(销毁后)在实列销毁之后调用。调用后，所有的事件监听器会被移除，所有的子实列也会销毁

### 1.什么是VUE生命周期？

    VUE实列从创建到销毁的过程，就是生命周期。从开始创建，初始化数据，编译模块，挂载Dom->渲染，更新->渲染，销毁等一系列过程称为VUE的生命周期

### 2.vue生命周期的作用是什么

    它的生命周期中有多个事件构子，让我们在控制整个Vue实列的过程所更容易形成好的逻辑。
  
### 3.vue生命周期总共有几个阶段

    它可以总共分为8个阶段。创建前/后，载入前/后 更新前/后 销毁前/销毁后

### 4.第一次页面加载会触发哪几个构子

    会触发下面几个beforeCreate created beforeMount Mounted
  
### 5.DOM渲染在哪个周期中就已经完成了

    DOM渲染在mounted中就已经完成了。
  
## 五.Vue的路由实现：hash模式 和 history模式

### hash模式：
    在浏览器中符合"#" #以及#后面的字符字符称之为hash window.location.hash读取

#### 特点：
    hash虽然在URL中，但不被包括在HTTP请求中；用来指导浏览器动作，对服务端安全无用，hash不会重加载页面。

> hash 模式

    hash 模式下，仅 hash 符号之前的内容会被包含在请求中，如 http://www.xxx.com，因此对于后端来说，
    即使没有做到对路由的全覆盖，也不会返回 404 错误
    
> history模式：

    history采用HTML5的新特性；且提供了两个新方法：pushState（），replaceState（）可以对浏览器历史记录栈进行修改，以及popState事件的监听到状态变更

    history 模式下，前端的 URL 必须和实际向后端发起请求的 URL 一致，如 http://www.xxx.com/items/id。后端如果缺少对 /items/id 的路由处理，将返回 404 错误

## 六，Vue与Angular以及React的区别

### 1.与Angularjs的区别
> 相同点：

       都支持指令:内置指令和自定义指令；都支持过滤器 内置过滤器和自定义过滤器;都支持双向数据绑定；都不支持低端浏览器

> 不同点:

       Angularjs的学习成本高，比如增加了Dependency Injection 特性,而Vue.js本身提供的API都比较简单，直观；在性能上
       Angularjs依赖对数据做脏检查，所以watcher越多越慢; Vue.js使用基于依赖追踪的观察并且使用异步队列更新，所有的
       数据都是独立触发的

### 2.与React的区别

> 相同点:

       React采用特殊的JSX语法，Vue.js在组件中开发中也推崇编写.vue特殊文件格式，对文件内容都有一些约定，两者都需要编译
    后使用;中心思想相同:一切都是组件，组件实列之间可以嵌套;都提供合理的钩子函数，可以让开发者定制化去处理需求;都不内置
    列数AJAX,route等功能到核心宝，而是一插件的方式加载:在组件开发中都支持mixins的特性

> 不同点：

       React采用的Virtual DOM会对渲染出来的结果做脏检查;Vue.js在模块中提供了指令，过滤器等可以非常方便，快捷的操作VirTual Dom。

## 七，vue路由的钩子函数

>首先可以控制导航跳转，beforeEach ,afterEach等 一般用于页面title的修好。一些需要登录才能登录才能调整页面的重定向功能。

    beforeEach 主要有3个参数to from next

    to: route 即将进入的目标路由对象,
   
    from: route 当前导航正要离开的路由

    next: function 一定要调用该方法resolve这个钩子。执行效果依赖next方法的调用参数。可以控制网页的跳转。

## 八，vuex是什么 怎么使用 那种功能场景使用它

    只用来读取的状态集中放在store中; 改变状态的方式是提交 mutations,这个同步的事物;异步逻辑应该封装在action中在main.js 引入 store 注入 新建一个目录 store ...export

> 场景有:

    单页面应用中，组件之间的状态，音乐播放，登录状态，加入购物车
  
    1.state 
        Vuex 使用单一状态树，既每个应用将仅仅包含一个store实列，单一状态树和模块化并不冲突。存放数据状态，不可以直接修改里面的数据
        
    2.mutations
        mutations定义的方法动态修改Vuex的store中的状态或者数据。
    
    3.getters
        类似Vue的计算属性，主要用来过滤一些数据。
    
    4.action
        action可以理论为通过将mutations里面处理数据的方法变成异步处理数据的方法，简单的说就是异步操作数据。view层通过store.dispath来分发 action

        const store = new Vuex.Store({ //store实例
            state: {
                count: 0
            },
            mutations: {                
                increment (state) {
                state.count++
                }
            },
            actions: { 
                increment (context) {
                context.commit('increment')
                }
            }
        })

    5.modules
       项目特别复杂的时候，可以让每一个模块拥有自己的state,mutation,action getters，使得结构非常清晰，方便管理

    const moduleA = {
        state:{},
        mutations:{},
        actions:{},
	    getters:{}
    } 

    const moduleB = {
	    state:{},
	    mutations:{},
	    actions:{}
    } 

    const store = mew Vuex.Store({
        modules:{
            a:moduleA,
                b:moduleB
        }
    })

          
    
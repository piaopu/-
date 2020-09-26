
### 双向绑定原理
vue.js 是采用数据劫持结合发布者-订阅者模式的方式，通过 Object.defineProperty()来劫持各个属性的 setter，getter，在数据变动时发布消息给订阅者，触发相应的监听回调。

具体步骤：  
第一步：需要 observe 的数据对象进行递归遍历，包括子属性对象的属性，都加上 setter 和 getter 这样的话，给这个对象的某个值赋值，就会触发 setter，那么就能监听到了数据变化  

第二步：compile 解析模板指令，将模板中的变量替换成数据，然后初始化渲染页面视图，并将每个指令对应的节点绑定更新函数，添加监听数据的订阅者，一旦数据有变动，收到通知，更新视图  

第三步：Watcher 订阅者是 Observer 和 Compile 之间通信的桥梁，主要做的事情是:

+ 在自身实例化时往属性订阅器(dep)里面添加自己
+ 自身必须有一个 update()方法
+ 待属性变动 dep.notice()通知时，能调用自身的 update() 方法，并触发 Compile 中绑定的回调，则功成身退。

第四步：MVVM 作为数据绑定的入口，整合 Observer、Compile 和 Watcher 三者，通过 Observer 来监听自己的 model 数据变化，通过 Compile 来解析编译模板指令，最终利用 Watcher 搭起 Observer 和 Compile 之间的通信桥梁，达到数据变化 -> 视图更新；视图交互变化(input) -> 数据 model 变更的双向绑定效果。

### Vue与React的区别
- 监听数据变化的实现原理不同
- 数据流的不同
- HoC和mixins
- 组件通信的区别
- 模板渲染方式的不同
- 渲染过程不同
- 框架本质不同
- Vuex和Redux的区别

详细 https://blog.csdn.net/qq_26190177/article/details/93741368

### 父子间组件通信及跨组件间通信

#### 父子间组件通信
- 父级->子级通信 (依赖单向数据绑定+props实现)

- 子级 -> 父级通信 (依赖自定义事件)
 和父子通信依靠props属性不同，在子父通信中我们需要使用自定义事件的方法。  
 Vue中的自定义事件，不同于点击事件、监听事件等等依托一个特定媒介去触发事件内部函数方法，自定义事件依靠this.$emit()触发事件

#### 非父子组件之间的通信
+ 通过ref链实现 不推荐使用
在Vue实例对象下有一个refs属性，其内容包含了所以作用域内组件的具体信息，利用ref实现非父子组件通信的核心逻辑就是通过操作$refs作为一个中间件来进行数据交换。

+ 事件总线
因为$refs性能低下的问题，所以产生了另外一条思路：将数据托管在一个公共（全局属性）的中间件上，这样无论是不是存在父子关系都可以访问的到其内部的数据。
 - 全局定义一个公共的Vue实例对象bus，用于存储数据

 - 利用自定义事件发布和触发，实现通信

详细 https://blog.csdn.net/sanbeisuk/article/details/101419638

------------


### computed与watch的区别
#### 计算属性computed
1. 支持缓存，只有依赖数据发生改变，才会重新进行计算
2. 不支持异步，当computed内有异步操作时无效，无法监听数据的变化
3. computed 属性值会默认走缓存，计算属性是基于它们的响应式依赖进行缓存的，也就是基于data中声明过或者父组件传递的props中的数据通过计算得到的值
4. 如果一个属性是由其他属性计算而来的，这个属性依赖其他属性，是一个多对一或者一对一，一般用computed
5. 如果computed属性属性值是函数，那么默认会走get方法；函数的返回值就是属性的属性值；在computed中的，属性都有一个get和一个set方法，当数据变化时，调用set方法。

#### 侦听属性watch：
1. 不支持缓存，数据变，直接会触发相应的操作；
2. watch支持异步；
3. 监听的函数接收两个参数，第一个参数是最新的值；第二个参数是输入之前的值；
4. 当一个属性发生变化时，需要执行对应的操作；一对多；
5. 监听数据必须是data中声明过或者父组件传递过来的props中的数据，当数据变化时，触发其他操作，函数有两个参数
 - immediate：组件加载立即触发回调函数执行
 - deep: 深度监听，为了发现对象内部值的变化，复杂类型的数据时使用，例如数组中的对象内容的改变，注意监听数组的变动不需要这么做。注意：deep无法监听到数组的变动和对象的新增，参考vue数组变异,只有以响应式的方式触发才会被监听到。

### v-bind 和 v-model 的区别
1. v-bind 用来绑定数据和属性以及表达式，缩写为`:`
2. v-model 使用在表单中，实现双向数据绑定的，在表单元素外使用不起作用

### v-if与v-show的区别
1. v-if和v-show用于视图层进行条件判断视图展示

2. v-if的原理是根据判断条件来动态的进行增删DOM元素，v-show是根据判断条件来动态的进行显示和隐藏元素，频繁的进行增删DOM操作会影响页面加载速度和性能，由此我们可以得出结论：
  - 当您的项目程序不是很大的时候，v-if和v-show都可以用来进行判断展示和隐藏（这种场景使用v-if只是影响不大，并不是没有影响）；
  - 当您的项目程序比较大的时候，不推荐使用v-if来进行判断展示和隐藏，推荐使用v-show；

3. 只有v-if能和v-else连用进行分支判断，v-show是不能和v-else连用的，如果出现多种条件场景的情况下，可以使用v-if来进行判断


### vue 的优点是什么？
+ 低耦合。
视图（View）可以独立于 Model 变化和修改，一个 ViewModel 可以绑定到不同的"View"上，当 View 变化的时候 Model 可以不变，当 Model 变化的时候 View 也可以不变。

+ 可重用性
你可以把一些视图逻辑放在一个 ViewModel 里面，让很多 view 重用这段视图逻辑。

+ 独立开发
开发人员可以专注于业务逻辑和数据的开发（ViewModel），设计人员可以专注于页面设计，使用 Expression Blend 可以很容易设计界面并生成 xml 代码。
可测试。界面素来是比较难于测试的，而现在测试可以针对 ViewModel 来写。

### vue实例的生命周期
+ 什么是生命周期：从Vue实例创建、运行、到销毁期间，总是伴随着各种各样的事件，这些事件，统称为生命周期
+ 生命周期钩子：就是生命周期事件的别名而已
+ 生命周期钩子 = 生命周期函数 = 生命周期事件
+ 主要的生命周期函数分类：
 - 创建期间的生命周期函数：
      + beforeCreate：实例刚在内存中被创建出来，此时，还没有初始化好 data 和 methods 属性
      + created：实例已经在内存中创建OK，此时 data 和 methods 已经创建OK，此时还没有开始 编译模板
      + beforeMount：此时已经完成了模板的编译，但是还没有挂载到页面中
      + mounted：此时，已经将编译好的模板，挂载到了页面指定的容器中显示
 - 运行期间的生命周期函数：
     + beforeUpdate：状态更新之前执行此函数， 此时 data 中的状态值是最新的，但是界面上显示的 数据还是旧的，因为此时还没有开始重新渲染DOM节点
     + updated：实例更新完毕之后调用此函数，此时 data 中的状态值 和 界面上显示的数据，都已经完成了更新，界面已经被重新渲染好了！
 - 销毁期间的生命周期函数：
     + beforeDestroy：实例销毁之前调用。在这一步，实例仍然完全可用。
     + destroyed：Vue 实例销毁后调用。调用后，Vue 实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁。 






------------



### Vuex相关
1. vuex 有哪几种属性
 有 5 种，分别是 state、getter、mutation、action、module

2. vuex 的 store 特性是什么
 - vuex 就是一个仓库，仓库里放了很多对象。其中 state 就是数据源存放地，对应于一般 vue 对象里面的 data
 - state 里面存放的数据是响应式的，vue 组件从 store 读取数据，若是 store 中的数据发生改变，依赖这相数据的组件也会发生更新
 - 它通过 mapState 把全局的 state 和 getters 映射到当前组件的 computed 计算属性

3. vuex 的 getter 特性是什么
 - getter 可以对 state 进行计算操作，它就是 store 的计算属性
 - 虽然在组件内也可以做计算属性，但是 getters 可以在多给件之间复用
 - 如果一个状态只在一个组件内使用，是可以不用 getters

4. vuex 的 mutation action 特性是什么

 -  action 类似于 muation, 不同在于：action 提交的是 mutation,而不是直接变更状态
 -  action 可以包含任意异步操作

5. vue 中 ajax 请求代码应该写在组件的 methods 中还是

  - 如果请求来的数据不是要被其他组件公用，仅仅在请求的组件内使用，就不需要放入 vuex 的 state 里
 -  如果被其他地方复用，请将请求放入 action 里，方便复用，并包装成 promise 返回

6. 不用 vuex 会带来什么问题

 -  可维护性会下降，你要修改数据，你得维护 3 个地方
 -  可读性下降，因为一个组件里的数据，你根本就看不出来是从哪里来的
 -  增加耦合，大量的上传派发，会让耦合性大大的增加，本来 Vue 用 Component 就是为了减少耦合，现在这么用，和组件化的初衷相背

7. vuex 原理

  - vuex 仅仅是作为 vue 的一个插件而存在，不像 Redux,MobX 等库可以应用于所有框架，vuex 只能使用在 vue 上，很大的程度是因为其高度依赖于 vue 的 computed 依赖检测系统以及其插件系统，
 -  vuex 整体思想诞生于 flux,可其的实现方式完完全全的使用了 vue 自身的响应式设计，依赖监听、依赖收集都属于 vue 对对象 Property set get 方法的代理劫持。最后一句话结束 vuex 工作原理，vuex 中的 store 本质就是没有 template 的隐藏着的 vue 组件；

8. store 是如何实现注入vue
Vue.use(Vuex) 方法执行的是 install 方法，它实现了 Vue 实例对象的 init 方法封装和注入，使传入的 store 对象被设置到 Vue 上下文环境的$store 中。因此在 Vue Component 任意地方都能够通过 this.$store 访问到该 store。

9. state 内部支持模块配置和模块嵌套，如何实现的
在 store 构造方法中有 makeLocalContext 方法，所有 module 都会有一个 local context，根据配置时的 path 进行匹配。所以执行如 dispatch('submitOrder', payload)这类 action 时，默认的拿到都是 module 的 local state，如果要访问最外层或者是其他 module 的 state，只能从 rootState 按照 path 路径逐步进行访问。

10. action 执行函数中第一个参数 store 从哪里获取的？
store 初始化时，所有配置的 action 和 mutation 以及 getters 均被封装过。在执行如 dispatch('submitOrder', payload)的时候，actions 中 type 为 submitOrder 的所有处理方法都是被封装后的，其第一个参数为当前的 store 对象，所以能够获取到 { dispatch, commit, state, rootState } 等数据。

11. Vuex 如何区分 state 是外部直接修改，还是通过
Vuex 中修改 state 的唯一渠道就是执行 commit('xx', payload) 方法，其底层通过执行 this._withCommit(fn) 设置_committing 标志变量为 true，然后才能修改 state，修改完毕还需要还原_committing 变量。外部修改虽然能够直接修改 state，但是并没有修改_committing 标志位，所以只要 watch 一下 state，state change 时判断是否_committing 值为 true，即可判断修改的合法性。



------------

### vue父子组件的渲染顺序
#### 加载渲染过程
父beforeCreate->父created->父beforeMount->子beforeCreate->子created->子beforeMount->子mounted->父mounted

#### 子组件更新过程
父beforeUpdate->子beforeUpdate->子updated->父updated

#### 父组件更新过程
父beforeUpdate->父updated

#### 销毁过程
父beforeDestroy->子beforeDestroy->子destroyed->父destroyed


### Vue-Router路由

对于 Vue 这类渐进式前端开发框架，为了构建 SPA（单页面应用），需要引入前端路由系统，这也就是 Vue-Router 存在的意义。前端路由的核心，就在于 ——** 改变视图的同时不会向后端发出请求**

1. hash —— 即地址栏 URL 中的 # 符号（此 hash 不是密码学里的散列运算）。
比如这个 URL：`http://www.abc.com/#/hello`，hash 的值为 #/hello。它的特点在于：hash 虽然出现在 URL 中，但不会被包括在 HTTP 请求中，对后端完全没有影响，因此改变 hash 不会重新加载页面。
2. history —— 利用了 HTML5 History Interface 中新增的 pushState()和 replaceState()方法。（需要特定浏览器支持）这两个方法应用于浏览器的历史记录栈，在当前已有的 back、forward、go 的基础之上，它们提供了对历史记录进行修改的功能。只是当它们执行修改时，虽然改变了当前的 URL，但浏览器不会立即向后端发送请求。  

因此可以说，hash 模式和 history 模式都属于浏览器自身的特性，Vue-Router 只是利用了这两个特性（通过调用浏览器提供的接口）来实现前端路由。
详细 https://www.jianshu.com/p/3318bb674060



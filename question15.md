vue面试第十五题：
谈谈你对vuex使用及其理解？

答：vuex就是将数据共享给多个组件共同使用，同时也将这个数据的状态进行了共享（一个组件改变这个数据的状态其它组件也跟着改变）。。

vuex有五大核心属性：

1、state：存储数据，存储状态；在根实例中注册了store 后，用 `this.$store.state` 来访问；对应vue里面的data；存放数据方式为响应式，vue组件从store中读取数据，如数据发生变化，组件也会对应的更新。

2、getter：可以认为是 store 的计算属性，它的返回值会根据它的依赖被缓存起来，且只有当它的依赖值发生了改变才会被重新计算。

3、mutation：更改 Vuex 的 store 中的状态的唯一方法是提交 mutation。

4、action：包含任意异步操作，通过提交 mutation 间接更变状态。

5、module：将 store 分割成模块，每个模块都具有state、mutation、action、getter、甚至是嵌套子模块。

当组件进行数据修改的时候我们需要调用dispatch来触发actions里面的方法。actions里面的每个方法中都会有一个commit方法，当方法执行的时候会通过commit来触发mutations里面的方法进行数据的修改。mutations里面的每个函数都会有一个state参数，这样就可以在mutations里面进行state的数据修改，当数据修改完毕后，会传导给页面。页面的数据也会发生改变。


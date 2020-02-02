vue面试第十四题：
谈谈你对vue生命周期的理解？

答：从源码我们可以知道，在new Vue（）创建实例的过程中，在src\core\instance\init.js的文件中会依次执行下方代码

```js
 initLifecycle(vm) //声明$parent,$root,$children,$refs

  initEvents(vm) //对父组件传入的事件和回调添加监听

  initRender(vm) //声明$slots,$createElement()

  callHook(vm, 'beforeCreate') //调用beforeCreate钩子

  initInjections(vm) // resolve injections before data/props 注入数据

  initState(vm)  //数据的初始化，响应式

  initProvide(vm) // resolve provide after data/props 提供数据
  callHook(vm, 'created')
```

在initState(vm)的时候，进行数据初始化，实现数据响应式，以及对computed（计算属性）、watch侦听器初始化，在此之前data里的数据和methods里的方法无法操作，最早只能在created中操作

```js
if (vm.$options.el) {

   vm.$mount(vm.$options.el)

  }
```

判断是否有el属性，如果有就调用$mount，而$mount中主要是调用mountComponent，源码如下

```js
//实现$mount

*Vue*.prototype.$mount = *function* (

 *el*?: *string* | Element,

 *hydrating*?: *boolean*

): Component {

 el = el && inBrowser ? query(el) : undefined

 //初始化，将首次渲染的结果替换el

 return mountComponent(this, el, hydrating)

}
```

mountComponent中，相关的 render 函数首次被调用，有了render函数后再调用beforeMount，最后调用mounted

```js
export *function* mountComponent (

 *vm*: Component,

 *el*: ?Element,

 *hydrating*?: *boolean*

): Component {

 vm.$el = el

 if (!vm.$options.render) {

  vm.$options.render = createEmptyVNode

 }

 callHook(vm, 'beforeMount')



 *let* updateComponent

updateComponent = () *=>* {

   vm._update(vm._render(), hydrating)

  }



 // we set this to vm._watcher inside the watcher's constructor

 // since the watcher's initial patch may call $forceUpdate (e.g. inside child

 // component's mounted hook), which relies on vm._watcher being already defined

 new Watcher(vm, updateComponent, noop, {

  before () {

   if (vm._isMounted && !vm._isDestroyed) {

​    callHook(vm, 'beforeUpdate')

   }

  }

 }, true /* isRenderWatcher */)

 hydrating = false



 // manually mounted instance, call mounted on self

 // mounted is called for render-created child components in its inserted hook

 if (vm.$vnode == null) {

  vm._isMounted = true

  callHook(vm, 'mounted')

 }

 return vm

}
```



以上四个钩子函数在初始化时被调用，其他钩子的调用需要外部的触发才能执行。

当有数据的变化，会调用beforeUpdate，然后经过Virtual DOM，最后updated更新完毕。当组件被销毁的时候，它会调用beforeDestory，以及destoryed。

activated、deactivated是和vue中一个原生的组件keep-alive有关系,当keep-alive组件激活时调用activated钩子。keep-alive 组件停用时调用deactivated钩子

钩子errorCaptured是当捕获一个来自子孙组件的错误时被调用。此钩子会收到三个参数：错误对象、发生错误的组件实例以及一个包含错误来源信息的字符串。此钩子可以返回 false 以阻止该错误继续向上传播。
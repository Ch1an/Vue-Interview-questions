vue面试第二题：
1.Vue组件data选项为什么必须是个函数而Vue的根实例则没有此限制？

答：在组件中data必须是一个返回初始对象的函数，因为组件可能被用来创建多个实例。如果data直接是一个对象，则所有的实例将共享引用同一个数据对象，一个组件实例中的数据改变将会影响其他组件实例。通过函数返回，每次创建一个新实例时，我们能够调用 `data` 函数，从而返回初始数据的一个全新副本数据对象。而根实例只有一个，所以没有这个限制
第二题：

 Vue组件data选项为什么必须是个函数而Vue的根实例则没有此限制？

当一个组件被定义，data必须声明为返回一个初始数据对象的函数，因为组件可能被用来创建多个实例。如果 data仍然是一个纯粹的对象，则所有的实例将共享引用同一个数据对象，
通过提供 data函数，每次创建一个新实例后，我们能够调用 data 函数，每个函数都有自己的作用域，从而保证了各组件之间数据的独立。

而根实例只能有一个，不存在创建多个根实例的问题，也就不存在实例间数据混淆的问题。

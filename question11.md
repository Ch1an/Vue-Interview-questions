vue面试第十一题：
你知道vue3有哪些新特性吗？它们会带来什么影响？

答：1.重写虚拟DOM，速度更快

​		2.优化slots的生成，Vue2.x 中，当父组件重新渲染时，其子组件也必须重新渲染。使用Vue 3，可以单独重新渲染父级和子级。

​		3.静态树提升，使用静态树提升，这意味着 Vue 3 的编译器将能够检测到什么是静态的，然后将其提升，从而降低了渲染成本。它将能够跳过 patching 整棵树。

​		4.为了降低复杂性，对复杂性进行隔离，开发团队将一些内部功能拆分为了多个单独的包，如observer 模块将成为一个单独的包，拥有自己对外的 API 和自己的测试用例。

​		5.基于代理的观察，速度更快，内存使用量更少

​		6.更多原生的支持，运行时内核将与平台无关，使得vue可以更容易的与任何平台（ios、android、web）一起使用

​		7.源码使用TypeScript编写

​		vue3.0的更新使它在未来更具竞争力，让它在速度和内存上的优势更进一步，速度更快，体积更小，更易维护，以原生为目标更容易，让生活更轻松。
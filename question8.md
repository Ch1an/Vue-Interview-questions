vue面试第八题：
谈谈你对MVC、MVP和MVVM的理解？

答：M：Model（数据层），负责数据的请求、存储以及处理

​		V：View（UI层），主要是页面的展示和用户的交互

​        C：Controller（控制层），负责连接数据层和UI层

​		当用户在View中发起事件时，Controller会接收到该事件，根据事件的不同，可能会调用Model的接口进行数据操作，可能会进行View的跳转，这样也意味着一个controller会对应多个View，页面复杂时，整个controller层会显得很臃肿。当Model的数据更新时，不会经干Controller，而是直接通知View，通常View会采用观察者模式监听Model的变化。



MVC模式增强了代码的复用性、也降低了耦合性，提高了代码的可维护性，但是不适合简单的中小型项目，增加了系统结构和实现的复杂性，而且View和Controller并没有隔离开来，所以MVP模式应运而生。



MVP模式中，View和Model不再有任何直接关系了。Presenter处理View的业务逻辑，与View耦合，Persenter也给视图暴露接口与其通信，它将原来需要在Controller层里面处理的逻辑移到了Persenter层。但是也使得它与特定的视图的联系过于紧密。



MVVM模式相对于MVP来说，增加了数据绑定。通过对ViewModel层的封装：封装业务逻辑处理，封装网络处理、封装数据缓存等，让逻辑处理分离出来，并且不需要处理Model数据，使得结构简单，条理清晰。
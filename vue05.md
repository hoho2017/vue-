# 对MVC、MVP和MVVM的理解？

复杂的app必须有清晰合理的架构，不然无法开发和维护。

MVC,MVP和MVVM都是一种架构模式，是为了解决图形界面应用程序复杂性管理问题而产生的应用架构模式/

`MVC` ：Model（数据保存）-View（用户界面）-Controller（业务逻辑）

​			 1.View 传送指令到Controller

​			 2.Controller完成业务逻辑后，要求Model改变状态

​			 3.Model将新的数据发送到View，用户得到反馈

所有的通信都是单向的。

`MVP` ： 在MVC模式上将Controller改为Presenter，同时改变了通信方向

​			  三者的通信都是双向的，但是View和Model不发生通信，由Presenter传递

​			  大部分的逻辑都在Presenter上面

`MVVM` ： 在MVP模式上将Presenter改为ViewModel，基本和MVP模式一样

​				 唯一的区别是它是双向绑定：View变，ViewModel就变，反之亦然。


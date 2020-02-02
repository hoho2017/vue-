#### Vue生命周期

l  每个Vue实例在被创建时都要经过一系列得初始化过程，如需要设置数据监听，编译模板，将实例挂载到DOM并在数据变化时更新DOM等，称为Vue实例得生命周期。

ll created和mounted在平时使用得比较多，created为组件实例被创建但是没有挂载到DOM上，所以不能访问DOM，而mounted是实例挂载到了DOM上，所以在mounted里面可以访问DOM；初始化时组件会依次执行beforeCreate，created，beforeMount，mounted；beforeDestroy时，组件实例还存在，destroyed时实例不存在，通常用于解除绑定，销毁子组件以及事件监听器；
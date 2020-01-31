# vue如果想扩展某个现有的组件时应该怎么做

- **slot扩展**

  ```
  <body>
   <div id="itany">
   <my-hello>180812</my-hello>
   </div>
  <template id="hello">
   <div>
   <h3>welcome to xiamen</h3>
   <slot>如果没有原内容，则显示该内容</slot>// 默认插槽
   </div>
  </template>
  <script>
   var vm=new Vue({
    el:'#itany',
    components:{
    'my-hello':{
    template:'#hello'
   }
    }
   }); 
  </script>
  ```

- **mixins**

  ```
  <h1>Mixins</h1>
   <hr>
   <div id="app">
    <p>num:{{ num }}</p>
    <P>
     <button @click="add">增加数量<tton>
    </P>
   </div>
   <script type="text/javascript">
    var addLog = { //额外临时加入时，用于显示日志
     updated: function () {
      console.log("数据发生变化,变化成" + this.num + ".");
     }
    }
    Vue.mixin({// 全局注册一个混入，影响注册之后所有创建的每个 Vue 实例
     updated: function () {
      console.log("我是全局的混入")
     }
    })
    var app = new Vue({
     el: '#app',
     data: {
      num: 1
     },
     methods: {
      add: function () {
       this.num++;
      }
     },
     updated() {
      console.log("我是原生的update")
     },
     mixins: [addLog]//混入
    })
  ```

- **extends**

  ```
  <h1>Extends</h1>
  <hr>
  <div id="app">
   num:{{ num }}
   <p>
    <button @click="add">add</button>
   </p>
  </div>
  <script type="text/javascript">
   var bbb = {
    updated() {
     console.log("我是被扩展出来的");
    },
    methods: {
     add: function () { //跟原生的方法冲突，取原生的方法，这点跟混入一样
      console.log('我是被扩展出来的add方法！');
      this.num++;
     }
    }
   };
   var app = new Vue({
    el: '#app',
    data: {
     num: 1
    },
    methods: {
     add: function () {
      console.log('我是原生add方法');
      this.num++;
     }
    },
    updated() {
     console.log("我是扩展出来的");
    },
    extends: bbb// 接收对象和函数
   })
  ```

- **Vue.extend**

  ```
  <div id="itany">
   <hello></hello>
   <my-world></my-world>
  </div>
  <script>
   /**
    * 方式1：先创建组件构造器，然后由组件构造器创建组件
    */
   //1.使用Vue.extend()创建一个组件构造器
   var MyComponent = Vue.extend({
    template: '<h3>Hello World</h3>'
   });
   //2.使用Vue.component(标签名,组件构造器)，根据组件构造器来创建组件
   Vue.component('hello', MyComponent);
   /**
    * 方式2：直接创建组件(推荐)
    */
   // Vue.component('world',{
   Vue.component('my-world', {
    template: '<h1>你好，世界</h1>'
   });
   var vm = new Vue({ //这里的vm也是一个组件，称为根组件Root
    el: '#itany',
    data: {}
   }); 
  </script>
  ```
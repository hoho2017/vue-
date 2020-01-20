## v-if和v-for哪个优先级高？如果两个同时出现，应该怎么优化得到更好的性能？
- v-for的优先级要高于v-if;
- 优化:

    `<div v-if="something" v-for="item of list">{{item}}</div>`

    1. 如果v-if是要将整个列表隐藏的情况 
        - 可以在列表外套一个template或套一个盒子,然后在外层盒子进行v-if判断
    ```
        <template v-if="false">
            <div :key="item" v-for="item of list">{{item}}</div>
        </template>
    ```
    
    2. 如果v-if是要隐藏列表的某项
        - 用一个计算属性，返回过滤后的列表替换原列表。这样的好处是渲染时只遍历过滤后的列表，渲染更高效，同时解耦了渲染和数据逻辑
    
    

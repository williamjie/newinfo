vue2.0s中eventBus实现兄弟组件通信
在vue1.0中，组件之间的通信主要通过vm.$dispatch沿着父链向上传播和用vm.$broadcast向下广播来实现。然而在vue2.0中，已经废除了这种用法。

vuex加入后，对组件之间的通信有了更加清晰的操作，对于中大型的项目来说，一开始就把vuex的使用计划在内是明智的选择。

然而在一些小型的项目，或者说像我这样写到一半才发现vue2.0用不了$.broadcast和$dispatch的人来说，就需要一个比较便捷的解决方法。那么，eventBus的作用就体现出来了。

主要是现实途径是在要相互通信的兄弟组件之中，都引入一个新的vue实例，然后通过分别调用这个实例的事件触发和监听来实现通信和参数传递。

这里来看一个简单的例子：

比如，我们这里有三个组件，main.vue、click.vue、show.vue。click和show是父组件main下的兄弟组件，而且click是通过v-for在父组件中遍历在了多个列表项中。这里要实现，click组件中触发点击事件后，由show组件将点击的是哪个dom元素console出来。

首先，我们给click组件添加点击事件

1 <div class="click" @click.stop.prevent="doClick($event)"></div> 
 

想要在doClick()方法中，实现对show组件的通信，我们需要新建一个js文件，来创建出我们的eventBus，我们把它命名为bus.js

import Vue from 'vue';  
export default new Vue();
 

这样我们就创建了一个新的vue实例。接下来我们在click组件和show组件中import它。

import Bus from 'common/js/bus.js'; 
 

接下来，我们在doClick方法中，来触发一个事件：

1 methods: {  
2    addCart(event) {  
3    Bus.$emit('getTarget', event.target);   
4    }  
5 }  
 

这里我们在click组件中每次点击，都会在bus中触发这个名为'getTarget'的事件，并将点击事件的event.target顺着事件传递出去。

 

接着，我们要在show组件中的created()钩子中调用bus监听这个事件，并接收参数：

created() {  
        Bus.$on('getTarget', target => {  
            console.log(target);  
        });  
      }  
这样，在每次click组件的点击事件中，就会把event.target传递到show中，并console出来。

 

所以eventBus的使用还是非常便捷的，但是如果是中大型项目，通信比较复杂，还是建议大家直接使用vuex。

 

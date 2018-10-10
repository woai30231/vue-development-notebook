*本文档基于官方文档，详情可查看[官方文档](https://vuex.vuejs.org/zh/guide/modules.html)*

#### 为什么要模块化管理vuex

首先默认的vuex使用的是单一状态树，所以当项目越来越大的时候，所以的数据将会集中到一个非常庞大的对象上，这很难管理。其次，我们可以利用module实现vuex状态更好的封装性和复用性，并且减少命名冲突，于是模块化管理vuex显得很有必要。

#### 怎么使用module

我们看一下默认vuex是怎么用的。代码如下：

* vuex01.js
```javascript
let store = new Vuex.Store({
   actions:{
      //...
   },
   mutations:{
      demoCtrl(state,{string=""}={}){
         state.demo = string;
      }
   },
   state:{
      demo:'this is a demo'
   }
});  
```
然后我们在组建中使用state和mutations，如：

* html01.vue
```javascript
export default {
   computed:{
      //计算属性中使用state
      demo(){
         return this.$store.state.demo;
      }
   },
   mounted(){
      //改变状态
      this.$store.commit('demoCtrl',{string:'这是一个新值'});
   }
};
```
那我们再来看一下，如果用模块化的方式重新来实现一遍前面的状态数据，如：

* vuex02.js
```javascript
let moduleA = {
   actions:{
      //...
   },
   muations:{
      demoCtrl(state,{string=""}={}){
         state.demo = string;
      }
   },
   state:{
      demo:'this is a demo!'
   }
};

let store = new Vuex.Store({
   modules:{
      a:moduleA
   }
});
```
然后我们向下面这样使用，如：

* html02.vue
```javascript
export default {
   computed:{
      demo(){
         return this.$store.state.a.demo
      }
   },
   mounted(){
      //改变状态
      this.$store.commit('demoCtrl',{string="这是一个新值！"});
   }
};   
```
我们发现在用module方式的时候，除了获取状态的时候会多一个命名空间之外，其它如mutations还是跟默认方式是一样的。其实这样做的目地是可以让vuex响应全局的mutations操作，而只是给了不同module的state多了一个命名空间。但实际情况，我们有时候不需要vuex响应全局的mutations，或者说，我们可以完全独立，这样可以更好的封装独立模块的功能，于是我们对vuex02.js作如下改动：

* vuex02.js
```javascript
let moduleA = {
   namespaced:true,//这能保证模块下的状态都有独有的命名空间
   actions:{
      //...
   },
   muations:{
      demoCtrl(state,{string=""}={}){
         state.demo = string;
      }
   },
   state:{
      demo:'this is a demo!'
   }
};

let store = new Vuex.Store({
   modules:{
      a:moduleA
   }
});
```

于是，我们的html02.vue可能就是这样的了。如：

* html02.vue
```javascript
export default {
   computed:{
      demo(){
         return this.$store.state.a.demo
      }
   },
   mounted(){
      //改变状态
      this.$store.commit('a/demoCtrl',{string="这是一个新值！"});
   }
};
```
这样就能做到即使在全局调用this.$store.commit('demoCtrl',{string="这是一个新值！"})也不会影响模块a下的状态，因为有独立的命名空间。

#### 使用module化管理vuex的好处

* 更好的管理我们的状态，把原本庞大的一个对象树分化到各个小的module里面。

* 更好的命名冲突，因为如果对象大了以后，我们难免后命名的state名字会跟之前的一样，或者多同事同时开发的时候，也会造成同样的问题，所以我们采用module化了之后，可以有效解决这种问题。


*本文档基于官方文档，详情可查看[官方文档](https://vuex.vuejs.org/zh/guide/modules.html)*

#### 为什么要模块化管理vuex

首先默认的vuex使用的是单一状态树，所以当项目越来越大的时候，所以的数据将会集中到一个非常庞大的对象上，这很难管理。其次，我们可以利用module实现vuex状态更好的封装性和复用性，并且减少命名冲突，于是模块化管理vuex显得很有必要。

#### 怎么使用module

我们看一下vuex是怎么用的。代码如下：

* vuex01.js
```javascript
let store = new Vuex.Store({
   actions:{
      //...
   },
   mutations:{
      //...
   },
   state:{
      //...
   }
});  
```


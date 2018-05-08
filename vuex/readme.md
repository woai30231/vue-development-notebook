### 前言

该部分开始之前假设你已经通过vue官方脚手架搭建了一个demo项目。怎么搭建可以查看[01-如何使用vue-router](https://github.com/woai30231/vue-development-notebook/tree/master/vue-router)中相关介绍。

这里会带领大家实现一个用vuex来实现加减器操作。

* 第一步：安装vuex，并在src目录下的main.js中引入

``` bash
  //安装
  npm install --save vuex
```

```javascipt
  //在main.js中引入vuex
  import Vuex from 'vue-vuex';
  //引入store.js文件，该文件保存了，mutation、action、state等信息
  import Store from './vuex/';
  
  //调用vue的use方法
  Vue.use(Vuex);
  
  //调用store
  let store = new Vuex.Store(Store);
```

最终我们的main.js代码如下：

<pre>
// The Vue build version to load with the `import` command
// (runtime-only or standalone) has been set in webpack.base.conf with an alias.
import Vue from 'vue'
import App from './App'
import router from './router'
import Vuex from 'vuex';
import Store from './vuex/';

Vue.use(Vuex);
let store = new Vuex.Store(Store);


Vue.config.productionTip = false

/* eslint-disable no-new */
new Vue({
  el: '#app',
  router,
  store,
  components: { App },
  template: '<App/>'
})
</pre>




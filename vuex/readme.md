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
import Store from './vuex/index.js';

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

* 第二步：初试vuex相关文件，在src目录下，分别执行如下命令：

```bash
 cd src 
 mkdir vuex && cd vuex 
 touch index.js action.js mutaction.js state.js
```

执行上面的命令之后，分别会在src目录下新建vuex目录，并在vuex目录下新建index.js、mutation.js、action.js、state.js四个文件。内容分别如下：

```javascript
 //index.js
 import actions from './action.js';
 import mutations from './mutation.js';
 import state from './state.js';

 export default {
     actions,
     mutations,
     state
 }
```

```mutation.js
 //mutation.js
 export default {
     add(state,{num}={num:1}){
         state.count += num;
     },
     diff(state,{num}={num:1}){
         state.count -= num;
     }
 }
```

```javascript
 //action.js
 export default {
     //异步 1秒之后加1
     asyncAdd(store,{num}={num:1}){
         setTimeout(()=>{
             store.commit('add',{num})
         },1000);
     },
     //异步 1秒之后减1
     asyncDiff(store,{num} = {num:1}){
         setTimeout(()=>{
             store.commit('diff',{num});
         },1000)
     }
 }
```

```javascript
 //state.js
 let count = 0;
 export default {
     count
 }
```

* 第三部，我们来改App.vue文件，实现用户界面。最终App.vue代码如下：

<pre>
 
 <template>
  <div>
    {{count}}
    <div>
      <button @click="$store.commit('add')">加1</button><br />
      <button @click="$store.commit('diff')">减1</button><br />
      <button @click="$store.dispatch('asyncAdd')">异步加1</button><br />
      <button @click="$store.dispatch('asyncDiff')">异步减1</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  computed:{
    count(){
      return this.$store.state.count;
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>


</pre>

* 最后一步，浏览器打开localhost:8080，验证结果

_ 点击加1, 结果加1

_ 点击减1，结果减1

_ 点击异步加1，结果在1秒之后加1

_ 点击异步减1，结果在1秒之后减1

* 结语

通过一步一步的操作，我么知道在vue里面怎么用vuex。其它高级用法参考官方地址和相关论坛！




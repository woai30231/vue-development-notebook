#### 前期准备

1、搭建项目架构

```bash
  npm install -g vue-cli
  vue init webpack vue-router
```

2、安装项目依赖

```bash
  npm install
```

3、跑项目

```bash
  npm start || npm run dev
```

4、查看网页

用浏览器打开 http://localhost:8080 ，我们发现能够正常打开欢迎网页！

#### 改项目架构，使用vue-router

1、安装vue-router

```bash
  npm install --save vue-router
```

2、配置路由文件

进入src目录，新建router目录：

```bash
  mkdir router && cd router && touch index.js
```

其中index.js文件内容如下：

```javascript
import Vue from 'vue';
import Router from 'vue-router';
import Nav1 from '../components/Nav1.vue';
import Nav2 from '../components/Nav2.vue';
import Nav3 from '../components/Nav3.vue';
Vue.use(Router);

let router = new Router({
    mode:'hash',
    routes:[
        {
            path:'/nav1',
            component:Nav1
        },
        {
            path:'/nav2',
            component:Nav2
        },
        {
            path:'/nav3',
            component:Nav3
        },
        {
            path:'/',
            redirect:{
                path:'nav1',
                component:Nav1
            }
        }
    ]
})
export default router;
```

同时，我们对App.vue作如下修改：

```vue
<template>
  <div id="app">
    <nav>
      <ul>
        <li v-for="(item,index) in nav">
          <router-link :to="{path:item.path}">{{item.text}}</router-link>
        </li>
      </ul>
    </nav>
    <router-view></router-view>
  </div>
</template>

<script>
export default {
  name: 'App',
  data(){
    return {
      nav:[
        {
          text:'nav1',
          path:'nav1'
        },
        {
          text:'nav2',
          path:'nav2'
        },
        {
          text:'nav3',
          path:'nav3'
        }
      ]
    };
  }
}
</script>
<style>
</style>

```

并在components目录下新建三个文件Nav1.vue、Nav2.vue、Nav3.vue，三个文件内容分别如下：

Nav1.vue
```vue
  <template>
  <div>

    nav1正文
  </div>
</template>

<script>
export default {  
}
</script>
<style>
</style>
```

Nav2.vue
```vue
  <template>
  <div>

    nav2正文
  </div>
</template>

<script>
export default {  
}
</script>
<style>
</style>
```

Nav3.vue
```vue
  <template>
  <div>

    nav3正文
  </div>
</template>

<script>
export default {  
}
</script>
<style>
</style>
```

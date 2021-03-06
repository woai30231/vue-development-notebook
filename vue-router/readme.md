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

#### 结果

此时我们再打开localhost:8080，我们发现路由默认跳到localhost:8080/#/nav1。而后我们分别切换三个导航，相应内容和路由也会作相应的切换，至此，我们一个简单的关于使用vue-router的实例就完成了！

#### 说明

* **router-view**

该标签是用来放置路由动态切换内容的地方，实际项目开发中也就是放置page内容的地方。这里需要注意的将来的组件内容和配置的路径是匹配对应的，这是在router/index.js里面配置好的。如：

```txt
  /nav1 对应 Nav1.vue
  /nav2 对应 Nav2.vue
  /nav3 对应 Nav3.vue
```

* **router-link**

在vue-router搭建的项目中，开发者有两种方式切换路由，其一就是使用router-link来实现路由的切换，其二就是使用编程式来切换。如要切换到/nav1路由，两种方式分别实现如下：

router-link
```
<router-link :to="{path:'/nav1'}"></router-link>
```

编程式
```
  this.$router.push({path:'/nav1'})
```

**注：** 在使用vue-router之前，需要先调用如下：

```javascript
  Vue.use(Router)
```

#### 原理

# 待续………………

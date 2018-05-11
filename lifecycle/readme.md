### 准备 

本文假设你已通过vue官方脚手架搭建了一个简单的demo项目，命令如下：

```bash
  vue init webpack myproject
```

运行程序

```bash

  npm install  && npm run dev
```

打开浏览器 [http://localhost:8080](http://localhost:8080)， 即可浏览一个初始界面。

### vue生命周期介绍

如果用一张图来描述vue组件的整个周期过程，那么可以借用vue官网的一张图，如下：

![](https://cn.vuejs.org/images/lifecycle.png)

由图可知，一个vue组件大概需要经历如下过程：beforeCreate、created、beforeMount、mounted、beforeUpdate、updated、beforeDestroy、destroyed！对应的时间段触发对应的回调函数来处理相关时间点的数据！

### 验证每个周期回调函数里数据是怎么样的 

* 首先改下用户界面 ，App.vue代码如下：

``` html
  <template>
  <div id="app">
    <Test :parentdata="parentdata"/>
  </div>
</template>

<script>
import Test from './components/Test.vue';
export default {
  name: 'App',
  data(){
    return {
      parentdata:'parent'
    }
  },
  components:{
    Test
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

```

并在components目录下新建Test.vue，其代码如下：

```html
  <template>
    <div>
        <p>父组件传过来的数据:{{parentdata}}</p>
        <p>子组件自身的数据:{{childselfdata}}</p>
    </div>
</template>
<script>
export default {
    props:{
        parentdata:[Array,String,Number]
    },
    data(){
        return {
            childselfdata:'child'
        };
    }
}
</script>
<style>

</style>
```

此时我们打开 [http://localhost:8080](http://localhost:8080) 可以查看得到新界面。

#### 查看周期回调里面拿到的数据是怎么样的

##### beforeCreate

在Test.vue里面添加如下代码:

```javascript
  beforeCreate(){
    console.log(this);
  }
```

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
        <p ref="dom">获取dom</p>
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
      console.log(this.$data);
      console.log(this.$props);
      console.log(this.$el);
      console.log(this.$refs.dom);
  }
```

我们发现控制台打印这些数据时得到下面的结果：

<pre>
  undefined
  undefined
  undefined
  undefined
</pre>
所以我们在使用vue开发的过程中，千万别在这个周期里面获取这些数据，没有用！

##### created

增加代码：

```javascript
  created(){
      console.log(this.$data);
      console.log(this.$props);
      console.log(this.$el);
      console.log(this.$refs.dom);
  }
```
在控制台发现，我们能正常获取this.$data和this.$props，但是this.$el和this.$refs.dom照样是undefined。所以在这个回调里面千万不要获取跟dom结构相关的数据，因为vue还没有渲染出来！

##### beforeMount

增加代码

```javascript
     beforeMount(){
        console.log(this.$data);
        console.log(this.$props);
        console.log(this.$el);
        console.log(this.$refs.dom);
    }
```

在控制台发现，我们能正常获取this.$data和this.$props，但是this.$el和this.$refs.dom照样是undefined。所以在这个回调里面千万不要获取跟dom结构相关的数据，因为vue还没有渲染出来！

##### mounted

增加代码

```javascript
      mounted(){
        console.log(this.$data);
        console.log(this.$props);
        console.log(this.$el);
        console.log(this.$refs.dom);
    }  
```

我们发现在这个回调里面能正常获取四个相关数据。

##### beforeUpdate

增加代码以及改一下代码：

```javascript
  data(){
    return {
      childselfdata:'child',
      childtimer:0
    };
  },
  created(){
    setInterval(()=>{
      this.childtimer++;
    },1000)
  },
  beforeUpdate(){
    console.log("这里会执行吗？");
  }
```

我们会发现这样写的话，beforeUpdate回调根本没有执行！

ok，我们进一步修改html结构：

```html
  <template>
      <div>
          <p>父组件传过来的数据:{{parentdata}}</p>
          <p>子组件自身的数据:{{childselfdata}}</p>
          <p ref="dom">获取dom</p>
          <p>{{childtimer}}</p>
      </div>
  </template>
```
我们发现，当我们把数据写在模板中时，如果数据改变驱动视图更新，那么beforeUpdate回调就会相应的执行函数，也就是说，视图没更新，只是数据更新，那么beforeUpdate回调是不会执行的！


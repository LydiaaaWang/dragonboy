### 拿到一个vue+webpack项目，该如何去看，摸索中

~~首先得知道每个文件夹是干啥的吧：~~

1、先看配置文件package.json，里面定义了这个项目所需要的各个模块，以及项目的配置信息。`scripts`指定了运行脚本命令的npm命令行缩写，比如dev指定了运行`npm run dev`时所要执行的命令。

2、我拿到的这个项目在开发环境下通过命令npm run dev来启动的，所以我去package.json文件里找到了scripts配置，其中有设置dev选项，也就是说在运行命令npm run dev时，启动了webpack-dev-server服务，并指定了配置文件webpack.dev.config.js，所以我们接下来就去看webpack.dev.config.js文件。

```js
"scripts": {
    "dev": "webpack-dev-server --inline --progress --config build/webpack.dev.conf.js",
    "start": "npm run dev",
    "unit": "jest --config test/unit/jest.conf.js --coverage",
    "e2e": "node test/e2e/runner.js",
    "test": "npm run unit && npm run e2e",
    "lint": "eslint --ext .js,.vue src test/unit test/e2e/specs",
    "build": "node build/build.js"
  },
```

3.看代码不能从第一行开始看，不然看的时候你无法串起来，看完了也不知道在讲啥。这里我看webpack.dev.config.js文件时先看最后输出了什么模块，然后前面肯定是围绕生成这个模块而写的代码，所以我们直接从模块生成的地方开始。里面的一些配置其实根据属性名就能猜出个大概意思，不懂的可以去查官方文档。我这里publicPath还搞得不是很清楚-\_-!

我们这里输出的模块大概是：`devWebpackConfig`

4.找到配置文件webpack.dev.config.js中的入口文件，这里是src目录下的index.js文件，其中引入了一些通用的模块，还有一个重置的样式文件reset.css和一个动态适配移动端的js文件viewPort.js，另外，还创建了一个Vue实例

```
new Vue({
  el: '#root',
  router,
  store,
  render: h => h(App)
})
```

注意，render是一个方法，h = h\(App\)是ES6的写法，即render: function\(h\) {    return h\(App\);}其中h是createElement的一个别名，关于render和JSX的介绍可以看官方文档[https://cn.vuejs.org/v2/guide/render-function.html](https://cn.vuejs.org/v2/guide/render-function.html)

to me:

找到配置文件webpack.base.conf.js中的入口文件，这里是src目录下的main.js文件，

```
entry: {
    app: './src/main.js'
  },
```

引入了一些通用的模块：比如echarts/axios/elementUi/vuex, 并且use them,然后还创建了一个vue实例。

```
new Vue({
  el: '#app',
  router,
  store,
  components: { App },
  template: '<App/>'
})
```

5、h\(App\)以App组件为参数，它是引入的App.vue，所以我们去看看App.vue，

```
<script>
export default {
  render () {
    return (
      <div>
        <router-view></router-view>
      </div>
    )
  }
}

</script>
```

to me:

vue实例里边有很多app.所以去看看app.vue吧

```
<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<script>
</script>

<style>
</style>
```

6、上面可以看出把&lt;router-view&gt;&lt;/router-view&gt;挂载到主页面index.html的&lt;div id="root"&gt;&lt;/div&gt;元素下了，所以在启动项目并在浏览器地址栏中输入网址后，会根据路由渲染相应的组件。所以接下来我要去看路由配置了，router-&gt;index.js：

```
import Vue from 'vue'
import VueRouter from 'vue-router' 
import routes from './routes.js' 
Vue.use(VueRouter) 
export default new VueRouter({  routes})
```

发现它就只是引用了当前文件夹下的另一个路由js文件routes.js：

```
export default [  
    {    
    path: '/',    
    redirect: '/mrReading'  
    },  
    {    
    path: '/mrReading',    
    component: () => import('../views/mrReading/Index.vue')  
    }
]
```

TO ME:

可以看出把&lt;router-view&gt;挂载到主页面index.html的&lt;div id="app"&gt;&lt;/div&gt;元素下了,所以在启动项目并在浏览器地址栏中输入网址后，会根据路由渲染相应的组件。所以接下来我要去看路由配置了，./router/index.js：

```
import Vue from 'vue'
import Router from 'vue-router'
import Index from '@/components/Index'

Vue.use(Router)

export default new Router({
    routes: [
    {
      path: '/',
      name: 'Index',
      component: Index

    },
    {
      path: '/messagelist',
      name: 'messagelist',
      component: Messagelsit,
      meta: {
        requiresAuth: true
      }
    }
  ]
})
```

那么关于路由到底有哪些东西呢？稍微浏览一下文档先：

怎么浏览呢？看一遍还要敲吗?

资料参考

1、[拿到一个vue+webpack项目，该如何去看](https://blog.csdn.net/DreamFJ/article/details/82146779)


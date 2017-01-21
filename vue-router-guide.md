## vue-router知识点整理 ##

> 在vue的官方教程虽然提供了简单路由的实现方法，但是在做过的项目中，都没有采用这种方式。无论
> 项目大小，都是采用Vue官方出品的路由插件vue-router。


#### 开始 ####
> 使用vue-route流程
> 确保引入vue.js和vue-router.js
> 定义组件或者引入组件
> 生成路由对象，路由对象中写入路径和引入组件
> 将路由对象注入vue对象

#### 动态路由匹配 ####

1. 动态路由
> 路由路径不一定确定的，可能是动态变化的，所以可以在路由对象写路径的时候添加参数
> 形式 { path: '/user/:id', component: User}
> 在模板中可以用$route.params.id访问，在JS中可以用this.$route.params.id访问
> 如果想响应路由参数为空的情况，可以在子路由children中设置一个空路径

2. 响应路由参数变化
> 当路由参数发生变化的时候，Vue会复用原来的组件，所以组件的生命钩子函数不会再执行。想要对路
> 由参数的变化做出响应，可以在组件站使用watch。
<pre><code>
const User = {
  template: '...',
  watch: {
    '$route' (to, from) {
      // 对路由变化作出响应...
    }
  }
}
</code></pre>

3. 高级匹配模式

 
> Vue使用path-to-exp作为路径匹配引擎，查看[文档](https://github.com/pillarjs/path-to-regexp#parameters)学习高阶用法。

4. 匹配优先级
> 有时候，同一个路径可以匹配多个路由，此时，匹配的优先级就按照路由的定义顺序：谁先定义的，
> 谁的优先级就最高。

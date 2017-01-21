## Vue知识点整理 ##


> 说起Vue的学习要说到上一份实习——2016年7月20日-9月30日在佛山无影角的实习。是在那里Kilmas
> 带我入了Vue的坑，引我入现代前端开发的门，才有了后来的一切。



### 本项目根据[Vue中文文档](https://vuefe.cn/) 整理而成

## 快速开始 ##

#### vue-cli ####
>首先安利一个好东西vue-cli。使用vue构建单页的时候，可以使用vue官方提供的脚手架,省去构建应用
>时需要的各种配置，快速构建应用。

####  Vue实例 ####
> Vue实例包括data、methods、computed等属性，Vue实例会代理data的所有属性，所以可以直接用
> vue实例例如vm，访问data的属性，如message，即vm.message。

<br/>

## 模板语法 ##
> 对于页面的描绘，Vue采用基于html的模板，在普通html的基础加上一些Vue特有的语法。

#### 插值 ####
> 插值就是利用Vue语法绑定Vue实例的值
- mustache语法。使用mustache语法绑定Vue实例中data的属性，{{ message }}。<br/>
- v-html语法。Vue 2.x之后用 v-html="message"语法绑定Vue 2.X之前如果数据是html代码，可
以使用{{{ message }}}语法渲染。


#### 指令 ####
> 指令的标志就是前缀为v-,每个指令可携带一个参数
- v-bind:,简写“：”，用来响应式更新html属性
- v-on:,简写“@”，用来绑定事件类型和handle，想用DOM事件
- 修饰符，带在指令后面，指定以特殊方式绑定，如prevent

#### 过滤器 ####
> 利用 pipe语法—— “|”，可在mustache和v-bind中使用过滤器，过滤器总接受表达式的值作为第一个参数。

## class与style绑定 ##

#### class绑定 ####
> class的绑定有两种语法，对象绑定和数组绑定。

- 对象语法指在class上绑定一个对象，对象属性名为类名，对象属性值为boolean值，指定类是否生效。
有两种形式，一种直接绑定vm对象，一种是对象属性值绑定vm属性，不支持对象属性名绑定vm属性。
- 数组语法中数组元素都是vm的属性。而vm属性的值都为类名，数组元素不能是类名，这样会出现undefined错误。

#### style绑定 ####
> style绑定也有两种语法，对象语法和数组语法。
- 对象语法指在style上绑定一个对象，对象属性名为css属性，对象属性值为css属性值，同样有两种，
一种直接绑定vm对象，一种是对象属性值绑定vm属性，不支持对象属性名绑定vm属性。
- 数组语法中每个数组元素都是一个对象，对象名为css属性，对象值为css属性值。

## 渲染 ##

#### 条件渲染 ####
> 条件渲染包括v-if v-else v-else-if 三个指令，其中v-else-if 是新增指令。
> 
> Vue为了更有效率的渲染页面，会重复使用已有元素。例如在条件渲染中的v-if与v-else中切换时，
> 里面的元素会被重用，在使得渲染更有效率的情况下，还有一些额外的好处。例如input元素，切换
> 后还是使用原来的元素，所以会保留原本输入的内容。
> 
> v-show也可以实现条件渲染效果，用法与v-if一致，但二者有不同的地方。
> v-if是真实的条件渲染，每一次切换都会重建条件块内的事件监听器和子组件，而v-show只是简单的
> css属性display值变换。
> v-if的渲染还是惰性的，当初始的值为假时，不会渲染，当值变换为真时，才实现第一次渲染。
> 所以频繁切换的话，使用v-show，运行条件不太可能改变使用v-if。

#### 列表渲染 ####

- 基本用法 v-for="item in items" "(item,index) in items" 可以用来迭代对象和数组
- 迭代对象 v-for="value in object" "(value,key) in object"
- 整数迭代 v-for="n in 10"

#### 变异数组方法 ####
> 变异方法：顾名思义调用这些方法会改变原来的数组
> push()
> pop()
> shift()
> unshift()
> splice()
> sort()
> reverse()

#### 非变异数组方法 ####
> filter()
> concat()
> slice()

## 事件 ##

#### v-on事件修饰符 ####
> .stop 阻止冒泡
> .prevent 阻止默认事件
> .capture 启动captrue模式
> .self 只在元素本身触发。不在子元素触发

#### v-on按键修饰符 ####
> 任意keycode都可以作为按键修饰符，但是keycode比较难记，而且无法见名知意，所以Vue给出一些
> 别名，可以通过 config.keyCodes设置按键修饰符别名 如Vue.config.keyCodes.f1 = 112
> .enter
.tab
.delete (捕获 “删除” 和 “退格” 键)
.esc
.space
.up
.down
.left
.right

#### 鼠标事件修饰符 ####
> 可以用如下修饰符在相应按键响应时进行鼠标事件监听
.ctrl
.alt
.shift
.meta


## 表单 ##

#### 表单控件绑定 ####
- 对于input textarea，v-model绑定文本内容
- 对于checkbox，单个复选框是逻辑值，多个复选框为value值
- 对于radio，v-model绑定value值
- 对于select绑定的是value，如果没有value，绑定option中间的值

>  v-bind:true-value="a"
   v-bind:false-value="b" 实现value的动态绑定

#### v-model 修饰符 ####
> .lazy 不会同步更新，只在change事件发生时更新
> .trim 去掉输入的首位空格
> .number 转换为数字，如果结果为NaN，则返回原值

## 组件 ##
> 组件注册分为全局注册he局部注册
> is属性用在html元素上，可以突破html元素本身对于子元素的限制，如<tr is="my-component">
> 组件中data必须是函数

#### 使用prop传递数据到子组件 ####
> 组件定义时，使用props数组定义父组件传递到该子组件的属性，可以使用v-bind语法。
> 可以对prop进行验证，不符合验证要求子组件会拒绝赋值。

#### 使用事件传递数据到父组件 ####
> 利用v-on/@可以自定义事件，将事件绑定在子组件上，然后在子组件中利用this.$emit('custom-event-type')
> 触发事件。
> PS使用 this.$on()可以监听事件
> 如果想对组件绑定原生事件，需要在事件后面加一个修饰符


#### 非父子组件通信 ####
> 对于非父子组件之间的通信，可以使用一个空的Vue实例作为中央事件总线。例如把数据从A传到B，在
> 组件B的创建钩子函数 bus.$on()监听事件,然后利用bus.$emit()触发A中事件。
> 在复杂情况更应该使用vuex这个状态管理工具。

#### 单个slot ####
> 子组件的slot可以插入内容，作为备份内容，宿主元素为空时，且没有插入内容时显示。

#### 具名slot ####
> slot即在自组件定义的时候，采用类似格式：<slot name="header"></slot>
> 使用的时候，采用类似格式： <h1 slot="header"></h1>

#### 作用域插槽 ####
> 通过template中scoped属性获取到自组件传递上来的对象，这个对象包含自组件中slot的属性值
> 文档说，可以自定义列表渲染。

#### 动态组件 ####
> 多个组件可以动态的使用同一个挂载点，使用保留的component进行加载，加载方式为绑定组件到它的
> is特性上。

#### keep-alive ####
> 使用keep-alive标签包含组件，可以将切换出去的组件保留在内存中，保留它的状态 避免被重新渲染。
> 这个在单页应用应该有很好的应用。

#### 解决组件互相引用的问题 ####

> beforeCreate: function () {
  this.$options.components.TreeFolderContents = require('./tree-folder-contents.vue')
}

#### nextTick ####
> this.$nextTick() 可以在DOM更新完做一些事情，括号内传入回调函数
    

## 自定义指令 ##

#### 自定义指令时的钩子函数 ####
> bind
> update
> inserted
> componentUpdated
> unbind

#### 参数 ####
> el，binding，vnode，oldVnode
> 
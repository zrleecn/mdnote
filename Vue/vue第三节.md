# vue第三节课

## 1、vue-cli

### 简介及安装

`vue-cli`是官方提供的一个**脚手架工具**(已经帮组写好基础代码).可以`快速生成一个vue的项目模板`

[github地址](https://github.com/vuejs/vue-cli)  ： https://github.com/vuejs/vue-cli

主要的功能：

* 规范的目录结构
* 本地调试
* 代码部署
* 热加载
* 单元测试

vue-cli的优势：

* 成熟的vue项目的架构设计
* 本地测试服务器-node-server
* 集成打包上线

环境要求

* nodejs>4.0  (通过node   -v查看版本)
* git
* **能够使用命令行的终端**

安装流程：

如果没有装cnpm可以使用`npm install cnpm -g`安装(Mac系统则一律需要加sudo)

`cnpm install vue-cli -g`  -g表示`安装到全局`

也可以通过`vue list`来查看所有可以使用的模板

安装成功以后新建一个目录，在该目录下执行(先去到该目录)：

   `vue init webpack vuecli`

会生成一个自定义的目录名vuecli(可修改)

- `webpack`是`vue-cli的webpack模板`
- `vuecli`是项目名称
- 然后配置信息
- **进入vuecli目录**执行`npm install`安装依赖(如果是从别人那里拷贝过来的
- src目录，则可能需要执行npm install安装可能需要的依赖)  
- 或者sudo  cnpm install  (sudo是临时获得超级用户权限，c是表示国内网址速度比较快)
- 到**vuecli目录下执行`npm run dev或者cnpm run dev`**运行项目
- (或者Mac下使用sudo  cnpm run  dev)

【注意1】有时候网络速度差的话可能会出现各种问题,导致失败。

【注意2】如下错误：![](XXX)

![](http://i2.muimg.com/567571/c6f87475c1456107.png)

是因为启动了两个或多个服务器程序，或者两次或多次启动同一个服务程序占用了同一个端口造成的，所以在结束一个服务程序的时候，必须在控制台获取焦点的情况下使用ctrl + C退出(与端口解除绑定)，否则可能并没有真正的退出。比如直接关闭控制台，直接关闭浏览器，并不能真正地退出服务程序。你可以在浏览器地址栏输入localhost: + 端口号进行尝试。或者采取其他更换端口的方式也可以。

【注意3】如果你的src目录是从别人那里拷贝过来的，那么可能会因为某些依赖dependency没有安装而不能run成功。你可以查看错误的原因，安装相应的依赖即可。比如：npm install --save  vue-router   具体知识见下文。

路由的安装可以直接在创建项目文件的时候选择Y即可(后面就不需要手动安装了)。

=========================================================================

### 目录文件介绍

<img src="http://i4.buimg.com/567571/60cdfa675f15418a.jpg" width="200">

* `build`和`config`是webpack的配置文件(没有build或config都不能执行)
* node_modules中存放的是`npm install`安装的**文件依赖代码库**
* `src`文件中存放的是项目源码
* `static`存放的是第三方的静态资源，里面默认情况下只有`.gitkeep`这个文件，它的意思是当这个目录为空的时候，也是可以提交到git代码仓库里，如果没有这个文件git会忽略这个目录
* `.babelrc`这个文件是`babel`的一些配置,主要就是用于将es6的代码转成es5的,详细介绍：[babel](http://www.ruanyifeng.com/blog/2016/01/babel.html)
* http://www.ruanyifeng.com/blog/2016/01/babel.html
* `.editorconfig`是编辑器的一些配置
* `eslintignore`如果安装`eslint`会出现这个文件，用于的就是说明不做语法检查的文件
* `eslintrc.js`如果安装`eslint`会出现这个文件，用于`eslint`的配置文件
* `.gitignore`用于向git声明需要**忽略提交的文件**
* `.postcssrc.js`这个文件是postCSS的配置文件，postCSS是一款通过JS插件来转换CSS的工具，这些插件能帮你校验你的CSS代码、转换未来的CSS语法、支持变量和混写、以及内联图片等等，其中[自动前缀](https://github.com/postcss/autoprefixer)插件是PostCSS最受欢迎预处理器之一。默认就配置使用了`autoprefixer`也就是自动前缀的这个插件
* `index.html`就是入口的html文件，在编译打包过程中会将资源文件自动插入到这个html文件中
* `package.json`项目的配置文件，这个文件中的信息是我们在初始化`vue-cli`的时候填入的信息：
  * 最重要的就是里面的`scripts`属性，表示的是我们可以执行的一些命令,比如`npm run dev`就是执行的`node build/dev-server.js`这个命令，然后`npm run build`就是执行的`node build/build.js`也就是打包的操作，我们也可以自己在`scripts`中去配置一些脚本
  * `dependencies`里面放的项目生产环境的一些依赖，然后在安装一些模块的时候可以通过`--save`保存到这个属性下，比如要使用`vue-router`就可以使用`npm install vue-router --save`
  * `devDependencies`里面放的编译过程中的一些依赖，在最后打包的时候不存在
* `README.md`就是项目的描述文件


如果在HBuilder中遇到文件是只读文件，则可以把整个src文件夹或者整个工程文件夹修改成777权限，即获取可读可写可执行权限。一般在HBuilder中是只读权限的。   执行： sudo chmod -R   777   +文件夹名src


### 项目运行

项目的入口文件是`main.js`,然后在`main.js`中依赖`app.vue`组件. `app.vue`组件中又依赖了`hello.vue`这个组件。一个标准组件的构成就是由：

`template(模板),script,style`这三个**标签**构成，如果要在`app.vue`中使用`hello.vue`这个**组件**的话，需要**把hello定义为app的子组件**

```javascript
mponents/Hello'

export default {
  name: 'app',
  components: {
     Hello
   }
}
```

===============================================================

## 2、webpack

### 简介

`webpack`是当下最热门的**前端资源模块化管理和打包工具**。它可以将许多松散的模块按照依赖和规则打包成符合生产环境部署的前端资源。还可以将按需加载的模块进行代码分隔，**等到实际需要的时候再异步加载**。通过 `loader` 的转换，任何形式的资源都可以视作模块，比如 CommonJs 模块、 AMD 模块、 ES6 模块、CSS、图片、 JSON、Coffeescript、 LESS 等

![](http://webpackdoc.com/images/what-is-webpack.png)

<img src="http://webpackdoc.com/images/what-is-webpack.png" >

文档：[webpack](http://webpackdoc.com/index.html)

### 现状

伴随着移动互联的大潮，当今越来越多的网站已经从网页模式进化到了 Webapp 模式。它们运行在现代的高级浏览器里，使用 HTML5、 CSS3、 ES6 等更新的技术来开发丰富的功能，网页已经不仅仅只能完成浏览的基本需求，并且webapp通常是一个**单页面应用**，每一个视图通过异步的方式加载，这导致页面初始化和使用过程中会加载越来越多的 JavaScript 代码，这给前端开发的流程和资源组织带来了巨大的挑战。

前端开发和其他开发工作的主要区别，首先是前端是基于多语言、多层次的编码和组织工作，其次前端产品的交付是基于浏览器，这些资源是通过增量加载的方式运行到浏览器端，如何在开发环境组织好这些碎片化的代码和资源，并且保证他们在浏览器端快速、优雅的加载和更新，就需要一个模块化系统，这个理想中的**模块化系统**是前端工程师多年来一直探索的难题。



### 模块系统的演进-扩展

#### <script>标签

```html
<script src="module1.js"></script>
<script src="module2.js"></script>
<script src="libraryA.js"></script>
<script src="module3.js"></script>
```

这是最原始的 JavaScript 文件加载方式，如果把每一个文件看做是一个模块，那么他们的接口通常是暴露在全局作用域下，也就是定义在 `window` 对象中，不同模块的接口调用都是在一个作用域中，一些复杂的框架，会使用**命名空间**的概念来组织这些模块的接口，典型的例子如 [YUI](http://yuilibrary.com/) 库。

这种原始的加载方式暴露了一些显而易见的弊端：

- 全局作用域下容易造成变量冲突
- 文件只能按照 `<script>` 的书写顺序进行加载，否则可能报错
- 开发人员必须主观解决**模块和代码库的依赖关系**
- 在大型项目中各种资源难以管理，长期积累的问题导致代码库混乱不堪

#### CommonJS(普通JS)

服务器端的 Node.js 遵循 [CommonJS规范](http://wiki.commonjs.org/wiki/CommonJS)，该规范的核心思想是允许模块通过 `require` 方法来**同步加载所要依赖的其他模块**，然后通过 `exports` 或 `module.exports` 来导出需要暴露的接口。

```javascript
require("module");
require("../file.js");
exports.doStuff = function() {};
module.exports = someValue;
```

优点：

- 服务器端模块便于重用
- [NPM](https://www.npmjs.com/) 中已经有超过45万个可以使用模块包
- 简单并容易使用

缺点：

- 同步的模块加载方式不适合在浏览器环境中，同步意味着**阻塞加载**，浏览器资源是**异步加载**的
- 不能非阻塞的并行加载多个模块

实现：

- 服务器端的 [Node.js](http://www.nodejs.org/)
- [Browserify](http://browserify.org/)，浏览器端的 CommonJS 实现，可以使用 NPM 的模块，但是编译打包后的文件体积可能很大
- [modules-webmake](https://github.com/medikoo/modules-webmake)，类似Browserify，还不如 Browserify 灵活
- [wreq](https://github.com/substack/wreq)，Browserify 的前身

================================================================

####AMD

[Asynchronous Module Definition](https://github.com/amdjs/amdjs-api) 规范其实只有一个主要接口 `define(id?, dependencies?, factory)`，它要在声明模块的时候指定所有的依赖 `dependencies`，并且还要当做形参传到 `factory`中，对于依赖的模块提前执行，依赖前置。

```javascript
define("module", ["dep1", "dep2"], function(d1, d2) {
  return someExportedValue;
});
require(["module", "../file"], function(module, file) { /* ... */ });
```

优点：

- 适合在浏览器环境中**异步加载模块**
- 可以**并行加载多个模块**

缺点：

- 提高了开发成本，代码的阅读和书写比较困难，模块定义方式的语义不顺畅
- 不符合通用的模块化思维方式，是一种妥协的实现

实现：

- [RequireJS](http://requirejs.org/)
- [curl](https://github.com/cujojs/curl)

================================================================

#### CMD

[Common Module Definition](https://github.com/cmdjs/specification/blob/master/draft/module.md) 规范和 AMD 很相似，尽量保持简单，并与 CommonJS 和 Node.js 的 Modules 规范保持了很大的兼容性。

```javascript
define(function(require, exports, module) {
  var $ = require('jquery');
  var Spinning = require('./spinning');
  exports.doSomething = ...
  module.exports = ...
})
```

优点：

- 依赖就近，延迟执行
- 可以很容易在 Node.js 中运行

缺点：

- 依赖 SPM 打包，模块的加载逻辑偏重

实现：

- [Sea.js](http://seajs.org/)
- [coolie](https://github.com/cloudcome/coolie)

================================================================

#### ES6 模块

EcmaScript6 标准增加了 JavaScript 语言层面的**模块体系定义**。[ES6 模块](http://es6.ruanyifeng.com/#docs/module)的设计思想，是尽量的静态化，使得编译时就能确定模块的依赖关系，以及输入和输出的变量。CommonJS 和 AMD 模块，都只能在运行时确定这些东西。

```javascript
import "jquery";
export function doStuff() {}
module "localModule" {}
```

优点：

- 容易进行静态分析
- 面向未来的 EcmaScript 标准  如：ES7

缺点：

- 原生浏览器端还没有实现该标准
- 全新的命令字，新版的 Node.js才支持

实现：

- [Babel](https://babeljs.io/)

#### 期望的模块系统

可以兼容多种模块风格，尽量可以利用已有的代码，不仅仅只是JavaScript 模块，还有 **CSS、图片、字体等资源也需要模块化**。

==============================================================

## 单独使用webpack

# 3、Webpack入门指南

### 一、什么是 webpack？

[webpack](http://webpack.github.io/)是一款**模块加载器兼打包工具**，它能把各种资源，例如JS（含JSX）、ES6、样式（含less/sass）、图片等都作为模块来使用和处理。npm是包管理工具。

[更多webpack学习内容](https://github.com/lengziyu/learn-webpack)

[webpack详细教程http://www.cnblogs.com/jaycewu/p/6010872.html]

### 二、安装

```basic
$ npm install webpack -g   (Mac系统在npm之前加sudo)
优先使用：sudo cnpm install webpack -g (c表示国内的网站，速度更快)
```

### 三. 配置

创建 **webpack.config.js** 它的作用和gulpfile.js一样就是一个配置项，设置 webpack 任务功能。

* entry 入口文件 让webpack用哪个文件作为项目的入口
* output 出口 让webpack把处理完成的文件放在哪里
* module 模块 要用什么不同的模块来处理各种类型的文件
* plugins 用于提取多个入口文件的公共脚本部分，然后生成一个 common.js 来方便多页面之间进行复用。
* resolve 用来设置路径指向
* watch 用来监听文件有改动后执行打包

```javascript
module.exports = {
	entry:"xxx",//入口文件
	output:{//出口
		path:"",
		filename:"XXX"
	},
	module:{//模块
		loaders:[
			{test:/\.js$/,loader:""}
		]
	},
	plugins:{},
	resolve:{},
	wacth:true
}
```



### webpack命令

```basic
//直接运行webpack.config.js来打包
$ webpack 

[注意]如果找不到某些插件，则需要在当前目录下和全局目录下各安装一个webpack，这样才能找到某些插件
sudo cnpm install webpack --save-dev
生成一个node_modules才行。

//压缩混淆脚本(使用-p选项)
$ webpack -p    
```

=================================================================

## 在vue-cli中使用webpack

我们可以先从`npm run dev`这个入口开始去分析它.

`npm run dev`其实执行的就是`"dev": "node build/dev-server.js"`这个代码

`build/dev-server.js`这个文件主要是启动一个**node服务器**

在`dev-server.js`中我们可以看到关于`webpackConfig`的配置引入了一个`./webpack.dev.conf`的文件，在`./webpack.dev.conf`文件中又依赖了`./webpack.base.conf`的文件，然后这个`webpack.base.conf`文件就是`webpack`的配置文件了.

### 分析webpack.base.conf的结构

[webpack2.x最新版文档](http://www.css88.com/doc/webpack2/concepts/)

#### entry

入口的配置，它表示webpack编译的入口是指向这个src下的`main.js`

#### output

输出的配置

* `path`:`config.build.assetsRoot`表示输出的一个文件路径，对应的就是`config/index.js`下的`build.assetsRoot`，意思就是会在根目录下创建一个叫dist的文件目录(文件名可修改)
* `filename`：输出文件的名称,`[name]`获取的是`entry`的键，它是一个变量
* `publicPath`:请求的静态资源绝对路径
####resolve

引入的一些模块相关配置

* `extensions`自动补全引入文件的文件后缀
  * `fallback`：**指向的是node_modules文件夹，就是在require找不到这个模块的时候，会去node_modules里面查找**
  * `alias`:提供一些别名
####[module](http://www.css88.com/doc/webpack2/configuration/module/)

这些选项决定了如何处理项目中的[不同类型的模块](http://www.css88.com/doc/webpack2/concepts/modules)，也是webpack最核心的功能

* `rules`:创建模块时，匹配请求的[规则](http://www.css88.com/doc/webpack2/configuration/module/#rule)数组。这些规则能够修改模块的创建方式。这些规则能够对模块(module)应用**加载器(loader)**，或者修改解析器(parser)
  * [加载器](http://www.css88.com/doc/webpack2/loaders/)   loader
  * `include`：只对指定文件目录处理
  * `options`：属性为字符串或对象。值可以传递到 loader 中，将其理解为 loader 选项，由于兼容性原因，也可能有 `query` 属性，它是 `options` 属性的别名。使用 `options` 属性替代
    * `limit`:当文件大小小于10kb的时候，会生成base64串，如果超过的话就会单独生成一个文件，规则就是用`utils.assetsPath`去生成 

#### [plugins](http://www.css88.com/doc/webpack2/plugins/)

插件，webpack 自身的多数功能都使用这个插件接口。这个插件接口使 webpack 变得**极其灵活**

常用的：

* [HotModuleReplacementPlugin](http://www.tuicool.com/articles/aiEva2Q)

  **热更新插件**

* [HtmlWebpackPlugin](http://www.cnblogs.com/haogj/p/5160821.html),该插件可以简化创建调用webpack bundles的html文件


==============================================================

## 4、vue常用插件之vue-router

### 什么是**前端路由?**

根据不同的地址跳转到不同的页面，提到**前端路由**就不得不提**SPA单页应用**，单页面应用就是视觉感觉是页面的切换，但页面其实一直没有刷新，我们是通过js来让页面看起来好像是跳转到了另外一个页面。很多时候项目文件中也只有一个`.html`文件。不需要跟服务器频繁的进行交互，只需要通过**ajax**来**在切换的时候获取最新的数据**，而**不需要把整个页面都重新加载**。而前端路由是**实实在在地切换浏览器地址**，但确实通过js来控制切换的。

[api文档](https://router.vuejs.org/zh-cn/)

### 安装及基础

* 在终端中进入到你的项目目录: `cd 项目路径`
* 在项目目录下执行：`npm install vue-router --save`。后面加上`--save`的原因是要将`vue-router`添加到`package.json`的依赖中(可以在安装完之后去package.json中查看dependencies中是否有vue-router部分)
* 顺序这样也可以：`sudo  npm install --save vue-router`
* 然后在可以项目中引入`vue-router`，比如在`main.js`中

```javascript
/// The Vue build version to load with the `import` command
// (runtime-only or standalone) has been set in webpack.base.conf with an alias.
import Vue from 'vue'
import App from './App'
// 1.引入vue-router及组件
import Router from 'vue-router'
import Hello from './components/Hello'
import Orange from './components/Orange'
import Banana from './components/Banana'

// 2.使用vue-router
Vue.use(Router)
// 3.实例化router这个类
let router = new Router({
	// 5.做映射,什么样的地址,跳转到什么样的页面
	routes:[
		{
          	// path:路径
			path:'/',
          	// 跳转的组件
			component:Hello
		},
		{
			path:'/orange',
			component:Orange
		},
		{
			path:'/banana',
			component:Banana
		}
	]
})

Vue.config.productionTip = false

/* eslint-disable no-new */
new Vue({
  el: '#app',
  // 4.在vue实例中使用router
  router,
  template: '<App/>',
  components: { App }
})
```

然后在`App.vue`中指定路由的位置，使用`router-view`这个组件

```html
<template>
  <div id="app">
    <img src="./assets/logo.png">
   	<!--指定路由位置-->
    <router-view></router-view>
  </div>
</template>

<script>
// import Hello from './components/Hello'

export default {
  name: 'app',
  components: {
    // Hello
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

然后可以在浏览器中修改地址来实现跳转：`http://localhost:8080/#/banana`

### html5 History模式

`vue-router` 默认 为**hash 模式** —— 使用 URL 的 hash 来模拟一个完整的 URL，于是当 URL 改变时，页面不会重新加载。

如果不想要很丑的 hash，我们可以用路由的 **history 模式**，这种模式充分利用 `history.pushState` API 来完成 URL 跳转而无须重新加载页面。使用history的模式无锚点符号#

```javascript
const router = new Router({
  mode: 'history',
  routes: [...]
})
```

当你使用 history 模式时，URL 就像正常的 url，例如 `http://yoursite.com/user/id`，也好看！

### 页面中的跳转

在页面中的跳转可以使用`router-link`组件.它有一个`to`的属性**用于指定跳转的地址**:

```html
 <router-link v-bind:to="{path:'/orange'}">跳转到orange</router-link>
 <router-link v-bind:to="{path:'/banana'}">跳转到banana</router-link>
 <router-link v-bind:to="{path:'/'}">返回首页</router-link>
```

当然`v-bind:to`也可以缩写为`:to`

==============================================================

### 路由参数

以前我们页面之间的参数是**通过`?`号后面的键值对来传递的**，比如：

`http://localhost:8080/?user=xx&pass=12345`

然后在`vue-router`中是以`:`号开头作为我们的参数的，比如：

```javascript
{
  path:'/orange/:color',
  component:Orange
}
```

`:color`就是我们的参数，在地址栏中写入：`http://localhost:8080/orange/red`, red就是我们参数的值，可以通过`this.$route.parms`来获取到参数. 比如要获取传过来的red，就可以通过下面的代码：

```html
<template>
  <div class="orange">
    我是orange橙子
    <button @click="getParams">获取参数</button>
  </div>
</template>
<script type="text/javascript">
export default {
  methods:{
    getParams(){
        console.log(this.$route.params)
    }
  }
}
</script>
```

**这种方式就是固定死了**,如果在地址栏中没有参数是跳转不到`orange`这个页面的，作为变通你还可以使用`query`的方式传参。

```html
<router-link v-bind:to="{path:'orange',query:{color:'red'}}">跳转到orange</router-link>
```

在跳转到地址栏中显示的就是：`http://localhost:8080/orange?color=red`，然后通过`this.$route.query`获取传过来的值，**这种方式就算是没有参数也会正常跳转**到`orange`：

```html
<template>
  <div class="orange">
    我是orange橙子
    <button @click="getQuery">获取参数</button>
  </div>
</template>
<script type="text/javascript">
export default {
  methods:{
    getQuery(){
      console.log(this.$route.query)
    }
  }
}
</script>
```

==============================================================

### 路由嵌套

实际生活中的应用界面，通常由**多层嵌套的组件**组合而成。同样地，URL 中各段动态路径**也按某种结构对应嵌套的各层组件**

比如在要在orange组件中添加一个**子路由**，可以通过配置`children`来实现：

比如我编写了一个组件叫`RedOrange`,代码如下：

```html
<template>
  <div class="orange">
      我是红色的橙子
  </div>
</template>
<script type="text/javascript">
	
</script>
```

想把他作为我orange的子路由，修改`main.js`中关于orange的配置：

```javascript
{
  path:'/orange',
    component:Orange,
      children:[
        {
          path:'red',
          component:RedOrange
        }
      ]
}
```

`children`接受的是一个**数组**，就是说在`orange`下可以定义多个子路由，子路由的核心参数就是`path`和`component`定义的就是路径和子组件，**要注意，以 / 开头的嵌套路径会被当作【根路径】。 这让你充分的使用嵌套组件而无须设置嵌套的路径。**所以`path`中的`red`是不加`/`线的

然后在`orange`需要显示子路由的位置添加`router-view`：

```html
<template>
  <div class="orange">
    我是orange橙子
    <button @click="getQuery">获取参数</button>
    <router-view></router-view>
  </div>
</template>
<script type="text/javascript">
export default {
  methods:{
    getQuery(){
      console.log(this.$route.query)
    }
  }
}
</script>
```

如果想跳转到`RedOrange`页面也是可以通过`router-link`来实现的，比如在`app.vue`中添加一个`router-link`:

```html
<template>
  <div id="app">
    <img src="./assets/logo.png">
    <router-view></router-view>
    <router-link v-bind:to="{path:'/orange',query:{color:'red'}}">跳转到orange</router-link>
    <router-link v-bind:to="{path:'/banana'}">跳转到banana</router-link>
    <router-link v-bind:to="{path:'/'}">返回首页</router-link>
    <router-link v-bind:to="{path:'/orange/red'}">跳转到Redorange</router-link>
  </div>
</template>
```

**注意：路径如果不加/线，那就是个相对路径，默认跳转就是基于当前路径开始的,比如如果跳转orange的path没加/，那在RedOrange中点跳转到orange的时候路径是`localhost:8080/orange/orange?color=red`**即会将/orange/red中的red覆盖掉，用orange？color=red代替。

==============================================================

### 重定向

```javascript
{
  path:'/',
  redirect:'/orange'
}
```

redirect：重定向地址

==============================================================

### 为页面跳转添加【动画】

为**页面跳转**添加动画的方式跟为**组件**加动画的方法是一样的:

```html
<!-- transition添加过渡 -->
    <transition name="fade">
      <!-- 缓存已访问过的组件 -->
       <keep-alive>
          <router-view></router-view>
       </keep-alive>
    </transition>
```

```css
.fade-enter-active, .fade-leave-active {
  transition: opacity .5s
}
.fade-enter, .fade-leave-active {
  opacity: 0
}
```


==============================================================
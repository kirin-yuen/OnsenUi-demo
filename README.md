# OnsenUi笔记

<br/>

### Fundamentals 基本原则
---
<br/>

### What is a Page 什么页面
应用程序中，页面通常指`窗口或者页面视图`；OnsenUI所指一个`包含完整屏幕视口的容器`，OnsenUI中页面定义为`ons-page组件`

带page和toolbar的APP样板，可以使用`OnsenUI组件`与`本地html DOM`
```html
<body>
  <ons-page>
    <ons-toolbar>
      <div class=”center”>Toolbar</div>
    </ons-toolbar>

    <!-- Your page content here. -->
  </ons-page>
</body>
```


<br/>

### Managing Pages 页面管理
大部分应用程序拥有多页面，OnsenUI中可通过多个ons-page实现

<br/>

#### Templates 模板
多页面需要使用模板，模板是一个`在运行时创建实例所需的基本布局`，若模板在给定的时间内被修改，`是不会改变已有的实例`，但会影响之后创建的实例。

模板布局应为`单独一个根的ons-page组件`，其他组件从属于该页

模板必须`指定唯一ID`作为之后的引用，两种方式定义模板
* 外部分离文件：包含`ons-page作为根节点的外部html文件`，
```html
'外部页面./views/page.html'
<ons-page id="page1">

'主页index.html中ons-navigator的page属性引用外部文件'
<ons-navigator id="myNavigator" page="./views/page1.html"></ons-navigator>
```
* 主页index.html中使用ons-template元素，应使用id唯一标识该模板
```html
'原生template标签在2.4后已被支持'
<ons-template id="page.html">
  <ons-page><!-- Content here--></ons-page>
</ons-template>
```

<br/>

#### 3种页面切换
* **Navigator**：多页面以分层顺序可使用`ons-navigator`，提供页面堆叠，可带动画地push或pop页面
* **Tabbar**：页面同层级可使用`ons-tabbar`，通过tap标签可以切换页面显示
* **Splitter**： `ons-splitter`小分辨率的设备以侧边菜单显示，大分辨率的会以分离页面方式显示
可组合使用这些组件完成你所需要的界面

<br/>

### The ons Object
`ons` js对象是`全局可用`提供多种有用的方法与属性，如`ons.ready(callback)`用于等待app初始化完成(等待DOMContentLoaded与Cordova's deviceready触发)，


<br/>

### Attributes, Properties, Methods and Events
Onsen UI组件是一个`简单的DOM元素`，同样拥有属性、方法、事件，用ons-navigator举例
* **Attribute 特性**：特性`修改组件默认功能或如何展示`，大部分特性是可选，某些需要页面初始化前指定如animation
```html
<ons-navigator animation="slide"></ons-navigator>
<script>
  var myNavigator = document.querySelector('ons-navigator');
  myNavigator.setAttribute('animation', 'lift');
</script>
```

* **Properties 属性**：属性`可访问DOM元素`，如访问ons-navigator组件的topPage属性
```js
var myNavigator = document.querySelector('ons-navigator');
console.log(myNavigator.topPage);
```

* **Methods 方法**：方法是触发组件`执行指定动作`
```js
var myNavigator = document.querySelector('ons-navigator');
myNavigator.pushPage('page2.html');
```

* **Events 事件**：
```js
var myNavigator = document.querySelector('ons-navigator');
myNavigator.addEventListener('postpush', function(event) {
  console.log("'pushPage' is completed!", event);
});
```


[翻译自](https://onsen.io/v2/guide/fundamentals.html#fundamentals-onsen-ui-101)

<br>

<br/>

### Page LifeCycle 页面生命周期
---
Onsen UI提供`ons-page生命周期`方法，让我们可以在`合适的时机处理指定操作`，如加载数据、更新视图、销毁前的保存数据等操作。

<br/>

### Events 事件
`ons-page`提供一套DOM事件，在生命周期指定时机中触发
* **init** `ons-page`绑定到DOM后，用于`初始化代码和页面动态内容处理`，页面创建后显示前
* **destroy**：`ons-page`已销毁但未解绑DOM，用于清空或保存处理
* **show**：`ons-page`进入视口时，页面创建然后马上显示或已创建页面显示，用于执行代码每当页面显示
* **hide**：`ons-page`消失于视口，页面销毁或隐藏但仍然存在页面堆中，用于指定代码每当页面消失

页面生命周期事件会在页面中层级地传递，因此显示隐藏销毁都会有影响

因为生命周期事件是正常DOM事件，可以在文档或任意页面的父级元素加入监听器，event对象包含了`页面对象的引用->event.target`

```html
<ons-page id="page1">This is a blank page</ons-page>

<script>
document.addEventListener('init', function(event) {
  if (event.target.matches('#page1')) {
    ons.notification.alert('Page 1 is initiated.');
    // Set up content...
  }
}, false);
</script>
```


<br/>

### Hooks
得益于2.4后的版本支持本地template元素，生命周期hook可以使用，hook的运行方式与相对应的event相似
```html
<template id="page1.html">
  <ons-page>
    <ons-toolbar>
      <div class="center"></div>
    </ons-toolbar>
    <!-- More content here -->

    <script>
      ons.getPageScript().onInit = function() {
        // Set up page's content or anything else
        this.querySelector('ons-toolbar .center').innerHTML = 'Title';

        this.onShow = function() { ... };
        this.onHide = function() { ... };
        this.onDestroy = function() { ... };
      };
    </script>
  </ons-page>
</template>
```
记住一个template只能有一个根节点`ons-page`，template内允许放同步的script标签，
script中的变量`会污染(pollute)全局作用域`中，除非在闭包中


开发者决定选择events还是hooks，event允许从逻辑中分离view而hooks提供更紧凑的方法

[翻译自](https://onsen.io/v2/guide/lifecycle.html)
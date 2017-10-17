### Navigator 导航
ons-navigator元素处理页面堆叠，利用转场动画在当前页之上推送导航页，这是移动端导航的常用方式。

### 结构
首页指向`id为page2.html`的模板，page也可`指向路径`
```html
<ons-navigator page="page2.html"></ons-navigator>
```

模板
```html
<ons-template id="page2.html">
  <ons-page>
    ...
  </ons-page>
</ons-template>
```

### ons-navigator
已试用**属性**

* **page**：首页指向，可以是ons-template的id或者路径
* **animation**：转场动画可选`fade` `lift` `slide` `none`
```html
<ons-navigator animation="fade"></ons-navigator>
```
注意：ios添加的`swipeable`滑动返回上页效果，在android已移除，除非加上`swipeable="force"`

* **swipeable**：启用ios的滑动返回功能
* **swipe-target-width**：距离边缘多少滑动才生效
* **swipe-threshold**：滑动超过多少比例才返回上页，0-1
* **animation-options**：动画效果参数，表达式
```html
<ons-navigator animation-options="{duration: 1, delay: 1, timing: 'ease-in'}"></ons-navigator>
```



已试用**方法**
* **pushPage(page, [options])**：推送页面到页面堆中，push返回promise对象供链式调用，推送的参数可以通过`topPage`进行获取
```js
myNavigator
  .pushPage('page2.html', {data: { title: 'title here'}})
  .then(function(currentPage) {
    ons.notification.alert('Page pushed!');
    alert(myNavigator.topPage.data.title); // title here
  });
```

* **popPage(options)**：返回上一页，或者使用`<ons-back-button>`，按钮会找到navigator然后出发popPage方法
```js
myNavigator
  .popPage()  
```


参考自[ons-navigator](https://onsen.io/v2/api/js/ons-navigator.html)
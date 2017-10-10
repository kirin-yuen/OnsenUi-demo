### Onsen UI 提供3种元素用来组合列表
```html
<ons-list> <!-- 父元素 -->
<ons-list-header> <!-- 子元素，一个list可以有多个header -->
<ons-list-item> <!-- 子元素 -->
```

### 结构
* 简易方式
```html
<ons-list-item>Alice</ons-list-item> <!-- 包含单一文本 -->
渲染成
<div class="center list-item__center">Alice</div>
```
* 三部分方式
```html
<ons-list-item>
  <div class="left">
    <ons-icon icon="md-face" class="list-item__icon"></ons-icon>
  </div>
  <div class="center">
    Icon and switch
  </div>
  <div class="right">
    <ons-switch></ons-switch>
  </div>
</ons-list-item>
```

* 组件属性，所有组件都会有属性，其中`modifier属性`用于处理组件显示方式，使用多个需要用空格分割

特别举例
#### ons-list-item
  * **tappable属性**，让item点击带效果
  * **tap-background-color属性**，让item点击带颜色反馈，android不适用
  * **modifier属性**
      * **tappable**：让item点击有效果，建议使用`attribute的tappable`(因android没效果)
      * **chevron**：item右侧有V形图标，一般搭配attribute的tappable使用
      * **material**：变成安卓material风格，但没ripple效果
    
### Splitter 分割菜单
可配置为`分割(split mode)`或者`折叠模式(collapse mode)`
```html
<ons-splitter> <!-- 父元素，容器-->
<ons-splitter-side> <!-- 子元素，侧边菜单内容 ，左右均可-->
<ons-splitter-content> <!-- 子元素，显示主要内容，应使用ons-page作为根容器-->
```

### 结构
```html
<ons-splitter>
  <ons-splitter-side></ons-splitter-side>
  <ons-splitter-content></ons-splitter-content>
</ons-splitter>
```


#### ons-splitter-side
已试用属性
* **collapse**：控制菜单是否折叠，不加则是`展开状态`
  * **portrait**：竖屏时折叠
  * **landscape**：横屏时折叠
  * **'媒体查询范围'**：当媒体查询返回true则处于折叠状态
    ```html
      <v-ons-splitter-side collapse="screen and (max-width:768px)"></v-ons-splitter-side>
    ```
* **swipe-target-width**：边距多少开始可以滑动
* **animationOptions**：无法使用
* **open-threshold**：滑动多少才可以将菜单呼出，值0-1，1是滑多少都会折叠回去
* **width**：菜单宽度

    
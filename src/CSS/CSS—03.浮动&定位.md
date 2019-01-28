
# 盒子模型

> <p style="font-size:18px">什么是盒子模型</p>
> <p style="color:blue">所有的HTML元素都可以看成是一个盒子，在CSS中利用盒子模型进行设计和布局。</p>

***

> <p style="font-size:18px">盒子模型和属性</p>

![盒子模型](https://github.com/wyd288/fan1111/blob/master/src/images/CSS%E7%AC%94%E8%AE%B0/CSS%E2%80%9403.%E6%B5%AE%E5%8A%A8&%E5%AE%9A%E4%BD%8D-%E7%9B%92%E5%AD%90%E6%A8%A1%E5%9E%8B.png?raw=true)

- Margin(外边距) - 边框外的区域。
- Border(边框) - 围绕在内边距和内容外的边框。
- Padding(内边距) - 内容周围的区域。
- Content(内容) - 盒子的内容，包括文本、图像等。

***

# CSS浮动

> <p style="font-size:18px">什么是标准文档流</p>
> <p style="color:blue">根据块元素或行内元素的特性按从上到下，从左到右的方式自然排列。这也是元素的默认排列方式。</p>

***

> <p style="font-size:18px">CSS使用float属性设置元素浮动</p>

- float(浮动)
    - left
    - right
    - none
- clear（清除浮动）
    - left
    - right
    - both
    - none

***

# CSS定位

> <p style="font-size:18px">什么是css的定位</p>
> <p style="color:blue">通过使用 position 属性对元素进行定位</p>

```css
div {
    <!--设置div元素的定位模式：绝对定位-->
    position:absolute;
    <!--设置偏移量：向右偏移20px-->
    right:20px;
}
```

***

> <p style="font-size:18px">定位的分类</p>

- static(默认定位)
- relative(相对定位)
- absolute(绝对定位)
- fixed(固定定位)

***

> <p style="font-size:18px">定位的详细介绍</p>

- **static(默认定位)**
    - 位置
        - 默认位置
    - 说明
        - 按默认位置出现在标准文档流中

- **relative(相对定位)**
    - 位置
        - top(顶部)
        - left(左侧)
        - right(右侧)
        - bottom(底部)
    - 说明
        - 盒子元素会相对它原来的位置，通过移动指定的偏移量而达到新的位置。
        - 盒子元素仍在标准文档流中（原来位置会被保存下来，不会消失），它对父级盒子与相邻盒子没有影响。
    - 使用场景
        - 很少单独使用，一般都是配合绝对定位创造定位父级元素而又不进行实际偏移。

- **absolute(绝对定位)**
    - 位置
        - top(顶部)
        - left(左侧)
        - right(右侧)
        - bottom(底部)
    - 说明
        - 盒子元素会以离它最近的一个已经定位的‘祖先元素’为基准位置，通过指定的偏移量而达到新的位置。
        - 如果其没有‘祖先元素’，则会以浏览器窗口作为基准位置。
        - 盒子元素脱离标准文档流（原来的位置消失），通过设置z-index的层级值可以覆盖其他元素。
    - 使用场景
        - 一般用在下拉菜单、轮播图、弹出框等。

- **fixed(固定定位)**
    - 位置
        - top(顶部)
        - left(左侧)
        - right(右侧)
        - bottom(底部)
    - 说明
        - 与绝对定位类似，盒子元素以浏览器窗口作为基准位置进行定位。
      
    - 使用场景
        - 一般用固定框、吸顶导航、回到顶部图标、广告等。

***














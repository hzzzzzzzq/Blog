# css 面试题汇总

## 1. flex 布局

- 创建
  父元素属性设置 `display: flex`.

**父属性**

- flex-direction 更改主轴方向
- flex-wrap 是否换行
- flex-flow 是 flex-direction flex-wrap 的缩写
- justify-content 在主轴上的布局
- align-items 在交叉轴上的布局
- align-content 多行在交叉轴上的布局

**子元素属性**

- order 定义项目的顺序，数值越小，排在越前
- flex-grow 放大比例，默认 `0`
- flex-shrink 压缩比例，默认 `1`
- flex-basis 分配多余空间之前，项目占据的主轴空间
- flex 是 flex-grow flex-shrink flex-basis 的缩写
- align-self 可以设置单个子项目在交叉轴上的布局

## 2. img 中 title 和 alt 的区别

- alt 是在图片不能正常显示时出现的文本提示
- title 是鼠标移动在图片上面是，显示的文本

## 3. CSS 创建一个三角形

原理其实也很简单，就是不设置我们容器宽度，只设置边框，就会进行挤压，然后我们让三条边框的颜色呈现透明，就会出现三角形。

```css
.box {
  width: 0;
  heigth: 0;
  border: 40px solid transparent;
  border-bottom: 40px solid red;
}
```

## 4. CSS 盒子模型

可以看看，我写的 `css` 文章 [1. 盒模型]()

设置通过 box-sizing

- 标准模型(默认值 content-box)：元素宽度 = 内容宽度(content) +border+padding
- IE 模型(border-box)：元素宽度 = 内容宽度(content+border+padding)

## 5. 如何让一个 div 水平居中

- block 元素 ，添加 margin:0 auto 属性。
- 已知宽度，绝对定位的居中 ，上下左右都为 0，margin:auto
- 相对定位或绝对定位 left: 50%, tranform: translateX(-50%)，偏移回内部元素宽度的 50%
- flex 布局 jusitify-content: center

## 6. div 垂直居中

- block line-height 同高度
- 相对定位或绝对定位 top: 50% , tranfrom: translateY(-50%) ，偏移回内部元素高度的 50%
- flex 布局 align-items: center

## 7. display:none 和 visibility: hidden 的区别

- `display: none` 隐藏对应的元素，在文档布局中不再给它分配空间
- `visibility: hidden` 隐藏对应的元素，但是在文档布局中仍保留原来的空间

## 8. link 和 @import 区别

- link 属于 HTML 标签，而 @import 是 CSS 提供的
- 页面被加载的时，link 会同时被加载，而 @import 引用的 CSS 会等到页面被加载完再加载
- import 只在 IE5 以上才能识别，而 link 无兼容问题
- link 方式的权重高于 @import 的权重.

## 9. position 的 absolute 与 fixed 共同点与不同点

- 相同：改变行内元素的呈现方式，display 被置为 block 让元素脱离普通流，不占据空间 默认会覆盖到非定位元素上
- 不同： absolute 的”根元素“是可以设置的 fixed 的”根元素“固定为浏览器窗口。当你滚动网页，fixed 元素与浏览器窗口之间的距离是不变的

## 10. css 优先级

- !importtant(无穷大) > 行内样式(10000) > id 选择器(1000) > class/伪类/属性(100) > 标签选择器/伪元素(10) > 通配符(1)
- 行内样式 > 内联样式 & 外联样式

## 11. 清浮动

- clear: both
- 给浮动元素的父级设置高度
- 父级同时浮动
- 父级设置成 inline-block，其 margin: 0 auto 居中方式失效
- 给父级添加 overflow:hidden 清除浮动方法
- 万能清除法 after 伪类 清浮动（现在主流方法，推荐使用）

```css
float_div:after {
  content: '.';
  clear: both;
  display: block;
  height: 0;
  overflow: hidden;
  visibility: hidden;
}
```

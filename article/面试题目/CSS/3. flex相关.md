记录题目： 6，29，38，46





### 6. flex:1 的完整写法是？ 分别是什么意思？

Flex: 1 1auto;

利用flex:1可以实现三个不同内容的div平分空间

```html
<style>
        * {
            margin: 0;
            padding: 0;
        }

        ul {
            display: flex;
            list-style: none;
            border: 4px solid black;
        }

        li {
            flex: 1;
            border: 4px solid red;
            margin: 5px;
        }
    </style>
    <ul>
        <li>1</li>
        <li>2</li>
        <li>3</li>
        <li>4</li>
    </ul>
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210424153913452.png)

#### 6.2 flex 属性

flex属性 flex-grow、flex-shrink、flex-basis的简写，默认值为 0，1，auto

- flex-grow 定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大
- Flex-shrink 定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小
- Flex-basis 给上面两个属性分配多余空间之前，计算项目是否有多余空间，默认为auto，即项目本身的大小

#### 6.3 flex:1 完整写法

Flex:1 的完整写法是

```css
flex-grow:1;
flex-shrink:1;
flex-basis:auto;
```

#### 6.4 flex 赋值情况

- Flex:none

```css
flex-grow:0;
flex-shrink:0;
flex-basis:auto;
```

- Flex:auto

```css
flex-grow:1;
flex-shrink:1;
flex-basis:auto;
```



- Flex: 非负数字

该数字为 flex-grow 的值，flex-shrink为1，flex-basis为0%

```css
flex-grow:1;
flex-shrink:1;
flex-basis:0%;
```



- flex 取值为一个长度或百分比

这时这个值则视为是flex-basis的值，flex-grow为1，flex-shrink为1

```css
.item{
    flex:0%;
}
/* 等价于 */
.item{
    flex-grow:1;
    flex-shrink:1;
    flex-basis:0%;
}

.item2{
    flex:10px;
}
/* 等价于 */
.item2{
    flex-grow:1;
    flex-shrink:1;
    flex-basis:10px;
}
```

- Flex 取两个非负数字

这时则视为flex-grow 和 flex-shrink的值，flex-basis为0%

```css
.item{
    flex:2 3;
}
/* 等价于 */
.item{
    flex-grow:2;
    flex-shrink:3;
    flex-basis:0%;
}
```

- Flex 取值为一个非负数字和一个长度或百分比

这时则视为 flex-grow 和 flex-basis的值，flex-shrink的值为1.



###  29. flex布局，如何实现把八个元素分成两行摆放

- 父盒子排序方式为flex-start，从起点开始放置盒子；通过flex-wrap设置换行
- 子盒子设置，设置 flex: 0 0 25%，flex属性是 flex-grow，flex-shrink，flex-basis的简写，默认值是 0 1 auto
  - flex-grow：默认值0，不放大
  - flex-shrink：默认值0，不缩小
  - flex-basis：项目占据主轴的空间

```html
<style>
	.parent {
		width: 100%;
		height: 150px;
		display: flex;
		flex-wrap: wrap;
		align-content: flex-start;
	}
	.child {
		box-sizing: border-box;
		background-color: white;
		flex: 0 0 25%;
		height: 50px;
		border: 1px solid red;
	}
</style>
<div class="parent">
	<div class="child"></div>
	<div class="child"></div>
	<div class="child"></div>
	<div class="child"></div>
	<div class="child"></div>
	<div class="child"></div>
	<div class="child"></div>
	<div class="child"></div>
</div>
```



### 38. 介绍下flex布局，属性都有哪些，都是干啥的

#### 父元素属性

- display:flex 定义了一个flex容器
- Flex-direction 决定主轴的方向
  - row 默认值，水平从左到右
  - column 垂直从上倒下
  - row-reverse 水平从右到左
  - column-reverse 水平从下到上
- flex-wrap 定义如何换行
  - nowrap 默认值，不换行
  - wrap 换行
  - wrap-reverse 换行，且颠倒行顺序，第一行在下方
- flex-flow 属性是flex-direaction 属性 和 flex-wrap属性的简写形式，默认值是 row nowrap
- justify-content 设置主轴方向上的对齐方式
  - flex-start 默认值，弹性盒子元素将向行起始位置对齐
  - flex-end 弹性盒子元素将向行结束为止对齐
  - center 弹性盒子元素将向行中间位置对齐。改行的子元素将相互对齐并在行中居中对齐
  - space-between 弹性盒子元素会平均地分布在行里，左右定到界面
  - space-around 弹性盒子元素会平均地分布在行里，两端保留子元素和子元素之间间距大小的一半
- align-items 设置或检索弹性盒子子元素在侧轴方向上的对齐方式
  - flex-start 弹性盒子元素的侧轴起始位置的边界紧靠住该行的侧轴起始边界
  - flex-end 弹性盒子元素的侧轴起始位置的边界紧靠住该行的侧轴结束边界
  - center 侧轴 居中
  - baseline 如果弹性盒子元素的行内轴与侧轴为同一条，则该值与flex-start等效。其他情况下，该值将参与基线对齐
  - stretch 如果指定侧轴大小的属性值为：auto，则其值会使项目的边距盒的尺寸尽可能接近所在行的尺寸，但同时会遵照‘min/max-width/height’ 属性的限制
- align-content 设置或检索弹性盒堆叠伸缩行的对齐方式
  - flex-start
  - flex-end
  - center
  - space-between
  - space-around
  - stretch

#### 子元素上属性

- .order 默认情况下flex order 会按照书写顺序呈现，可以通过order属性改变，数值小的在前面，还可以是负数
- flex-grow 设置或检索弹性盒的扩展比率，根据弹性盒子元素所设置的扩展因子作为比率来分配剩余空间
- flex-shrink 设置或检索弹性盒的收缩比率，根据弹性盒子元素所设置的收缩因子作为比率来收缩空间
- flex-basis 设置或检索弹性盒伸缩基准值，如果所以子元素的基准值之和大于剩余空间，则会根据每项设置的基准值，按比率伸缩剩余空间
- flex flex属性是flex-grow，flex-shrink，flex-basis的简写，默认值为 0 1 auto。后两个属性可选。
- align-self 设置或检索弹性盒子元素在侧轴方向上的对齐方式，可以覆盖父容器align-items的设置



### 46. space-between 和 space-around 的区别

space-between 使每个块之间产生相同的间隔，但是不会跟容器之间产生

![image-20210422090155036](/Users/hzq/Library/Application Support/typora-user-images/image-20210422090155036.png)

space-around 则会在每个块的两边产生一个相同大小的间隔，也就是说最外层块和容器之间的间隔大小刚好是两块之间间隔大小的一半

![image-20210422090257273](/Users/hzq/Library/Application Support/typora-user-images/image-20210422090257273.png)

```html
<style>
	* {
		padding: 0px;
		margin: 0px;
	}
	.parent {
		width: 100%;
		height: 150px;
		display: flex;
		flex-wrap: wrap;
		justify-content: space-between;
		/* justify-content: space-around; */
	}
	.child {
		box-sizing: border-box;
		background-color: white;
		width: 100px;
		height: 50px;
		background-color: pink;
	}
</style>
<div class="parent">
	<div class="child"></div>
	<div class="child"></div>
	<div class="child"></div>
</div>
```


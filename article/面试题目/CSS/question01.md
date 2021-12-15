记录题目：1，4,5,7,8,12,13,15,16,22





# 面试题目

### 1. css伪类与伪元素区别

**解释**

- 伪类
  - 其核心就是用来 选择DOM树之外的信息，不能够被普通选择器选择的文档之外的元素，用来添加一些选择器的特殊效果
  - 比如:hover :active :visited :link :visited :first-child :focus :lang等
  - 由于状态的变化是非静态的，所以元素达到一个特定状态时，它可能得到一个伪类的样式；当状态改变时，它又会失去这个样式。
  - 由此可以看出，它的功能和class有些类似，但它是基于文档之外的抽象，所以叫 伪类
- 伪元素
  - DOM树没有定义的虚拟元素
  - 核心就是需要创建通常不存在文档中的元素
  - 比如::before ::after 它选择的是元素指定内容，表示选择元素内容的之前内容或之后内容
  - 伪元素控制的内容和元素是没有差别的，但是它本身只是基于元素的抽象，并不存在于文档中，所以称为伪元素。用于将特殊的效果添加到某些选择器
- 区别
  - 表示方法
    - css2中伪类、伪元素都是以单冒号 `:` 表示
    - css2.1 后规定伪类用单冒号表示，伪元素用双冒号 `::` 表示。
    - 浏览器同样接受css2时代以及存在的伪元素( ::before, :after, :first\ufffeline, :first-letter等) 的单冒号写法
    - css2之后所有新增的伪元素(如 ::selection)，应该采用双冒号的写法。
    - css3中，伪类与伪元素在语法上也有所区别，伪元素修改以::开头。浏览器对以:开头的伪元素也继续支持，但建议规范书写为::开头
  - 定义不同
    - 伪类即假的类，可以添加类来达到效果
    - 伪元素即假元素，需要通过添加元素才能达到效果
  - 总结：
    - 伪类和伪元素都是用来表示文档树以外的"元素"
    - 伪类和伪元素分别用单冒号: 和双冒号::来表示。
    - 伪类和伪元素的区别，关键点在于如果没有伪元素(或伪类)
    - 是否需要添加元素才能达到效果，如果是则是伪元素，反之则是伪类
- 相同之处
  - 伪类和伪元素都不出现在源文件和DOM树中。也就是说在HTML源文件中是看不到伪类和伪元素的，不同之处：
  - 伪类其实就是基于普通DOM元素而产生的不同状态，他是DOM元素的某一特征
  - 伪元素能够创建在DOM树中不存在的抽象对象，而且这些抽象对象是能够访问到的





### 4. css实现div宽度自适应，宽高保持等比缩放

1.1 实现一个自适应浏览器的正方形，宽高比等比缩放

```css
.square{
    width:30%;
    height:30vh;
    background:red;
}
```

优点：简洁方便

缺点：需要注意兼容问题

1.2 使用padding来实现

由于margin，padding的百分比数值是相对父元素的宽度计算的，只需将元素垂直方向的一个padding值设定为与width相同的百分比就可以制作出适应正方形了

但要注意，仅仅设置padding-bottom是不够的，若向容器添加内容，内容会占据一定高度，为了解决这个问题，需要设置height：0.

```css
.square{
    width:30%;
    height:0;
    padding-bottom:30%;
    background:red;
    /* 这样max-height就失效了 */
    /* max-height: 100px */
}
```

优点：简洁明了，兼容性好

缺点：会导致在元素设置上的 max-height 属性失效（max-height 不收缩）

1.3 利用伪元素的 margin-top 撑开容器

Max-height 属性失效的原因是：max-height属性只限制于height，也就是只会对元素的content height起作用。解决方法是：用一个元素撑开content部分的高度，从而使max-height属性生效

首先需要设置为元素，其内容为空，margin-top设置为100%

但要注意，若使用垂直方向上的margin撑开父元素，仅仅设置伪元素是不够的，这涉及到margin collapse外边距合并的概念，由于容器与伪元素在垂直方向发生了外边距合并，所以撑开父元素高度并没有出现，解决方法是在父元素上触发BF：设overflow：hidden。

```css
.square{
    width:30%;
    overflow:hidden;
    background:red;
    /* 这样max-height就生效了 */
    /* max-height: 100px */
}
.square:after{
    content:'';
    display:block;
    margin-top:100%;
}
```

若使用垂直方向上的padding撑开父元素，则不需要触发BFC。子元素的100%就相当于父元素的30%。

```css
.square{
    width:30%;
    overflow:hidden;
    background:red;
    /* 这样max-height就生效了 */
    /* max-height: 100px */
}
.square:after{
    content:'';
    display:block;
    padding-top:100%;
}
```



### 5. ul 内部除最后一个 li 以外设置右边框效果

- last-child

```css
ul li{
  border-right: 1px solid blue;
}

ul li:last-child{
  border-right: unset;
}
```

- nth-last-of-type/nth-last-child

```css
ul li{
  border-right:1px solid blue;
}
ul li:nth-last-of-type(1){
  border-right:unset;
}
/* 或者 */
ul li:nth-last-child(1){
  border-right:unset;
}
```

- not

```css
ul li:not(:last-child) {
  border-right: 1px solid blue;
}
```





### 7. 行内元素和块级元素区别

#### 区别

- 行内元素会在一条直线上排序（默认宽度只与内容有关），都是同一行的，水平方向排列。
- 块级元素各占据一行（默认宽度是它本身父容器的 100%（和父元素的宽度一致），与内容无关），垂直方向排序。块级元素从新行开始，结束接着一个断行。
- 块级元素可以包含行内元素和块级元素。行内元素不能包含块级元素，只能包含文本或者其他行内元素
- 行内元素与块级元素属性的不同，主要是盒模型属性上：行内元素设置width无效，height无效（可以设置line-height），margin上下无效，padding上下无效

#### 互相转换

- `display: block`  字面意思 表现形式设为块级元素
- `display: inline` 字面意思 表现形式设为行内元素



#### 扩展：inline-block

- Inline-block 的元素（如input、img）既具有block元素可以设置宽高的特性，同时又具有inline元素默认不换行的特性。当然不仅仅是这些特性，比如 inline-block 元素也可以设置vertical-align(因为这个垂直对齐属性只对设置了inline-block的元素有效)属性
- HTML 中的换行符、空格符、制表符等合并为空白符，字体大小不为0的情况下，空白符自然占据一定的宽度，使用 inline-block 会产生元素间的空隙



### 8. link 和 @import 区别

#### link样式

链接方式指的是使用 HTML 头部的标签引入外部的CSS文件

```html
<head>
	<link rel="stylesheet" type="text/css" href="style.css">
</head>
```

这是最常见的也是最推荐的引入css的格式。使用这种方式，所有的css代码只存在于单独的css文件中，所以具有良好的可维护性。并且所有的css代码只存在于css文件中，css文件会在第一次加载时引入，以后切换页面时只需要加载HTML文件即可。

#### 导入样式

导入方式指的是使用css规则引入外部css文件。

```html
<style>
	@import url(style.css);
</style>
```

或者在 css样式中

```css
@import(style.css)
*{
	margin:0;
	padding:0;
}
.notice-link a{
  color:#999
}
```

#### 区别

- link是xhtml标签，除了加载css外，还可定义rss等其他事物；@import属于css范畴，只能加载css。
- link引用css时，在页面载入时同时加载；@import需要页面网页完成载入以后加载。所以会出现一开始没有css样式，闪烁一下出现样式后的页面（网速慢的情况下）
- link是xhtml标签，无兼容问题；@import是在css2.1提出的，低版本的浏览器不支持
- link支持使用JS控制DOM去改变样式，而@import不支持



### 9. 屏幕正中间有个元素A，元素A中有文字A，随着屏幕宽度的增加，始终需要满足下列条件

```html
/* 
  A元素垂直居中于屏幕中央
  A元素距离屏幕左右边距各10px
  A元素里面的文字A的font-size:20px；水平垂直居中
  A元素的高度始终是A元素宽度的50%；(如果搞不定可以实现为A元素的高度固定为200px)

  请用html及css实现
*/
```

#### 实现1:

- position+transform 实现水平垂直居中
- padding-top 实现高是宽的 50%

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
      html,
      body {
        padding: 0px;
        margin: 0px;
        height: 100%;
        width: 100%;
      }
      .box {
        width: 100%;
        height: 100%;
        position: relative;
        background-color: cadetblue;
      }
      .A {
        left: 10px;
        right: 10px;
        font-size: 20px;
        text-align: center;
        position: absolute;
        top: 50%;
        transform: translate(0, -50%);
        background-color: chartreuse;
      }
      .aaa {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        background-color: pink;
      }
    </style>
  </head>
  <body>
    <div class="box">
      <div class="A">
        <div class="aaa">AAA</div>
      </div>
    </div>
  </body>
</html>

```



#### 实现二

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>居中</title>
</head>

<body>
  <style>
    * {
      padding: 0;
      margin: 0;
    }

    .A {
      margin: 0 10px;
      text-align: center;
      font-size: 20px;
      position: absolute;
      top: 50%;
      transform: translateY(-50%);
      width: calc(100vw - 20px);
      height: calc(50vw - 10px);
      line-height: calc(50vw - 10px);
      background-color: aquamarine;
    }
  </style>
  <div class="A">
    A
  </div>
</body>

</html>
```

#### 实现三

Flex + 伪元素

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>居中</title>
</head>

<body>
  <style>
    html,
    body {
      padding: 0;
      margin: 0;
      height: 100%;
    }

    body {
      display: flex;
      align-items: center;
    }

    .A {
      flex: 1;
      margin: 0 10px;
      padding-top: 50%;
      position: relative;
      background: #999;
    }

    .A::after {
      content: 'A';
      display: block;
      font-size: 20px;
      position: absolute;
      /* 样式1 */
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);

      /* 样式2 */
      /* top: 0%;
            left: 0%;
            width: 100%;
            height: 100%;
            display: flex;
            align-items: center;
            justify-content: center; */
    }
  </style>
  <div class="A"></div>
</body>

</html>
```



#### 12. css单位都有哪些？

- css 有几个不同的单位用于表示长度，长度由一个数字和单位组成如10px、2em等。
- 数字与单位之间不能出现空格。如果长度值为0，则可以省略单位。
- 对于一些css属性，长度可以是负数。

有两种类型的长度单位：相对和绝对

#### 相对长度单位

绝对长度单位表示为一个固定的值，不会改变。不利于页面渲染。

| 单位 | 描述                                                         |
| ---- | ------------------------------------------------------------ |
| em   | 它是描述相对应用在当前元素的字体尺寸，所以它也是相对长度单位。一般浏览器字体大小默认为16px，则2em == 32px； |
| ex   | 依赖于英文字母小 x 的高度                                    |
| ch   | 数字 0 的宽度                                                |
| rem  | 根元素(html) 的font-size                                     |
| vw   | viewpoint width，视窗宽度，1vw=视窗宽度的1%                  |
| vh   | viewpoint height，视窗度高，1vh=视窗高度的1%                 |
| vmin | vw和vh中较小的那个                                           |
| vmax | vw和vh中较大的那个                                           |

#### 绝对长度单位

绝对长度单位是一个固定的值，它反应一个真实的物理尺寸。绝对长度单位视输出介质而定，不依赖于环境（显示器、分辨率、操作系统等）



| 单位 | 描述                                 |
| ---- | ------------------------------------ |
| cm   | 厘米                                 |
| mm   | 毫米                                 |
| in   | 英寸(1in = 96px = 2.54cm)            |
| px * | 像素(1px = 1/96th of 1 in)           |
| pt   | Point，大约 1/72 英寸；(1pt = 1/72in |
| pc   | Pica，大约6pt，1/6英寸；(1pc = 12pt) |



### 13. css实现多列等高布局，要求元素实际占用的高度以多列中较高的为准

#### flex布局

```html
    <style>
        html,
        body,
        p {
            padding: 0;
            margin: 0;
        }
        .wrap {
            display: flex;
        }
        .item {
            width: 0;
              flex:1;
            margin-right: 5px;
            background-color: brown;
        }
    </style>
    <div class="wrap">
        <div class="item">left</div>
        <div class="item">
            <p>center</p>
            <p>center</p>
            <p>center</p>
            <p>center</p>
            <p>center</p>
            <p>center</p>
        </div>
        <div class="item">right</div>
    </div>
```

#### table-cell 布局

```html
<style>
    html,body,p{
        margin:0;
        padding:0;
    }
    .wrap{
        width:100%;
        display: table;
        background-color: darkgrey;
        table-layout:fixed;
    }
    .left,.centerWrap,.right{
        display: table-cell;
    }
    .left,.right,.center{
        background-color: brown;
    }
    .center{
        margin: 0 10px;
    }
    </style>
    <div class="wrap">
        <div class="left">left</div>
        <div class="centerWrap">
            <div class="center">
                <p>center</p>
                <p>center</p>
                <p>center</p>
                <p>center</p>
                <p>center</p>
                <p>center</p>
            </div>
        </div>
        <div class="right">right</div>
    </div>
```

#### 3. 假等高布局，内外边距底部正负值

```html
<style>
        html,body,p {
            padding: 0;
            margin: 0;
        }
        .wrap {
            overflow: hidden;
            background-color: darkgray;
        }
        .left,.centerWrap,.right {
            float: left;
            width: 33.3%;
            padding-bottom: 9999px;
            margin-bottom: -9999px;
        }
        .left,.center,.right{
            background-color:brown;
        }
        .center{
            margin: 0 10px;
        }
    </style>
    <div class="wrap">
        <div class="left">left</div>
        <div class="centerWrap">
            <div class="center">
                <p>center</p>
                <p>center</p>
                <p>center</p>
                <p>center</p>
                <p>center</p>
                <p>center</p>
                <p>center</p>
            </div>
        </div>
        <div class="right">right</div>
    </div>
```

#### 4. grid布局

```html
   <style>
        html,
        body,
        p {
            margin: 0;
            padding: 0;
        }

        .wrap {
            display: grid;
            grid-template-columns: 33.3% 33.3% 33.3%;
            grid-auto-flow: column;
            grid-gap: 10px;
            background-color: grey;
        }

        .item {
            background-color: brown;
        }
    </style>
    <div class="wrap">
        <div class="item">left</div>
        <div class="item">
            <p>center</p>
            <p>center</p>
            <p>center</p>
            <p>center</p>
            <p>center</p>
        </div>
        <div class="item">right</div>
    </div>
```





### 15. Css 如何实现动画

**CSS实现动画的方式**

- hover实现动画

```css
.div{
    width:100px;
    height:100px;
    background:red;
}
.div:hover{
    width:100px;
    height:100px;
    background:yellow;
}
```

有一个问题，就是元素的状态是立即发生变化的，没有过渡的过程。css3新增的 transition 就很好的解决了这个问题。

- transition

```css
.div{
    width:100px;
    height:100px;
    background:red;
    /* 添加过渡 */
    transition: 1s;
}
.div:hover{
    width:100px;
    height:100px;
    background:yellow;
}
```

这样元素的变化就有了一个过渡的过程

语法：transition: property duration timing-function delay;

property: 规定设置过度效果的css属性名称

duration: 规定完成过渡效果需要多少秒或毫秒

timing-function: 规定速度效果的速度曲线

delay: 定义过渡效果何时开始

上边的代码中没有设置 property，则默认所有发生的变化状态都会应用过渡，如果只需要某个特定属性发生过渡变化，写明就可以了

```css
.div{
    width:100px;
    height:100px;
    background:red;
    /* 多个过渡 */
    transition: background 1s,width 2s,height 3s;
}
.div:hover{
    width:200px;
    height:200px;
    background:yellow;
}
```

- animation

出来transtion 还有一个animation，比transition更加强大，看一下使用方式，同样是实现上边的效果

```css
.div{
    width:100px;
    height:100px;
    background:red;
}
.div:hover{
    animation:div-ani 1s linear;
}
@keyframes div-ani{
    100%{
        width:200px;
        height:200px;
        background:yellow;
    }
}
```

语法： animation: name duration timing-function delay iteration-count direction play-state fill-mode;

name: 用来调用@keyframes定义好的动画，与@keyframes定义的动画名称一致。

duration: 指定元素播放动画所持续的时间

timing-function: 规定速度效果的速度曲线，是针对每一个小动画所在时间范围的变换速率

delay: 定义在浏览器开始执行动画之前等待的时间，值整个animation执行之前等待的时间

iteration-count: 定义动画的播放次数，可选具体次数或无限

direction: 设置动画播放方向：normal(按时间轴顺序)，reverse(时间轴反方向运行)，alternate(轮流，即来回往复进行)，alternate-reverse(动画先反运行再正方向运行，并持续交替运行)

Play-state: 控制元素动画的播放状态，通过此来控制动画的暂停和继续，两个值：running（继续，paused（暂停

fill-mode：控制动画结束后，元素的样式

- Animation 与 transition 的不同

Keyframes 提供更多的控制，尤其是 时间轴的控制，这点让css animation更加强大，使得flash的部分动画效果可以由css直接控制完成，而这一切，仅仅只需要几行代码，也因此诞生了大量基于css的动画库，用来取代flash的动画部分。

- css动画实现中常用的一些易混淆的概念
  - amimation：用于设置动画属性，它是一个简写的属性，包含六个属性
  - transition：用于设置元素的样式过渡，和anmation有着类似的效果，但细节上有很大的不同
  - transform：用于元素进行旋转、缩放、移动或倾斜，和设置样式的动画并没有什么关系，就相当于color一样用来设置元素的外表
  - translate：translate只是transform的一个属性值，即移动





### 16. 如何实现一个半圆

设置两个 border-radius即可

```css
/* 上半圆 */
.box{
  with: 50px
	border-radius: 25px 25px 0px 0px;
}

```



### 22. 上下固定，中间滚动布局如何实现

1. flex实现

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>flex</title>
    <style>
        html,
        body {
            padding: 0;
            margin: 0;
            height: 100%;
        }

        .wrap {
            display: flex;
            height: 100%;
            flex-direction: column;
        }
        .header,.footer{
            height:40px;
            line-height:40px;
            text-align: center;
            background-color:cadetblue;
        }
        .main{
            flex:1;
            background-color:chocolate;
            overflow:auto;
            text-align: center;
        }
    </style>
</head>

<body>
    <div class="wrap">
        <div class="header">header</div>
        <div class="main">
            main
            <div style="height: 2000px;"></div>
        </div>
        <div class="footer">footer</div>
    </div>
</body>

</html>
```

2. 绝对定位



```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>position</title>
    <style>
        html,
        body {
            padding: 0;
            margin: 0;
            height: 100%;
        }

        .header,
        .footer {
            position: absolute;
            width: 100%;
            height: 40px;
            line-height: 40px;
            text-align: center;
            background-color: chocolate;
        }

        .header {
            top: 0;
            left: 0;
        }

        .footer {
            bottom: 0;
            left: 0;
        }

        .main {
            width: 100%;
            position: absolute;
            top: 40px;
            left: 0;
            bottom: 40px;
            right: 0;
            background-color: cadetblue;
            overflow:auto;
            text-align:center;
        }
    </style>
</head>

<body>
    <div class="wrap">
        <div class="header">header</div>
        <div class="main">
            main
            <div style="height:2000px;"></div>
        </div>
        <div class="footer">footer</div>
    </div>
</body>

</html>
```










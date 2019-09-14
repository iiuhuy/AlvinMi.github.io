# CSS 揭秘

## CSS3 的诸多模块

CSS2 原有模块：

- [CSS 语法](http://w3.org/TR/css-syntax-3)
- [CSS 层叠与继承](http://w3.org/TR/css-cascade-3)
- [CSS 颜色](http://w3.org/TR/css3-color)
- [选择符](http://w3.org/TR/selectors)
- [CSS 背景与边框](http://w3.org/TR/css3-background)
- [CSS 值与单位](http://w3.org/TR/css-values-3)
- [CSS 文本排版](http://w3.org/TR/css-text-3)
- [CSS 文本装饰效果](http://w3.org/TR/css-text-decor-3)
- [CSS 字体](http://w3.org/TR/css3-fonts)
- [CSS 基本 UI 特性](http://w3.org/TR/css3-ui)

CSS3 新增：

- [CSS transforms](http://w3.org/TR/css-transforms-1)
- [图像混合效果](http://w3.org/TR/compositing-1)
- [滤镜效果](http://w3.org/TR/filter-effects-1)
- [CSS 遮罩](http://w3.org/TR/css-masking-1)
- [CSS flexbox 布局](http://w3.org/TR/css-flexbox-1)
- [CSS 网格布局](http://w3.org/TR/css-grid-1)

浏览器前缀，最常见的前缀分别是

```css
Firefox:  -moz-
IE: -ms-
Opera:  -o-
Safari:  -webkit-
Chrome:  -webkit-
```

为了解决

一条规范正式添加到规范中，会有一些实验性的特性。网页开发者可以根据浏览器给的前缀自由的添加相关特性，并将试用结果返还给工作组。结果开发者发现，这些有了前缀的特性能轻易的实现以前需要大费周折所实现的效果，所以，这些特性就被滥用。后来发现只写出当前适用的新特性时，还需要时不时回来打补丁，后来干脆将所有可能的浏览器前缀添加上去变成这样:

```css
-moz-border-radius: 10px;
-ms-border-radius: 10px;
-o-border-radius: 10px;
-webkit-border-radius: 10px;
border-radius: 10px;
```

CSS 编码技巧

尽量减少代码重复。在实践中，代码可维护性的最大要素是**尽量减少改动时要编辑的地方**。

关于响应式网页设计

- 1.媒体查询(MediaQuery)的断点不应该由具体的设备来决定，而应该根据设计自身来决定；
- 2.使用百分比长度来取代长度，实在不行也应该尝试使用与视口相关的单位(vm,vh,vmin,vmax)；
- 3.需要在较大分辨率下得到固定宽度时，使用 `max-width` 而不是 `width`，原因是可以适应较小的分辨率，而无需使用媒体查询;；
- 4.为替换元素(imag,object.video.iframe 等)设置一个 `max-width`,值为 100%；
- 5.背景图片 `background-size: cover` 属性不管容器尺寸如何变化都可以完整平铺，但是通过 CSS 把大图缩小会小号带宽；
- 6.图片或其他元素行列式布局时， 弹性盒布局(Flexbox) 或 `display: inline-block`布局；
- 7.多列文本，指定 `column-width`（列宽）而不是指定 `column-count`（列数）。

合理使用简写，是良好的防卫性编码方式，可以抵御未来的风险。

```css
background: rebeccapurple;
background-color: rebeccapurple;
```

要明确地去覆盖某个具体的展开式属性并保留其他相关央视就需要使用展开式属性。

## 2.背景与边框

### 2.1.半透明边框

> 背景知识: RGBA/HSLA 颜色

**难题**

最早可能是这样来实现半透明边框：

```CSS
border: 10px solid hsla(0,0%,100%,.5);
background: white;
```

但是却没有实现实现半透明边框？

**解决方案**

其实边框是存在的，默认情况下背景会延伸到边框所在的区域下层。我们需要做的是让 body 的背景从半透明白色边框透出来，可以通过 `background-clip` 来调整上述的特性，这个属性的初始值是 `border-box`, 意味着背景会被元素的 `border-box`（即边框的外沿框）裁切掉。我们修改为 `padding-box` 就可以用内边距的外沿来把背景裁切掉。

```css
border: 10px solid hsla(0, 0%, 100%, 0.5);
background: white;
bcakground-clip: padding-box;
```

> 相关规范： https://www.w3.org/TR/css-backgrounds/

### 2.2.多重边框

> 背景知识： box-shadow 的基本用法

**难题**

多重边框，当时一致认为这特性没有足够多的使用场景。

**box-shadow 方案**

我们需要了解 `box-shadow` 的第四个参数，称为 **扩张半径**, 可以让投影面积变大或者变小。

好处(优点)：支持逗号分隔语法，可以创建任意数量的投影。

```css
background: yellowgreen;
box-shadow: 0 0 0 10px #655, 0 0 0 15px deeppink;
```

box-shadow 是层层叠加的，第一层投影位于最顶端，以此类推。

缺点：

- 1.投影的行为和边框不一致；
- 2.假投影出现元素外圈，不会影响相关事件。

试一试： http://play.csssecrets.io/multiple-borders

**outline 方案**

某些情况下，只需要两层边框。可以在设置常规的边框后添加 `outline` 描边。优点是 `outline` 十分灵活，而 `box-shadow` 只能模拟实现边框。

```CSS
background: yellowgreen;
border: 10px solid #655;
outline: 5px solid deeppink;
```

缺点：

- 1.只适用于双层边框；
- 2.边框不一定贴合 `border-radius` 产生的圆角；
- 3.尽管说描边可以不是矩形，但大多数情况需要测试(最好在不同浏览器中完整地测试)。

### 2.3.灵活的背景定位

**难题**

很多时候，我们想针对容器的某个角对背景图案做偏移定位，例如想要类似内边距的效果怎么做呢。

**background-position 的扩展语法方案**

```css
background: url(...) no-repeat #58a;
background-position: right 20px bottom 10px;

/* 回退方案 */
background: url(...) no-repeat bottom right #58a;
background-position: right 20px bottom 10px;
```

试一试： http://play.csssecrets.io/extended-bg-position

**background-origin 方案**

需要图片的偏移量和内边距相同时。

```css
padding: 10px;
background: url(...) no-repeat #58a;
background-position: right 10px bottom 10px;
```

但是每次改动边距的值时，都需要改三个地方的值。

使用另一个更简单的方法实现：

```CSS
padding: 10px;
background: url(...) no-repeat #58a bottom right;
background-origin: content-box;
```

**calc() 方案**

```css
background: url(...) no-repeat;
background-position: calc(100% - 20px) calc(100% - 10px);
```

### 2.4.边框内圆角

> 背景知识：box-shadow、outline、多重边框

**难题**

有时我们需要一个容器，只在内侧有圆角，而边框或描边的四个角在外部依然保持矩形的形状。这里放弃两个 div 元素的方案。

**解决方案**

两个 `div` 的确很优秀，如果我们只是需要纯色的边框，只需要一个元素的方法呢。

```CSS
background: tan;
border-radius: .8em;
padding: 1em;
box-shadow: 0 0 0 .6em #655
outline: .6em solid #655
```

主要就是利用 `box-shadow` 的扩展半径填充元素与 `outline` 之间的缝隙。
根据勾股定理大约取值为半径的一半。

相关规范：

- CSS 背景与边框：https://w3.org/TR/css-backgrounds
- CSS 基本 UI 特性：http://w3.org/TR/css3-ui

试一试： http://play.csssecrets.io/inner-rounding

### 2.5.条纹背景

> 背景知识：CSS 线性渐变， background-size

**难题**

简单的条纹背景，我们用 CSS 自己创建。

**解决方案**

1.水平条纹

```CSS
background: linear-gradient(#fb3 33.3%, #58a 0, #58a 66.6%, yellowgreen 0);
background-size: 100% 45px
```

避免每次修改条纹宽度的捷径：如果某个色标的位置值比整个列表中在它之前的色标的位置值都要小，则该色标的位置值会被设置为它前面所有色标位置值的最大值。

2.垂直条纹

```CSS
linear-gradient(to right, /* 或 90deg*/ #fb3 50%, #58a 0);
background-size: 30px 100%;
```

3.斜向条纹

由于贴片问题，我们需要设置四个色块。贴片的面积也需要重新计算相当于 1.4 倍的需要的半径。

```CSS
background: linear-gradient(45deg, #fb3 25%, #58a 0, #58a 50%, #fb3 0, #fb3 75%, #58a 0);
background: 42px 42px;
```

4.更好的斜向条纹

`linear-gradient()` 和 `radial-gradient()` 还有循环加强版：`repeating-linear-gradient()` 和 `repeating-radial-gradient()`

```CSS
background: repeating-linear-gradient(60deg, #fb3, #fb3 15px, #58a 0, #58a 30px);
```

5.灵活的同色系条纹

```CSS
background: #58a;
background-image: repeating-linear-gradient(30deg, hsla(0,0%,100%,.1), hsla(0,0%,100%,.1) 15px, transparent 0, transparent 30px)
```

利用 transparent 实现条纹的深色，直接显示背景。

### 2.6.复杂的背景图案

> 背景知识：CSS 渐变，“条纹背景”

**难题**

不仅仅有各种条纹图案，一些稍复杂的几何图案，CSS 也能实现。

1.网格

```CSS
background: white;
background-image: linear-gradient(90deg, rgba(200,0,0,05) 50%, transparent 0),linear-gradient(rgba(200,0,0,05) 50%, transparent 0);
background-size: 30px 30px;
/* 长度单位线条 */
background: #58a;
background-image:
  linear-gradient(white 1px, transparent 0),
  linear-gradient(90deg, white 1px, transparent 0);
background-size: 30px 30px;
```

2.波点

直接放上波点的 mixin, 波点需要两个贴片重叠。

```CSS
@mixin polka($size, $dot, $base, $accent) {
  background: $base;
  background-image:
    radial-gradient($accent $dot, transparent 0),
    radial-gradient($accent $dot, transparent 0);
  background-size: $size $size;
  background-position: 0 0, $size/2 $size/2;
}
/* 调用例子 */
@include polka(30px, 30%, #655, tan)
```

3.棋盘

emmm，这里也只放上 mixin, 它也需要贴片的重叠。

```CSS
@mixin checkerboard($size, $base, $accent: rgba(0,0,0,.25)) {
  background: $base;
  background-image:
    linear-gradient(45deg,
      $accent 25%, transparent 0,
      transparent 75%, $accent 0)
    linear-gradient(45deg,
      $accent 25%, transparent 0,
      transparent 75%, $accent 0)
    background-position: 0 0, $size $size,
    background-size: 2*$size 2*$size;
}
/* 调用 */
@include checkerboard(15px, #58a, tan);
```

### 2.7.伪随机背景

> 背景知识：CSS 渐变，“条纹背景”，“复杂的背景图案”

**难题**

其实自然界的事物都不是以无限平铺的方式存在的。CSS 本身没有提供随机功能。

**解决方案**

通过质数来增加随机真实性，多个质数的话，那么只有经过这几个质数相乘才会重复一次。

### 2.8.连续的图像边框

> 背景知识：CSS 渐变，基本的 border-image，“条纹背景”，基本的 CSS 动画

**难题**

有时我们想把一副图案或者图片应用为边框，而不是背景。

**解决方案**

在石雕背景图案之上，再叠加一层纯色的实色背景。给两层背景指定不一样的 background-clip 值，实色用 css 渐变来实现。

```CSS
/* background-origin 消除拼接效果。 */
padding: 1em;
border: 1em solid transparent;
background: linear-gradient(white, white),
            url(...);
background-size: cover;
background-clip: padding-box, border-box;
background-origin: border-box;

/* 简写 */
padding: 1em;
border: 1em solid transparent;
background:
  linear-gradient(white, white) padding-box,
  url(...) border-box 0 / cover;

/* 信封边框图案 */
padding: 1em;
border: 16px solid transparent;
border-image: 16 repeating-linear-gradient(-45deg,
                    red 0, red 1em,
                    transparent 0, transparent 2em,
                    #58a 0, #58a 3em,
                    transparent 0, transparent 4em);
```

如果利用动画还能形成蚂蚁行军效果。即选中不停转动的虚线框。

```CSS
@keyframes ants {to {background-position: 100%}}

.marching-ants {
  padding: 1em;
  border: 1px solid transparent;
  background:
    linear-gradient(white, white) padding-box,
    repeating-linear-gradient(-45deg,
      black 0, black 25%, white 0, white 50%
      ) 0 / .6em .6em;
  animation: ants 12s linear infinite;
}
```

## 3.形状

### 3.1.自适应的椭圆

> 背景知识：border-radius 属性的基本用法

**难题**

设置一个自适应的椭圆，根据内容自动调整并适应。如果它的宽高相等，就显示为一个圆；如果宽高不等，就显示为一个椭圆。

解决方案:

`border-radius`，可以单独指定水平和垂直半径，只要用一个斜杠分开。

```css
border-radius: 50% / 50%;
/* 可以简写为 */
border-radius: 50%;
```

试一试： http://play.csssecrets.io/ellipse

**其他椭圆**

```CSS
/* 半椭圆 */
border-radius: 50% / 100% 100% 0 0;

/* 沿纵轴劈开的半椭圆 */
border-radius: 100% 0 0 100% / 50%;

/* 四分之一椭圆 */
border-radius: 100% 0 0 0;
```

### 3.2.平行四边形

> 背景知识：基本的 CSS 变形

**难题**

平行四边形可以通过 skew() 的变形属性来对这个矩形进行斜向拉伸，这导致它的内容也发生了斜向变形，这很不好看，而且难读，有没有办法只让容器的形状倾斜，而保持其内容不变呢？

**嵌套元素方案**

我们可以对内容再应用一次反向的 skew() 变形，从而抵消容器的变形效果，缺点：需要添加一层层额外的 HTML 元素来包裹内容。

```html
<a href="#yolo" class="button"><div>Click me</div></a>

.button { transform: skewX(-45deg) } .button > div { transform: skewX(45deg); }
```

试一试: http://play.csssecrets.io/parallelograms

**伪元素方案**

```CSS
.button {
 position: relative;
 /* 其他的文字颜色、内边距等样式…… */
}
.button::before {
 content: ''; /* 用伪元素来生成一个矩形 */
 position: absolute;
 top: 0; right: 0; bottom: 0; left: 0;
 z-index: -1;
 background: #58a;
 transform: skew(45deg);
}
```

适用其他任何变形样式，当我们想变形一个元素而不想变形它的内容时就可以用到它。

### 3.3.菱形图片

> 背景知识: CSS 变形，“平行四边形”

**难题**

在视觉设计中，把图片裁切为菱形是一种常见的设计手法，但在 CSS 中还没有一种简单直观的方法来实现它。事实上，直到最近，这种效果才基本成为可能。当网页设计师想要实现这种设计风格时，他们通常不希望在图像处理软件中预先把图片裁好。显然不用说你也知道，这个方法的可维护性并不好。如果未来有人想修改图片风格，将很难增加其他效果，而且最终往往会搞得一团糟。

**基于变形的方案**

和平行四边形类似，需要把图片用一个包裹起来，然后对其应用相反的 `rotate()` 变形样式，这个方法不是推荐的方法。

**裁切路径方案**

使用 `clip-path` 属性。这个特性也是从 SVG 那里借鉴而来，已经可以应用在 HTML 元素上了(至少对于支持的浏览器来说是这样的)。

这里将会使用 `polygon()`(多边形)函数来指定一个菱形。实际上，它允许我们用一系列(以逗号分隔的)坐标点来指定任意的多边形。

```css
img {
  clip-path: polygon(50% 0, 100% 50%, 50% 100%, 0 50%);
  transition: 1s clip-path;
}
img:hover {
  clip-path: polygon(0 0, 100% 0, 100% 100%, 0 100%);
}
```

### 3.4.切角效果

> 背景知识: CSS 渐变，background-size，“条纹背景”

**难题**

最常见的形态是把元素的一个或多个角切成 45° 的缺口(也称作斜面切角)。

**解决方案**

1.CSS 渐变

```CSS
background: #58a;
background:
 linear-gradient(135deg, transparent 15px, #58a 0)
 top left,
 linear-gradient(-135deg, transparent 15px, #58a 0)
 top right,
 linear-gradient(-45deg, transparent 15px, #58a 0)
 bottom right,
 linear-gradient(45deg, transparent 15px, #58a 0)
 bottom left;
background-size: 50% 50%;
/* 如果不设置的话，背景会相互覆盖 */
background-repeat: no-repeat;
/* 如果不设置，每层渐变图案各自平铺了两次 */
```

如果用 SCSS 来写，使用 mixin，在需要用到的时候直接调用：

```SCSS
@mixin beveled-corners($bg,
 $tl:0, $tr:$tl, $br:$tl, $bl:$tr) {
 background: $bg;
 background:
 linear-gradient(135deg, transparent $tl, $bg 0)
 top left,
 linear-gradient(225deg, transparent $tr, $bg 0)
 top right,
 linear-gradient(-45deg, transparent $br, $bg 0)
 bottom right,
 linear-gradient(45deg, transparent $bl, $bg 0)
 bottom left;
 background-size: 50% 50%;
 background-repeat: no-repeat;
}
// 调用 传入 2~5 个参数：
@include beveled-corners(#58a, 15px, 5px);
```

**弧形切角 方案**

很多人也把这种效果称为 **内凹圆角**，因为它看起来就像是圆角的反向版本。用径向渐变来替代上述线性渐变：

```css
background: #58a;
background: radial-gradient(circle at top left, transparent 15px, #58a 0) top left,
  radial-gradient(circle at top right, transparent 15px, #58a 0) top right,
  radial-gradient(circle at bottom right, transparent 15px, #58a 0) bottom right,
  radial-gradient(circle at bottom left, transparent 15px, #58a 0) bottom left;
background-size: 50% 50%;
background-repeat: no-repeat;
```

**内联 SVG 与 border-image 方案**

```css
border: 20px solid transparent;
border-image: 1 url('data:image/svg+xml,\
 <svg xmlns="http://www.w3.org/2000/svg"\
 width="3" height="3" fill="%2358a">\
 <polygon points="0,1 1,0 2,0 3,1 3,2 2,3 1,3 0,2"/>\
 </svg>');
background: #58a;
background-clip: padding-box;
```

**裁切路径方案**

还是利用 `clip-path` 属性。

```css
background: #58a;
clip-path: polygon(
  20px 0,
  calc(100% - 20px) 0,
  100% 20px,
  100% calc(100% - 20px),
  calc(100% - 20px) 100%,
  20px 100%,
  0 calc(100% - 20px),
  0 20px
);
```

补充多边形裁剪-参考大漠老师写的：https://www.w3cplus.com/preprocessor/creat-css-polygon-wiht-border-and-clip-path-property.html

### 3.5.体型标签页

> 背景知识：基本的 3D 变形，“平行四边形”

**难题**

一直以来，梯形都是众所周知难以用 CSS 生成的形状，尽管它也十分常用，尤其是对于标签页来说。

**解决方案**

利用 CSS 中用 3D 旋转来模拟出这个效果 `transform: perspective(.5em) rotateX(5deg);`。

对元素使用了 3D 变形之后，其内部的变形效应是 _不可逆转_ 的，这里我们像上一节利用伪类就好了。而给元素应用变形效果会让这个元素以它自身的中心线为轴进行空间上的旋转。所以我们需要设置 `transform-origin` 属性。`transform-origin:bottom;`，当它在 3D 空间中旋转时，可以把它的底边固定住。

```css
nav > a {
  position: relative;
  display: inline-block;
  padding: 0.3em 1em 0;
}
nav > a::before {
  content: "";
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: -1;
  background: #ccc;
  background-image: linear-gradient(
    hsla(0, 0%, 100%, 0.6),
    hsla(0, 0%, 100%, 0)
  );
  border: 1px solid rgba(0, 0, 0, 0.4);
  border-bottom: none;
  border-radius: 0.5em 0.5em 0 0;
  box-shadow: 0 0.15em white inset;
  transform: perspective(0.5em) rotateX(5deg);
  transform-origin: bottom;
}
```

### 3.6.简单的饼图

> 背景知识: CSS 渐变，基本的 SVG，CSS 动画，“条纹背景”，“自适应的椭圆”

**难题**

饼图在网页中的运用极为普遍，比如简单的统计图表、进度指示器、定时器等。

**基于 transform 的解决方案**

三个遮罩层的互相重叠。

```css
.pie {
  position: relative;
  width: 100px;
  line-height: 100px;
  border-radius: 50%;
  background: yellowgreen;
  background-image: linear-gradient(to right, transparent 50%, #655 0);
  color: transparent;
  text-align: center;
}
@keyframes spin {
  to {
    transform: rotate(0.5turn);
  }
}
@keyframes bg {
  50% {
    background: #655;
  }
}
.pie::before {
  content: "";
  position: absolute;
  top: 0;
  left: 50%;
  width: 50%;
  height: 100%;
  border-radius: 0 100% 100% 0 / 50%;
  background-color: inherit;
  transform-origin: left;
  animation: spin 50s linear infinite, bg 100s step-end infinite;
  animation-play-state: paused;
  animation-delay: inherit;
}
```

**SVG 解决方案**

一个圆形：

```svg
<svg width="100" height="100">
<circle r="30" cx="50" cy="50" />
</svg>
```

给它一些基本的样式

```css
circle {
  fill: yellowgreen;
  stroke: #655;
  /* stroke: 描边颜色 */
  stroke-width: 30;
  /* stroke-width：描边宽度 */
}
```

这里我们还需要了解一个属性 `stroke-dasharray`，它是为虚线描边而准备的。`stroke-dasharray`，第一个参数是线段长度，第二个是间隙长度。当我们把这个虚线描边的线段长度指定为 0，并且把虚线间隙的长度设置为等于或大于整个圆周的长度时，答案就会浮出水面了。(这里做个简单的计算，圆形的周长 C = 2πr，因此在这里 C= 2π × 30 ≈ 189)

然后可以优化，给这个圆形指定一个特定的半径，从而让它的周长无限接近 100，这样就可以直接把比率的百分比值指定为 strokedasharray 的长度，不需要做任何计算了。

```css
<svg viewBox="0 0 32 32" > <circle r="16" cx="16" cy="16" / > </svg > svg {
  width: 100px;
  height: 100px;
  transform: rotate(-90deg);
  background: yellowgreen;
  border-radius: 50%;
}
circle {
  fill: yellowgreen;
  stroke: #655;
  stroke-width: 32;
  stroke-dasharray: 38 100; /* 可得到比率为38%的扇区 */
}
```

## 4.视觉效果

### 4.1.单侧投影

**难题**

如何只在元素的一侧(偶尔是两侧)设置投影。

**box-shadow 解决方案**

```css
box-shadow: 0 5px 4px -4px black;
```

**邻边投影**

```css
/* 一层藏起来，另一侧自然漏出 */
box-shadow: 3px 3px 6px -3px black;
```

**双侧投影**

```css
box-shadow: 5px 0 5px -5px black, -5px 0 5px -5px black;
```

### 4.2.不规则投影

> 背景知识 box-shadow

**难题**

当我们想给一个矩形或其他能用 `border-radius` 生成的形状（在 “自适应的椭圆” 一节中可以看到一些示例）加投影时，`box-shadow` 的表现都堪称完美。但是，当元素添加了一些伪元素或半透明的装饰之后，它就有些力不从心了，因为 `border-radius` 会无耻地忽视透明部分。

**解决方案**

滤镜效果规范(http://w3.org/TR/filter-effects), 为这个问题提供了一个解决方案。`filter` 就是我们需要的属性，我们甚至可以用多个滤镜。

`drop-shadow()` 滤镜可接受的参数基本上跟 `box-shadow` 属性是一样的，不包括 `inset` 关键字，也不支持逗号分割的多层投影语法。

### 4.3.染色效果

> 背景知识: HSL 色彩模型，background-size

**难题**

为一幅灰度图片(或是被转换为灰度模式的彩色图片)增加染色效果(color tint)，是一种流行且优雅的方式，可以给一系列风格迥异的照片带来视觉上的一致性。

常见的解决方法就是给图层上面添加一层半透明的实色背景，但减少了图片的对比度。

**基于滤镜的方案**

参考：https://developer.mozilla.org/zh-CN/docs/Web/CSS/filter

**基于混合模式的方案**

**混合模式** 控制了上层元素的颜色与下层颜色进行混合的方式。要对一个元素设置混合模式，有两个属性可以派上用场：`mix-blendmode` 可以为整个元素设置混合模式，`background-blend-mode` 可以为每层背景单独指定混合模式。

缺点：

- 1.图片的尺寸需要在 CSS 代码中写死；
- 2.在语义上，这个元素并不是一张图片，因此并不会被读屏器之类的设备读出来。

### 4.4.毛玻璃效果

> 背景知识: RGBA/HSLA 颜色

**难题**

半透明颜色最初的使用场景之一就是作为背景。将其叠放在照片类或其他花哨的背层之上，可以减少对比度，确保文本的可读性。这种效果确实很有视觉冲击力，但仍然可能导致文字很难阅读。

**解决方案**

```css
body,
main::before {
  background: url("tiger.jpg") 0 / cover fixed;
}
main {
  position: relative;
  background: hsla(0, 0%, 100%, 0.3);
  overflow: hidden;
}
main::before {
  content: "";
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  filter: blur(20px);
  margin: -30px;
}
```

存在问题：

- 1.伪元素现在就覆盖在内容元素之上。可以用 `z-index: -1;` 来修正这个问题；
- 2.`blur` 模糊效果在中心区域看起来非常完美，但在接近边缘处会逐渐消退。为了补偿这种情况，我们需要让伪元素相对其宿主元素的尺寸再向外扩大至少 20px（即它的模糊半径）这里取 30px。
- 3.上一个解决方法会导致一圈模糊效果超出了容器。只要对 `main` 元素应用 `overflow: hidden;`，就可以把多余的模糊区域裁切掉了。

### 4.5.折角效果

> 背景知识: CSS 变形，CSS 渐变，“切角效果 “

**难题**

把元素的一个角(通常是右上角或右下角)处理为类似折角的形状，再配上或多或少的拟物样式。

**45° 折角的解决方案**

```css
background: #58a; /* 回退样式 */
background: linear-gradient(-135deg, transparent 2em, #58a 0);
```

增加一个暗色的三角形来实现翻折效果。

```css
background: #58a; /* 回退样式 */
background: linear-gradient(
      to left bottom,
      transparent 50%,
      rgba(0, 0, 0, 0.4) 0
    ) no-repeat 100% 0 / 2em 2em, linear-gradient(
    -135deg,
    transparent 1.5em,
    #58a 0
  );
```

**其他角度的解决方案**

直接放 `mixin`

```scss
@mixin folded-corner($background, $size, $angle: 30deg) {
  position: relative;
  background: $background; /* 回退样式 */
  background: linear-gradient(
    $angle - 180deg,
    transparent $size,
    $background 0
  );
  border-radius: 0.5em;
  $x: $size / sin($angle);
  $y: $size / cos($angle);
  &::before {
    content: "";
    position: absolute;
    top: 0;
    right: 0;
    background: linear-gradient(
        to left bottom,
        transparent 50%,
        rgba(0, 0, 0, 0.2) 0,
        rgba(0, 0, 0, 0.4)
      ) 100% 0 no-repeat;
    width: $y;
    height: $x;
    transform: translateY($y - $x) rotate(2 * $angle - 90deg);
    transform-origin: bottom right;
    border-bottom-left-radius: inherit;
    box-shadow: -0.2em 0.2em 0.3em -0.1em rgba(0, 0, 0, 0.2);
  }
}

/* 当调用时... */
.note {
  @include folded-corner(#58a, 2em, 40deg);
}
```

## 5.字体排印

### 5.1.连字符断行

CSS 文本（第三版）引入了一个新的属性 hyphens。它接受三个值：none、manual 和 auto。manual 是它的初始值，其行为正好对应了现有的工作方式：我们可以在任何时候手工插入软连字符，来实现断词折行的效果。

```css
hyphens: auto;
```

试一试： http://play.csssecrets.io/hyphenation

### 5.2.插入换行

通过 CSS 来插入换行的需求通常与定义列表有关, 利用伪类。

```css
dd + dd::before {
  content: ", ";
  margin-left: -0.25em;
  font-weight: normal;
}
```

试一试： http://play.csssecrets.io/line-breaks

### 5.3.文本的斑马条纹

> 背景知识: CSS 渐变，background-size，“条纹背景”，“灵活的背景定位”

**难题**

想把表格行的这种 _斑马条纹_ 效果，应用到文本行时，就有点力不从心。

```css
tr:nth-child(even) {
  background: rgba(0, 0, 0, 0.2);
}
```

**解决方案**

我们可以在 CSS 中用渐变直接生成背景图像，为了让背景自动跟着内边距的宽度走，我们需要在解析 `background-position` 时以 `content box` 的外沿作为基准。

```css
padding: 0.5em;
line-height: 1.5;
background: beige;
background-size: auto 3em;
background-origin: content-box;
background-image: linear-gradient(rgba(0, 0, 0, 0.2) 50%, transparent 0);
```

### 5.4.调整 tab 的宽度

**难题**

调整网页 code 的宽度。

**解决方案**

利用新属性。

```css
pre {
  tab-size: 2;
}
```

# CSS 揭秘

### CSS3 的诸多模块

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

尽量减少代码重复。在实践中，代码可维护性的最大要素是**尽量减少改动时要编辑的地方。**
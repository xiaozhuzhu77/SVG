# SVG 可缩放矢量图形（Scalable Vector Graphics）

##  什么是SVG？

* SVG 指可伸缩矢量图形 (Scalable Vector Graphics)
* SVG 用来定义用于网络的基于矢量的图形
* SVG 使用 XML 格式定义图形
* SVG 图像在放大或改变尺寸的情况下其图形质量不会有所损失
* SVG 是万维网联盟的标准
* SVG 与诸如 DOM 和 XSL 之类的 W3C 标准是一个整体

## SVG 的优势

与其他图像格式相比，使用 SVG 的优势在于：

* SVG 可被非常多的工具读取和修改（比如记事本）
* SVG 与 JPEG 和 GIF 图像比起来，尺寸更小，且可压缩性更强。
* SVG 是可伸缩的
* SVG 图像可在任何的分辨率下被高质量地打印
* SVG 可在图像质量不下降的情况下被放大
* SVG 图像中的文本是可选的，同时也是可搜索的（很适合制作地图）
* SVG 可以与 Java 技术一起运行
* SVG 是开放的标准
* SVG 文件是纯粹的 XML

## Canvas 和 SVG 的区别：

### SVG

* SVG 是一种使用 XML 描述 2D 图形的语言。
* SVG 基于 XML，这意味着 SVG DOM 中的每个元素都是可用的。您可以为某个元素附加 JavaScript事件处理器。
* 在 SVG 中，每个被绘制的图形均被视为对象。如果 SVG 对象的属性发生变化，那么浏览器能够自动重现图形。
* 特点：
    * 不依赖分辨率
    * 支持事件处理器
    * 最适合带有大型渲染区域的应用程序（比如谷歌地图）
    * 复杂度高会减慢渲染速度（任何过度使用 DOM 的应用都不快）
    * 不适合游戏应用

###Canvas

* Canvas 通过 JavaScript 来绘制 2D 图形。
* Canvas 是逐像素进行渲染的。
* 在 canvas 中，一旦图形被绘制完成，它就不会继续得到浏览器的关注。如果其位置发生变化，那么整个场景也需要重新绘制，包括任何或许已被图形覆盖的对象。
* 特点：
    * 依赖分辨率
    * 不支持事件处理器
    * 弱的文本渲染能力
    * 能够以 .png 或 .jpg 格式保存结果图像
    * 最适合图像密集型的游戏，其中的许多对象会被频繁重绘

SVG 的主要竞争者是 Flash。
与 Flash 相比，SVG 最大的优势是与其他标准（比如 XSL 和 DOM）相兼容。而 Flash 则是未开源的私有技术。

##SVG 实例

```
<?xml version="1.0" standalone="no"?>

<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" 
"http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">

<svg width="100%" height="100%" version="1.1"
xmlns="http://www.w3.org/2000/svg">

<circle cx="100" cy="50" r="40" stroke="black"
stroke-width="2" fill="red"/>
</svg>
```
######代码解释：

第一行包含了 XML 声明。请注意 standalone 属性！该属性规定此 SVG 文件是否是“独立的”，或含有对外部文件的引用。
standalone="no" 意味着 SVG 文档会引用一个外部文件 - 在这里，是 DTD 文件。     

第二和第三行引用了这个外部的 SVG DTD。该 DTD 位于 <http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd/>。 该 DTD 位于 W3C，含有所有允许的 SVG 元素。      

SVG 代码以 `<svg>` 元素开始，包括开启标签 <svg> 和关闭标签 `</svg>` 。这是根元素。width 和 height 属性可设置此 SVG 文档的宽度和高度。version 属性可定义所使用的 SVG 版本，xmlns 属性可定义 SVG 命名空间。   

SVG 的 `<circle>` 用来创建一个圆。cx 和 cy 属性定义圆中心的 x 和 y 坐标。如果忽略这两个属性，那么圆点会被设置为 (0, 0)。r 属性定义圆的半径。    

stroke 和 stroke-width 属性控制如何显示形状的轮廓。我们把圆的轮廓设置为 2px 宽，黑边框。

fill 属性设置形状内的颜色。我们把填充颜色设置为红色。

关闭标签的作用是关闭 SVG 元素和文档本身。


    
## HTML 页面中的 SVG

SVG 文件可通过以下标签嵌入 HTML 文档：`<embed>`、`<object>` 或者 `<iframe>`。

### 使用 `<embed>` 标签

`<embed>` 标签被所有主流的浏览器支持，并允许使用脚本。

当在 HTML 页面中嵌入 SVG 时使用 `<embed>` 标签是 Adobe SVG Viewer 推荐的方法！然而，如果需要创建合法的 XHTML，就不能使用 `<embed>`。任何 HTML 规范中都没有 `<embed>` 标签。

#####语法：

```
<embed src="rect.svg" width="300" height="100" 
type="image/svg+xml" pluginspage="http://www.adobe.com/svg/viewer/install/" />
```
pluginspage 属性指向下载插件的 URL。


### 使用 `<object>` 标签

`<object>` 标签是 HTML 4 的标准标签，被所有较新的浏览器支持。它的缺点是不允许使用脚本。

假如您安装了最新版本的 Adobe SVG Viewer，那么当使用 `<object>` 标签时 SVG 文件无法工作（至少不能在 IE 中工作）！

#####语法：
```
<object data="rect.svg" width="300" height="100" 
type="image/svg+xml" codebase="http://www.adobe.com/svg/viewer/install/" />
```
codebase 属性指向下载插件的 URL。

###使用 `<iframe>` 标签

`<iframe>` 标签可工作在大部分的浏览器中。

#####语法：

```
<iframe src="rect.svg" width="300" height="100">
</iframe>
```

##SVG 形状
SVG 有一些预定义的形状元素，可被开发者使用和操作：

* 矩形 <rect>
* 圆形 <circle>
* 椭圆 <ellipse>
* 线 <line>
* 折线 <polyline>
* 多边形 <polygon>
* 路径 <path>

###`<rect>` 标签
`<rect>` 标签可用来创建矩形，以及矩形的变种。
```
<rect x="200" y="200" width="300" height="300" rx="20" ry="20" 
        style="fill:red; stroke-width:5;stroke:black;
        fill-opacity:0.1;stroke-opacity:0.9;opacity:0.9"/>
```
![](http://7sbohv.com1.z0.glb.clouddn.com/rect.png)

[查看源代码](http://codepen.io/xiaozhuzhu77/pen/PPqmar)

代码解释：
* x 属性定义矩形的左侧位置（例如，x="0" 定义矩形到浏览器窗口左侧的距离是 0px）
* y 属性定义矩形的顶端位置（例如，y="0" 定义矩形到浏览器窗口顶端的距离是 0px）
* rect 元素的 width 和 height 属性可定义矩形的高度和宽度
* rx 和 ry 属性可使矩形产生圆角
* style 属性用来定义 CSS 属性
* CSS 的 fill 属性定义矩形的填充颜色（rgb 值、颜色名或者十六进制值）
* CSS 的 stroke-width 属性定义矩形边框的宽度
* CSS 的 stroke 属性定义矩形边框的颜色
* CSS 的 fill-opacity 属性定义填充颜色透明度（合法的范围是：0 - 1）
* CSS 的 stroke-opacity 属性定义笔触颜色的透明度（合法的范围是：0 - 1）
* CSS 的 opacity 属性定义整个元素的透明值（合法的范围是：0 - 1）

### `<circle>` 标签
`<circle>` 标签可用来创建一个圆
```
<svg width="100%" height="100%">

    <circle cx="300" cy="60" r="50" stroke="#ff0" stroke-width="3" fill="red" >
    </circle>
    
</svg>
```
![](http://7sbohv.com1.z0.glb.clouddn.com/circle.png)

[查看源代码](http://codepen.io/xiaozhuzhu77/pen/gapWvy)

代码解释：

cx 和 cy 属性定义圆点的 x 和 y 坐标。如果省略 cx 和 cy，圆的中心会被设置为 (0, 0)
r 属性定义圆的半径。

###`<ellipse>` 标签
`<ellipse>` 标签可用来创建椭圆。椭圆与圆很相似。不同之处在于椭圆有不同的 x 和 y 半径，而圆的 x 和 y 半径是相同的。
```
 <svg width="100%" height="100%" >

        <ellipse cx="300" cy="150" rx="200" ry="80" style="fill:rgb(200,100,50);
                 stroke:rgb(0,0,100);stroke-width:2">
        </ellipse>

</svg>
```
![](http://7sbohv.com1.z0.glb.clouddn.com/ellipse.png)

[查看源代码](http://codepen.io/xiaozhuzhu77/pen/MawoWv)

代码解释：

* cx 属性定义圆点的 x 坐标
* cy 属性定义圆点的 y 坐标
* rx 属性定义水平半径
* ry 属性定义垂直半径

###`<line>` 标签
`<line>` 标签用来创建线条。

```
<svg width="100%" height="100%">

    <line x1="0" y1="0" x2="300" y2="300" style="stroke:rgb(99,99,99);
            stroke-width:2"/>
            
</svg>
```
[查看源代码](http://codepen.io/xiaozhuzhu77/pen/JYdJom)

代码解释：

* x1 属性在 x 轴定义线条的开始
* y1 属性在 y 轴定义线条的开始
* x2 属性在 x 轴定义线条的结束
* y2 属性在 y 轴定义线条的结束



###`<polygon>` 标签
`<polygon>` 标签用来创建含有不少于三个边的图形（即，多边形）。
#### 三角形
```
<svg width="100%" height="100%">

    <polygon points="220,100 300,210 170,250"
             style="fill:#cccccc;stroke:red;stroke-width:2; opacity: 0.5;">

    </polygon>

</svg>
```
![](http://7sbohv.com1.z0.glb.clouddn.com/triangle.png)

[查看源代码](http://codepen.io/xiaozhuzhu77/pen/MawoaO)

points 属性定义多边形每个角的 x 和 y 坐标


####多边形
```
<div class="wrap">
    <div class="clip-block">
        <div class="clip-each clip-solid">
            <div class="social-share-block">
            </div>
        </div>
    </div>
    <!-- /clip-block -->

    <svg class="clip-svg">
    
        <defs>
            <clipPath id="hexagon-clip" clipPathUnits="objectBoundingBox">
                <polygon points="0.25 0.05, 0.75 0.05, 1 0.5, 0.75 0.95,
                        0.25 0.95, 0 0.5" />
            </clipPath>
        </defs>
        
    </svg>
    
    
    <svg class="clip-svg">
    
        <defs>
            <clipPath id="triangle-clip" clipPathUnits="objectBoundingBox">
                <polygon points="1 0.03, 0.17 1, 1 1" />
            </clipPath>
        </defs>
        
    </svg>
</div>
```
![](http://7sbohv.com1.z0.glb.clouddn.com/polygon.png)

[查看源代码](http://codepen.io/xiaozhuzhu77/pen/zvGzZJ)

###`<polyline>` 标签
`<polyline>` 标签用来创建仅包含直线的形状。

```
<svg width="100%" height="100%">

    <polyline points="0,0 0,20 20,20 20,40 40,40 40,60" 
            style="fill:white;stroke:red;stroke-width:2">
    </polyline>

</svg>
```
[查看效果](http://codepen.io/xiaozhuzhu77/pen/wKaqap)

###`<path>` 标签
`<path>` 标签用来定义路径。

下面的命令可用于路径数据：
* M = moveto 起始位置
* L = lineto  直线
* H = horizontal lineto 横向画线
* V = vertical lineto 纵向画线
* C = curveto 曲线
* S = smooth curveto 平滑曲线
* Q = quadratic Belzier curve 二次贝塞尔曲线
* T = smooth quadratic Belzier curveto  平滑二次贝塞尔曲线
* A = elliptical Arc 椭圆弧
* Z = closepath 关闭路径

#####注释：
以上所有命令均允许小写字母。大写表示绝对定位，小写表示相对定位。

```
<svg width="100%" height="100%">

    <path d="M153 334
            C153 334 151 334 151 334
            C151 339 153 344 156 344
            C164 344 171 339 171 334
            C171 322 164 314 156 314
            C142 314 131 322 131 334
            C131 350 142 364 156 364
            C175 364 191 350 191 334
            C191 311 175 294 156 294
            C131 294 111 311 111 334
            C111 361 131 384 156 384
            C186 384 211 361 211 334
            C211 300 186 274 156 274"
          style="fill:white;stroke:red;stroke-width:2">

    </path>

</svg>
```
![](http://7sbohv.com1.z0.glb.clouddn.com/path.png)

[查看源代码](http://codepen.io/xiaozhuzhu77/pen/BoNdpY)

## SVG 滤镜
在 SVG 中，必须在 `<defs>` 标签中定义 SVG 滤镜，可用的滤镜有：

* feBlend
* feColorMatrix
* feComponentTransfer
* feComposite
* feConvolveMatrix
* feDiffuseLighting
* feDisplacementMap
* feFlood
* feGaussianBlur
* feImage
* feMerge
* feMorphology
* feOffset
* feSpecularLighting
* feTile
* feTurbulence
* feDistantLight
* fePointLight
* feSpotLight

### feBlend
```
<svg width="100%" height="100%">

    <defs> 
        <linearGradient id="MyGradient" gradientUnits="userSpaceOnUse"
                x1="100" y1="0" x2="300" y2="0"> 
            <stop offset="0" style="stop-color:#000000"/> 
            <stop offset=".67" style="stop-color:#ffff00"/> 
            <stop offset="1" style="stop-color:#000000"/> 
        </linearGradient> 
        <filter id="normal"> 
            <feBlend mode="normal" in2="BackgroundImage"/> 
        </filter> 
        <filter id="multiply"> 
            <feBlend mode="multiply" in2="BackgroundImage"/> 
        </filter> 
        <filter id="screen"> 
            <feBlend mode="screen" in2="BackgroundImage"/> 
        </filter> 
        <filter id="darken"> 
            <feBlend mode="darken" in2="BackgroundImage"/> 
        </filter> 
        <filter id="lighten"> 
            <feBlend mode="lighten" in2="BackgroundImage"/> 
        </filter> 
    </defs> 
    
    <g style="enable-background: new"> 
        <rect x="40" y="20" width="300" height="450" 
                style="fill:url(#MyGradient)"/> 
        <g style="font-size:75;fill:#888888;fill-opacity:.6"> 
            <text x="50" y="90" style="filter:url(#normal)">Normal</text> 
            <text x="50" y="180" style="filter:url(#multiply)">Multiply</text> 
            <text x="50" y="270" style="filter:url(#screen)">Screen</text> 
            <text x="50" y="360" style="filter:url(#darken)">Darken</text> 
            <text x="50" y="450" style="filter:url(#lighten)">Lighten</text> 
        </g> 
    </g>

</svg>
```
[](http://7sbohv.com1.z0.glb.clouddn.com/feblend.png)

[查看效果](http://codepen.io/xiaozhuzhu77/pen/Xmbeoz)

###feColorMatrix
```
<svg width="100%" height="100%">

    <defs> 
        <linearGradient id="MyGrad" gradientUnits="userSpaceOnUse" x1="100" y1="0" x2="500" y2="0"> 
            <stop offset="0" style="stop-color:#ff00ff"/> 
            <stop offset=".33" style="stop-color:#88ff88"/> 
            <stop offset=".67" style="stop-color:#2020ff"/> 
            <stop offset="1" style="stop-color:#d00000"/> 
        </linearGradient> 
        <filter id="Matrix"> 
            <feColorMatrix type="matrix" values="1 0 0 0 0  0 1 0 0 0  0 0 1 0 0  0 0 0 1 0"/> 
        </filter> 
        <filter id="Saturate"> 
            <feColorMatrix type="saturate" values="0.4"/> 
        </filter> 
        <filter id="HueRotate"> 
            <feColorMatrix type="hueRotate" values="90"/> 
        </filter> 
        <filter id="Luminance"> 
            <feColorMatrix type="luminanceToAlpha" result="a"/> 
            <feComposite in="SourceGraphic" in2="a" operator="in"/> 
        </filter> 
    </defs> 
    
    <g style="font-size:50;fill:url(#MyGrad)">
        <text x="50" y="60">Unfiltered</text> 
        <text x="50" y="120" style="filter:url(#Matrix)">Matrix</text> 
        <text x="50" y="180" style="filter:url(#Saturate)">Saturate</text> 
        <text x="50" y="240" style="filter:url(#HueRotate)">HueRotate</text> 
        <text x="50" y="300" style="filter:url(#Luminance)">Luminance</text> 
    </g> 
</svg>
```
[](http://7sbohv.com1.z0.glb.clouddn.com/fecolormatrix.png)

[查看效果](http://codepen.io/xiaozhuzhu77/pen/KdpXJN)

###feComponentTransfer
```
<svg width="100%" height="100%">

    <defs>
        <linearGradient id="MyGrad" gradientUnits="userSpaceOnUse" x1="50" y1="0" x2="600" y2="0">
            <stop offset="0" stop-color="#ff0000" />
            <stop offset=".33" stop-color="#00ff00" />
            <stop offset=".67" stop-color="#0000ff" />
            <stop offset="1" stop-color="#000000" />
        </linearGradient>
        
        <filter id="Identity">
            <feComponentTransfer>
                    <feFuncR type="identity"/>
                    <feFuncG type="identity"/>
                    <feFuncB type="identity"/>
                    <feFuncA type="identity"/>
              </feComponentTransfer>
        </filter>
        <filter id="Table">
            <feComponentTransfer>
                    <feFuncR type="table" tableValues="0 0 1 1"/>
                    <feFuncG type="table" tableValues="1 1 0 0"/>
                    <feFuncB type="table" tableValues="0 1 1 0"/>
                </feComponentTransfer>
        </filter>
        <filter id="Linear">
            <feComponentTransfer>
                    <feFuncR type="linear" slope=".5" intercept=".25"/>
                    <feFuncG type="linear" slope=".5" intercept="0"/>
                    <feFuncB type="linear" slope=".5" intercept=".5"/>
            </feComponentTransfer>
        </filter>
        <filter id="Gamma">
            <feComponentTransfer>
                    <feFuncR type="gamma" amplitude="2" exponent="5" offset="0"/>
                    <feFuncG type="gamma" amplitude="2" exponent="3" offset="0"/>
                    <feFuncB type="gamma" amplitude="2" exponent="1" offset="0"/>
            </feComponentTransfer>
        </filter>
    </defs>
    
    <g font-size="50" font-weight="bold" fill="url(#MyGrad)">
        <text x="50" y="60" filter="url(#Identity)">Identity</text>
        <text x="50" y="120" filter="url(#Table)">TableLookup</text>
        <text x="50" y="180" filter="url(#Linear)">LinearFunc</text>
        <text x="50" y="240" filter="url(#Gamma)">GammaFunc</text>
    </g>
</svg>
```
[](http://7sbohv.com1.z0.glb.clouddn.com/fecomponenttransfer.png)

[查看效果](http://codepen.io/xiaozhuzhu77/pen/qOdPgy)


###feOffset
```
<svg width="100%" height="100%">

    <defs>
        <filter id="filter" x="0" y="0">
            <feGaussianBlur stdDeviation="5"/>
            <feOffset dx="5" dy="5"/>
        </filter>
    </defs>
    
    <rect width="90" height="90" fill="grey" filter="url(#filter)"/>
    <rect width="90" height="90" fill="yellow" stroke="black"/>

</svg>

```


###高斯滤镜（Gaussian Blur）
`<filter>` 标签用来定义 SVG 滤镜。<filter> 标签使用必需的 id 属性来定义向图形应用哪个滤镜？
`<filter>` 标签必须嵌套在 `<defs>` 标签内。`<defs>` 标签是 definitions 的缩写，它允许对诸如滤镜等特殊元素进行定义。

```
<svg width="100%" height="100%">

    <defs>
        <filter id="Gaussian_Blur">
            <feGaussianBlur in="SourceGraphic" stdDeviation="3" >
            </feGaussianBlur>
        </filter>
    </defs>

    <ellipse cx="200" cy="150" rx="70" ry="40" style="fill:#ff0000;
    stroke:#000000; stroke-width:2; filter:url(#Gaussian_Blur)">
    </ellipse>
    
</svg>
```
![](http://7sbohv.com1.z0.glb.clouddn.com/filter1.png)

[查看源代码](http://codepen.io/xiaozhuzhu77/pen/GpJvzd)

####代码解释：
* `<filter>` 标签的 id 属性可为滤镜定义一个唯一的名称（同一滤镜可被文档中的多个元素使用）
* filter:url 属性用来把元素链接到滤镜。当链接滤镜 id 时，必须使用 # 字符
* 滤镜效果是通过 `<feGaussianBlur>` 标签进行定义的。fe 后缀可用于所有的滤镜
* `<feGaussianBlur>` 标签的 stdDeviation 属性可定义模糊的程度
* in="SourceGraphic" 这个部分定义了由整个图像创建效果

另一个 stdDeviation 值不同的例子:

```
<svg width="100%" height="100%">

    <defs>
        <filter id="Gaussian_Blur">
            <feGaussianBlur in="SourceGraphic" stdDeviation="20">
            </feGaussianBlur>
        </filter>
    </defs>

    <ellipse cx="200" cy="150" rx="70" ry="40"style="fill:#ff0000;
            stroke:#000000; stroke-width:2; filter:url(#Gaussian_Blur)">
    </ellipse>

</svg>
```
![](http://7sbohv.com1.z0.glb.clouddn.com/filter2.png)


[查看源代码](http://codepen.io/xiaozhuzhu77/pen/gapxJj)

###feMerge
```
<svg width="100%" height="100%">

    <defs>
        <filter id="test" filterUnits="objectBoundingBox" x="0" y="0" width="1.5"
                height="4">
        
            <feOffset result="Off1" dx="15" dy="20"/>
            <feFlood style="flood-color:#ff0000;flood-opacity:0.8"/>
            <feComposite in2="Off1" operator="in" result="C1"/>
        
            <feOffset in="SourceGraphic" result="Off2" dx="30" dy="40"/>
            <feFlood style="flood-color:#ff0000;flood-opacity:0.4"/>
            <feComposite in2="Off2" operator="in" result="C2"/>
        
            <feMerge>
                <feMergeNode in="C2"/>
                <feMergeNode in="C1"/>
                <feMergeNode in="SourceGraphic"/>
            </feMerge>
        </filter>
    </defs>
    
    <text x="30" y="100" style="font:36px verdana bold;fill:blue;
            filter:url(#test)">This is some text!</text>

</svg>
```
[](http://7sbohv.com1.z0.glb.clouddn.com/femerge.png)

[查看效果](http://codepen.io/xiaozhuzhu77/pen/bVdoZV)

###feMorphology
```
<svg width="100%" height="100%">

    <defs>
        <filter id="Erode1">
            <feMorphology operator="erode" in="SourceGraphic" radius="1"/>
        </filter>
        <filter id="Erode3">
            <feMorphology operator="erode" in="SourceGraphic" radius="3"/>
        </filter>
        <filter id="Erode4">
            <feMorphology operator="erode" in="SourceGraphic" radius="4"/>
        </filter>
        <filter id="Dilate1">
            <feMorphology operator="dilate" in="SourceGraphic" radius="1"/>
        </filter>
        <filter id="Dilate3">
            <feMorphology operator="dilate" in="SourceGraphic" radius="3"/>
        </filter>
        <filter id="Dilate4">
            <feMorphology operator="dilate" in="SourceGraphic" radius="4"/>
        </filter>
    </defs>
    
    <g enable-background="new">
        <g font-family="Verdana" font-size="50" stroke="red" stroke-width="4">
            <text x="50" y="60">Unfiltered</text>
            <text x="50" y="120" filter="url(#Erode1)">Erode 1</text>
            <text x="50" y="180" filter="url(#Erode3)">Erode 3</text>
            <text x="50" y="240" filter="url(#Erode4)">Erode 4</text>
            <text x="50" y="300" filter="url(#Dilate1)">Dilate 1</text>
            <text x="50" y="360" filter="url(#Dilate3)">Dilate 3</text>
            <text x="50" y="420" filter="url(#Dilate4)">Dilate 4</text>
        </g>
    </g>

</svg>
```
[](http://7sbohv.com1.z0.glb.clouddn.com/femorphology.png)

[查看效果](http://codepen.io/xiaozhuzhu77/pen/rOVGRG)

##SVG 渐变
渐变是一种从一种颜色到另一种颜色的平滑过渡。另外，可以把多个颜色的过渡应用到同一个元素上。

在 SVG 中，有两种主要的渐变类型：

* 线性渐变
* 放射性渐变

###SVG线性渐变
`<linearGradient>` 可用来定义 SVG 的线性渐变。
`<linearGradient>` 标签必须嵌套在 `<defs>` 的内部。`<defs>` 标签是 definitions 的缩写，它可对诸如渐变之类的特殊元素进行定义。

线性渐变可被定义为水平、垂直或角形的渐变：
* 当 y1 和 y2 相等，而 x1 和 x2 不同时，可创建水平渐变
* 当 x1 和 x2 相等，而 y1 和 y2 不同时，可创建垂直渐变
* 当 x1 和 x2 不同，且 y1 和 y2 不同时，可创建角形渐变

#####水平渐变：

```
<svg width="100%" height="100%">

    <defs>
        <linearGradient id="orange_red" x1="0%" y1="0%" x2="100%" y2="0%">
            <stop offset="0%" style="stop-color:rgb(255,255,0);stop-opacity:1">
            </stop>
            
            <stop offset="100%" style="stop-color:rgb(255,0,0);stop-opacity:1">
            </stop>
        </linearGradient>
    </defs>

    <ellipse cx="200" cy="190" rx="85" ry="55" style="fill:url(#orange_red)">
    </ellipse>
    
</svg>
```
![](http://7sbohv.com1.z0.glb.clouddn.com/lineargradient.png)


[查看源代码](http://codepen.io/xiaozhuzhu77/pen/PPqJoy)

#####垂直渐变：
```
<svg width="100%" height="100%">

    <defs>
        <linearGradient id="orange_red" x1="0%" y1="0%" x2="0%" y2="100%">
            <stop offset="0%" style="stop-color:rgb(255,255,0); stop-opacity:1">
            </stop>
            <stop offset="100%" style="stop-color:rgb(255,0,0); stop-opacity:1">
            </stop>
        </linearGradient>
    </defs>
    
    <ellipse cx="200" cy="190" rx="85" ry="55" style="fill:url(#orange_red)">
    </ellipse>
    
</svg>
```
![](http://7sbohv.com1.z0.glb.clouddn.com/verticalgradient.png)


[查看源代码](http://codepen.io/xiaozhuzhu77/pen/avOLOJ)

###SVG 放射性渐变
`<radialGradient>` 用来定义放射性渐变。
`<radialGradient>` 标签必须嵌套在 `<defs>` 中。`<defs>` 标签是 definitions 的缩写，它允许对诸如渐变等特殊元素进行定义。
```
<svg width="100%" height="100%">

    <defs>
        <radialGradient id="grey_blue" cx="50%" cy="50%" r="50%" fx="50%" fy="50%">
            <stop offset="0%" style="stop-color:rgb(200,200,200);stop-opacity:0">
            </stop>
            <stop offset="100%" style="stop-color:rgb(0,0,255);stop-opacity:1">
            </stop>
        </radialGradient>
    </defs>

    <ellipse cx="230" cy="200" rx="110" ry="100" style="fill:url(#grey_blue)">
    </ellipse>
    
</svg>
```
![](http://7sbohv.com1.z0.glb.clouddn.com/radialGradient.png)

[查看源代码](http://codepen.io/xiaozhuzhu77/pen/JYdrRr)

#####代码解释：

`<radialGradient>` 标签的 id 属性可为渐变定义一个唯一的名称，fill:url(#grey_blue) 属性把 
ellipse 元素链接到此渐变，cx、cy 和 r 属性定义外圈，而 fx 和 fy 定义内圈 渐变的颜色范围可由两种
或多种颜色组成。每种颜色通过一个 `<stop>` 标签来规定。offset 属性用来定义渐变的开始和结束位置。

####另外一个例子：
```
<svg width="100%" height="100%">

    <defs>
        <radialGradient id="grey_blue" cx="20%" cy="40%" r="50%" fx="50%" fy="50%">
            <stop offset="0%" style="stop-color:rgb(200,200,200);stop-opacity:0">
            </stop>
            <stop offset="100%" style="stop-color:rgb(0,0,255);stop-opacity:1">
            </stop>
        </radialGradient>
    </defs>

    <ellipse cx="230" cy="200" rx="110" ry="100"style="fill:url(#grey_blue)">
    </ellipse>
    
</svg>
```
![](http://7sbohv.com1.z0.glb.clouddn.com/radialgradient2.png)

[查看源代码](http://codepen.io/xiaozhuzhu77/pen/qOdPRV)

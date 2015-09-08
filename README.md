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

        <ellipse cx="300" cy="150" rx="200" ry="80"
                 style="fill:rgb(200,100,50);
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
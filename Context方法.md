

### 1.arc

CanvasRenderingContext2D.arc()用来`绘制圆弧`，由于圆本质上就是个封闭圆弧，因此，此方法也可以用来绘制正圆

各个参数含义和作用如下：

`xNumber`
圆弧对应的圆心横坐标

`yNumber`
圆弧对应的圆心纵坐标

`radiusNumber`
圆弧的半径大小

`startAngleNumber`
圆弧开始的角度，单位是弧度

`endAngleNumber`
圆弧结束的角度，单位是弧度

`anticlockwise（可选）`Boolean
弧度的开始到结束的绘制是按照顺时针来算，还是按时逆时针来算。如何设置为true，则表示按照逆时针方向从startAngle绘制到endAngle



arc这个方法用于绘制圆弧，弧度的大小取决于开始、结束的角度值，如果开始角度为0，此事`Math.PI`就代表半圆弧度，这个时候我们如果要绘制一个圆的话

```javascript
// 绘制完整圆
context.beginPath();
context.arc(150, 75, 50, 0, Math.PI * 2);
context.stroke();
```



### 2.arcTo

CanvasRenderingContext2D.arcTo()作用是给路径添加圆弧，需要指定控制点和半径，意思就是说在两个点连接的路径上绘制圆弧



各个参数含义和作用如下：

`x1Number`
第1个控制点的横坐标

`y1Number`
第1个控制点的纵坐标

`x2Number`
第2个控制点的横坐标

`y2Number`
第2个控制点的纵坐标

`radiusNumber`
圆弧的半径大小



```javascript
context.beginPath();
context.moveTo(50, 50);
context.arcTo(117, 49, 200, 40, 40);
context.lineTo(200, 40);
context.stroke();
```



### 3.beginPath

很简单的一个方法，每调用一次开辟一个新路径，如果开辟新路径却不多调用一次beginPath的话，后续的对于路径的样式设置则无效

```javascript
// 开始路径
context.beginPath();
context.strokeStyle = 'blue';
context.moveTo(60, 20);
context.lineTo(220, 20);
context.stroke();

// 如果这里不调用beginPath，那么蓝色路径最终会统一设置成绿色
// 开始路径 again
context.beginPath();
context.strokeStyle = 'green';
context.moveTo(60, 20);
context.lineTo(160, 120);
context.stroke();
```

因此，只要是非连续路径绘制，都要记得都要执行一句context.beginPath()。



### 4.bezierCurveTo
用于绘制贝塞尔曲线，需要三个控制点，前两个是控制点，第三个是结束点，但是绘制贝塞尔曲线还需要一个起始点，贝塞尔曲线的起始点就是当前路径的最后一个控制点，也可以先moveTo设置一个开始点

各个参数含义和作用如下：

`cp1xNumber`
第1个控制点的横坐标

`cp1yNumber`
第1个控制点的纵坐标

`cp2xNumber`
第2个控制点的横坐标

`cp2yNumber`
第2个控制点的纵坐标

`xNumber`
结束点的横坐标

`yNumber`
结束点的纵坐标



```javascript
context.beginPath();
context.moveTo(50, 50);
context.bezierCurveTo(100, 100, 171, 21, 250, 100);
context.stroke();
```



### 5.stroke
对**路径**进行**描边**或者说绘制，在canvas中设置了路径以及路径样式以后，必须得调用stroke方法，不然就相当于空设置样式，没有图案。这里的路径不是说是直线，可能是曲线，圆弧都是属于路径的范畴

画一条直线

```javascript
context.moveTo(50, 50);
context.lineTo(250, 100);
context.stroke();
```



### 6.clearRect
用于将Canvas画布中一块矩形区域擦除或者说变成透明的

`xNumber`
矩形左上角x坐标

`yNumber`
矩形左上角y坐标

`widthNumber`
被清除的矩形区域的高度

`heightNumber`
被清除的矩形区域的宽度度



```javascript
context.clearRect(x, y, width, height);
```



### 7.clip

表示路径裁剪，使用前**要先绘制裁剪路径**，然后执行clip得到裁剪的区域，再进行其他的绘制，将内容绘制到裁剪出来的区域

各个参数含义和作用如下：

`fillRuleString`
填充规则。用来确定一个点实在路径内还是路径外。可选值包括：

nonzero：非零规则。此乃默认规则

evenodd：奇偶规则

关于'nonzero'和'evenodd'规则可参见[文章](https://www.zhangxinxu.com/wordpress/2018/10/nonzero-evenodd-fill-mode-rule/)

`pathObject`
指Path2D对象

```javascript
var context = canvas.getContext('2d');
// 需要图片先加载完毕
var img = new Image();
img.onload = function () {
    // 剪裁路径是三角形
    context.beginPath();
    context.moveTo(20, 20);
    context.lineTo(200, 80);
    context.lineTo(110, 150);
    // 剪裁
    context.clip();
    // 填充图片
    context.drawImage(img, 0, 0, 250, 167);
};
img.src = '1.jpg';

// 以上先是画了一个三角形，然后将图片填充到裁剪的区域
```



### 8.closePath()

闭合路径，会吧路径的最后的位置与开始位置直线相连，形成闭合区域，比如画三角形，如果不调用closePath，那么就要调用三次lineTo

```javascript
// 绘制三角
context.beginPath();
context.moveTo(10, 10);
context.lineTo(140, 70);
context.lineTo(70, 140);
// 不执行闭合，直接描边
context.stroke();

// 绘制另外一个三角
context.beginPath();
context.moveTo(160, 10);
context.lineTo(290, 70);
context.lineTo(220, 140);
// 执行闭合，然后描边
context.closePath();
context.stroke();
```



### 9.createImageData
创建一个全新的空的ImageData对象，该对象中的所有像素信息都是透明黑，通常会和putImageData搭配使用



语法：

```javascript
context.createImageData(width, height); 
context.createImageData(imagedata);
```



`widthNumber`

ImageData对象包含的width值。如果ImageData对象转换成图像，则此width也是最终图像呈现的宽度

`heightNumber`

ImageData对象包含的height值。如果ImageData对象转换成图像，则此height也是最终图像呈现的高度

`imagedataObject`

一个存在的ImageData对象，只会使用该ImageData对象中的width和height值，包含的像素信息会全部转换为透明黑



### 10.putImageData
将给定ImageData对象的数据绘制到位图上，意思是将ImageData对象填充到某个context对象上面，ImageData可以是getImageData获取的，也可以是createImageData创建的

```javascript
context.putImageData(imagedata, dx, dy);
context.putImageData(imagedata, dx, dy, dirtyX, dirtyY, dirtyWidth, dirtyHeight);
```



`imagedataObject`
包含图像像素信息的ImageData对象

`dxNumber`
目标Canvas中被图像数据替换的起点横坐标

`dyNumber`
目标Canvas中被图像数据替换的起点纵坐标

`dirtyX（可选）Number`
图像数据渲染区域的左上角横坐标，默认值是0

`dirtyY（可选）Number`
图像数据渲染区域的左上角纵坐标，默认值是0

`dirtyWidth（可选）Number`
图像数据渲染区域的宽度，默认值是imagedata图像的宽度

`dirtyHeight（可选）Number`
图像数据渲染区域的高度，默认值是imagedata图像的高度



### 11.getImageData

顾名思义，获取一个图片对象

```javascript
context.getImageData(sx, sy, sWidth, sHeight);
```

`sxNumber`
需要返回的图像数据区域的起始横坐标

`syNumber`
需要返回的图像数据区域的起始纵坐标

`sWidthNumber`
需要返回的图像数据区域的宽度

`sHeightNumber`
需要返回的图像数据区域的高度



### 12.drawImage
将图片资源画到context对象上

```javascript
context.drawImage(image, dx, dy);
context.drawImage(image, dx, dy, dWidth, dHeight);
context.drawImage(image, sx, sy, sWidth, sHeight, dx, dy, dWidth, dHeight);
```



`imageObject`
绘制在Canvas上的元素，可以是各类Canvas图片资源（见CanvasImageSource），如<img>图片，SVG图像，Canvas元素本身等

`dxNumber`
在Canvas画布上规划一片区域用来放置图片，dx就是这片区域的左上角横坐标

`dyNumber`
在Canvas画布上规划一片区域用来放置图片，dy就是这片区域的左上角纵坐标

`dWidthNumber`
在Canvas画布上规划一片区域用来放置图片，dWidth就是这片区域的宽度

`dHeightNumber`
在Canvas画布上规划一片区域用来放置图片，dHeight就是这片区域的高度

`sxNumber`
表示图片元素绘制在Canvas画布上起始横坐标

`syNumber`
表示图片元素绘制在Canvas画布上起始纵坐标

`sWidthNumber`
表示图片元素从坐标点开始算，多大的宽度内容绘制Canvas画布上

`sHeightNumber`
表示图片元素从坐标点开始算，多大的高度内容绘制Canvas画布上



使用的时候需要注意的地方是三种使用方式，最后一种的参数顺序不一致，另外实际使用的时候，如果原图的尺寸超过画布的尺寸，那还需要考虑下图片缩放的问题



### 13.createLinearGradient

创建线性渐变对象，各个参数含义和作用如下：

`x0Number`
渐变起始点横坐标

`y0Number`
渐变起始点纵坐标

`x1Number`
渐变结束点横坐标。

`y1Number`
渐变结束点纵坐标



创建的渐变对象是针对整个传递的坐标区域的，创建渐变对象一般与addColorStop配合使用

addColorStop规定 gradient 对象中的颜色和位置，参数

`stop`

 介于 0.0 与 1.0 之间的值，表示渐变中开始与结束之间的位置

`color`

在结束位置显示的 CSS 颜色值



```javascript
var context = canvas.getContext('2d');
// 创建渐变
var gradient = context.createLinearGradient(0, 0, 300, 0);
gradient.addColorStop(0, 'red');
gradient.addColorStop(1, 'green');
// 设置填充样式为渐变
context.fillStyle = gradient;
// 左上角和右下角分别填充2个矩形
context.fillRect(10, 10, 160, 60);
context.fillRect(120, 80, 160, 60);
```



### 14.createPattern

指定图案对象的平铺方式

各个参数含义和作用如下：

`imageObject`
用来平铺的CanvasImageSource图像。可以是下面的类型：

HTMLImageElement，也就是<img>元素。

HTMLVideoElement，也就是<video>元素，例如捕获摄像头视频产生的图像信息。

HTMLCanvasElement

CanvasRenderingContext2D

ImageBitmap

ImageData

Blob



`repetitionString`
图案的平铺方式，可以是下面的值：

'repeat'，水平和垂直平铺。当repetition属性值为空字符串''或者null，也会按照'repeat'进行渲染

'repeat-x'，仅水平平铺

'repeat-y'，仅垂直平铺

'no-repeat'，不平铺



使用案例

```javascript
// 先绘制图片
var img = new Image();
img.onload = function () {
    // 我们创建一个Canvas元素
    var canvasCreated = document.createElement('canvas');
    canvasCreated.width = 50;
    canvasCreated.height = 34;
    canvasCreated.getContext('2d').drawImage(this, 0, 0, 50, 34);
    // 页面上需要呈现最终纹理的Canvas上下文
    var context = canvas.getContext('2d');
    // 创建纹理并填充，顺便测试null是否渲染为'repeat'
    var pattern = context.createPattern(canvasCreated, null);
    context.fillStyle = pattern;
    context.fillRect(0, 0, 250, 167);
};
img.src = './1.jpg';
```



### 15.createRadialGradient

创建径向渐变

```javascript
context.createRadialGradient(x0, y0, r0, x1, y1, r1);
```

`x0Number`
起始圆的横坐标

`y0Number`
起始圆的纵坐标

`r0Number`
起始圆的半径

`x1Number`
结束圆的横坐标

`y1Number`
结束圆的纵坐标

`r1Number`
结束圆的半径



通常来讲，会将起始圆半径设置为0，化作一个点，这样设置成一个类似于圆环的渐变效果

```javascript
<canvas width="240" height="120"></canvas>


var context = canvas.getContext('2d');
// 创建一个起始圆半径为0的径向渐变对象
var gradient = context.createRadialGradient(120, 60, 0, 120, 60, 60);
// 设置起止颜色
gradient.addColorStop(0, 'red');
gradient.addColorStop(1, 'green');
// 矩形填充
context.fillStyle = gradient;
context.fillRect(0, 0, 240, 120);
```





### 16.ellipse
用于绘制椭圆



`xNumber`
椭圆弧对应的圆心横坐标

`yNumber`
椭圆弧对应的圆心纵坐标

`radiusXNumber`
椭圆弧的长轴半径大小

`radiusYNumber`
椭圆弧的短轴半径大小

`rotationNumber`
椭圆弧的旋转角度，单位是弧度

`startAngleNumber`
圆弧开始的角度，角度从横轴开始算，单位是弧度

`endAngleNumber`
圆弧结束的角度，单位是弧度

`anticlockwise（可选）Boolean`
弧度的开始到结束的绘制是按照顺时针来算，还是按时逆时针来算。如何设置为true，则表示按照逆时针方向从startAngle绘制到endAngle



绘制一个长轴短轴比2:1，同时旋转45°的椭圆：

```javascript
// 绘制椭圆
context.ellipse(150, 75, 80, 40, Math.PI / 4, 0, 2 * Math.PI);
context.stroke();
```



### 13.fill

 填充方法，我觉得我就是对描述的**路径**所形成的图形进行填充，填充的规则有非零规则，奇偶规则，既然是对描述路径形成的图形，那么在调用前一般会beginPath，描述路径

```javascript
context.fill();
context.fill(fillRule);
context.fill(path, fillRule);
```



`fillRuleString`

填充规则。用来确定一个点实在路径内还是路径外。可选值包括：

nonzero：非零规则，此乃默认规则

evenodd：奇偶规则



`pathObject`

指Path2D对象



### 14.fillRect

填充矩形

```javascript
context.fillRect(x, y, width, height);
```



`xNumber`

填充矩形的起点横坐标

`yNumber`

填充矩形的起点纵坐标

`widthNumber`

填充矩形的宽度

`heightNumber`

填充矩形的高度



### 15.fillText
填充文本

```javascript
context.fillText(text, x, y [, maxWidth])
```



`textString`
用来填充的文本信息

`xNumber`
填充文本的起点横坐标

`yNumber`

填充文本的起点纵坐标

`maxWidth（可选）Number`

最大宽度，超过后，文本会按照一定比例压缩



上述所说超过一定宽度后，文本会压缩，下面是文本换行的方法，其核心原理为，使用context的measureText方法获取每个文本占据的宽度，判断超过宽度后，使用fillText绘制当前行，然后其他内容放在下一个Y坐标渲染

```javascript
CanvasRenderingContext2D.prototype.wrapText = function (text, x, y, maxWidth, lineHeight) {
    if (typeof text != 'string' || typeof x != 'number' || typeof y != 'number') {
        return;
    }
    
    var context = this;
    var canvas = context.canvas;
    
    if (typeof maxWidth == 'undefined') {
        maxWidth = (canvas && canvas.width) || 300;
    }
    if (typeof lineHeight == 'undefined') {
        lineHeight = (canvas && parseInt(window.getComputedStyle(canvas).lineHeight)) || parseInt(window.getComputedStyle(document.body).lineHeight);
    }
    
    // 字符分隔为数组
    var arrText = text.split('');
    var line = '';
    
    for (var n = 0; n < arrText.length; n++) {
        var testLine = line + arrText[n];
        var metrics = context.measureText(testLine);
        var testWidth = metrics.width;
        if (testWidth > maxWidth && n > 0) {
            context.fillText(line, x, y);
            line = arrText[n];
            y += lineHeight;
        } else {
            line = testLine;
        }
    }
    context.fillText(line, x, y);
};
```



### 16.getLineDash

获取虚线的样式

返回一个数组，如果context设置了虚线样式的话，会返回虚线设置的值



### 17.isPointInPath
检测某个点是否在当前路径中。需要注意的是，每调用一次beginPath，检测的路径变成了这次beginPath之后的路径



```javascript
context.isPointInPath(x, y);
context.isPointInPath(x, y, fillRule);

// 下面语法IE不支持
context.isPointInPath(path, x, y);
context.isPointInPath(path, x, y, fillRule);
```



`xNumber`

用来检测的点的横坐标

`yNumber`
用来检测的点的纵坐标

`fillRuleString`

填充规则，用来确定一个点实在路径内还是路径外，可选值包括：

nonzero：非零规则，此乃默认规则
evenodd：奇偶规则

`pathObject`

指Path2D对象



### 18.isPointInStroke
与isPointInPath有点类似，不同的地方在于，他是针对stroke方法描绘出来的路径的

```javascript
context.isPointInStroke(x, y);
context.isPointInStroke(path, x, y);
```



参数
各个参数含义和作用如下：

`xNumber`
用来检测的点的横坐标

`yNumber`
用来检测的点的纵坐标

`pathObject`
指Path2D对象



### 19.lineTo

绘制直线

```javascript
context.lineTo(x, y)
```



`xNumber`

绘制的直线的落点的横坐标

`yNumber`

绘制的直线的落点的纵坐标



### 20.measureText
返回文本的一些信息，包含字符宽度、高度等等。一般来说会先fillText一个文本，然后调用measureText，传入fillText的文本，最后获取相应信息

```javascript
context.measureText(text)
```



### 21.moveTo
移动绘制点到某个坐标，通常是路径绘制的起始点

`xNumber`

落点的横坐标

`yNumber`

落点的纵坐标



```javascript
context.moveTo(x, y)
```



### 22.quadraticCurveTo
绘制二次贝塞尔曲线，相比贝赛尔曲线绘制方法bezierCurveTo()，少了一个控制点。

```javascript
context.quadraticCurveTo(cpx, cpy, x, y)
```



`cpxNumber`
控制点的横坐标

`cpyNumber`

控制点的纵坐标

`xNumber`

结束点的横坐标

`yNumber`

结束点的纵坐标



### 23.rect
和arc、ellipse一样，只是绘制路径，rect绘制的是矩形路径，要进行描边的话，还要调用`stroke`



`xNumber`

矩形路径的起点横坐标

`yNumber`

矩形路径的起点纵坐标

`widthNumber`

矩形的宽度

`heightNumber`

矩形的高度



```javascript
context.rect(100, 25, 100, 100);
context.stroke();
```



### 24.restore
Canvas的绘画状态以堆栈的形式存储，restore则是从堆栈的上方弹出存储的Canvas状态，想像一下数组的pop方法，以此对应的还有`save`保存状态方法，很多时候，为了描绘出连续的动画或者图形，需要多次save当前的状态，下一次再restore上一次的状态，以上一次的基础接着绘画



```javascript
context.restore();
```



### 25.rotate

顺时针旋转整个canvas画布，旋转单位为弧度

弧度计算方式：radian = degree * Math.PI / 180

```javascript
// 旋转45度
context.rotate(45 * Math.PI / 180);
```

默认情况下是基于左上角原点坐标旋转，如果想要修改旋转原点，还需使用translate移动画布的中心点



### 26.translate

`xNumber`

坐标系水平位移的距离

`yNumber`

坐标系垂直位移的距离

```javascript
context.translate(x, y);
```



### 27.save

保存当前Canvas画布状态并放在栈的最上面。这个方法通常与restore配合使用，实际的效果就是保存上一次context绘制的效果以及为画布设置的样式，restore后的绘制又是重新使用默认值或者重新设置属性

```javascript
// 保存初始Canvas状态
context.save();
// 设置红色填充
context.fillStyle = 'red';
// 矩形填充
context.fillRect(20, 20, 100, 60);
// 还原在绘制
context.restore();
// 矩形填充again
context.fillRect(180, 60, 100, 60);
```



以下的状态可被save



当前矩阵变换，transform()

当前剪裁区域，clip()

当前虚线设置，setLineDash()

以及下面这些属性的值：strokeStyle，fillStyle，globalAlpha，lineWidth，lineCap，lineJoin，miterLimit，lineDashOffset，shadowOffsetX，shadowOffsetY，shadowBlur，shadowColor，globalCompositeOperation，font，textAlign，textBaseline



### 28.scale

用来缩放Canvas画布的坐标系，只是影响坐标系，之后的绘制会受此方法影响，但之前已经绘制好的效果不会有任何变化



`xNumber`

Canvas坐标系水平缩放的比例。支持小数，如果值是-1，表示水平翻转

`yNumber`

Canvas坐标系垂直缩放的比例。支持小数，如果值是-1，表示垂直翻转

```javascript
context.scale(x, y)
```



### 29.strokeRect
描边矩形，可以画出一个矩形的路径

```javascript
context.strokeRect(x, y, width, height);
```

`xNumber`

描边矩形的起点横坐标

`yNumber`

描边矩形的起点纵坐标

`widthNumber`

描边矩形的宽度

`heightNumber`

描边矩形的高度



### 30.strokeText

实现文本描边效果

```javascript
context.strokeText(text, x, y [, maxWidth]);
```



`textString`

用来描边的文本信息

`xNumber`

描边文本的起点横坐标

`yNumber`

描边文本的起点纵坐标

`maxWidth（可选）Number`

最大宽度，超出会压缩文本，而非换行



### 31.setLineDash

为描绘的路径或者图形设置虚线样式

```javascript
ctx.setLineDash(segments)
```

`segments`一个数值列表，例如[5, 5]，表示虚线的实线和透明部分长度是5像素和5像素。如果此参数值适合空数组[]，则表示实线，常用来重置虚线设置。



### 32.setTransform




### 33.transform

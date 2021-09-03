### 1.fillStyle

fillStyle可以给Canvas中的各种图形填充样式，它的使用前提是**绘制图形**，然后才能设置填充样式，有三个值可设置

color

使用纯色填充，支持RGB，HSL，RGBA，HSLA以及HEX色值。

```javascript
context.fillStyle = 'RGB(255, 0, 0)';
```

gradient

使用渐变填充，可以是线性渐变或者径向渐变，需要事先创建一个渐变对象

```javascript
// 创建线性渐变对象
var gradientLinear = contextLinear.createLinearGradient(0, 0, 0, 100);
gradientLinear.addColorStop(0, 'red');
gradientLinear.addColorStop(1, 'green');

context.fillStyle = gradientLinear;
```

pattern

使用纹理填充，由于图片也能作为纹理，因此fillStyle也能填充普通的位图



### 2.font

绘制文本内容时设置字号字体，同样也是先绘制文本然后设置字号、字体内容

```javascript
context.font = '24px SimSun, Songti SC';
context.fillText('1', 20, 50);
```



### 3.globalAlpha

用来设置画布的全局透明度，值是0~1

```javascript
context.globalAlpha = value;
```



### 4.globalCompositeOperation

可以用来设置Canvas图形的混合模式，可以衍生很多其他效果，剪裁，例如遮罩，以及改变绘制图形的上下层叠关系，意思就是设置重叠图像的显示模式

```javascript
context.globalCompositeOperation = type;
```

[它的值以及用法](https://www.canvasapi.cn/CanvasRenderingContext2D/globalCompositeOperation)



### 5.lineCap
画一条线条，lineCap标识线条端点的样式

butt

默认值，线的端点就像是个断头台，例如一条横线，终点x坐标是100，则这条线的最右侧边缘就是100这个位置，没有超出

round

线的端点多出一个圆弧

square

线的端点多出一个方框，框框的宽度和线一样宽，高度是线厚度的一半



### 6.lineDashOffset
用来指定**虚线绘制**的偏移距离

lineDashOffset偏移的是虚线绘制的起点，如果值是10，表示虚线起点是10像素的位置，视觉表现上则是虚线缩进了10像素，这个和CSS中的tex-indent缩进正负表现正好相反的。

```javascript
context.clearRect(0,0, canvas.width, canvas.height);
context.setLineDash([8, 4]);
// 设置虚线边框的偏移距离
context.lineDashOffset = 10;
context.strokeRect(2, 2, 236, 116);
```



### 7.lineJoin

此属性用来表示线条转角的样式，支持的属性值为`miter`、`round`、`bevel`，默认为`miter`

```javascript
// 默认值，转角是尖头。如果折线角度比较小，则尖头会非常长，因此需要miterLimit进行限制。
context.lineJoin = 'miter';
// 转角是圆头。
context.lineJoin = 'round';
// 转角是平头
context.lineJoin = 'bevel';
```



### 8.lineWidth

表示绘制图形的线宽，数值类型，默认值是1.0，如果是负数，0，NaN，或者Infinity都会忽略。



### 9.miterLimit
表示的是当lineJoin类型是miter时候，miter效果生效的限制值。[其用法](https://www.canvasapi.cn/CanvasRenderingContext2D/miterLimit)



### 10.shadowBlur

shadowBlur可以用来指定阴影的模糊程度，默认值是0，表示不模糊，值为数值类型，可以为小数，如果是负数，NaN，或者Infinity都会忽略。

绘制一个矩形，然后给个投影，加点模糊

```javascript
// 设置阴影红色，同时模糊大小为10
context.shadowColor = 'red';
context.shadowBlur = 10;

// 填充一个颜色
context.fillStyle = '#f0f3f9';
context.fillRect(40, 40, 160, 40);
```



### 11.shadowColor

指定阴影的颜色，默认值是透明黑，也就是看不到颜色，因此，如果我们想要使用阴影效果，shadowColor是必须要指定的，它的值可以为颜色的字符串也可以为一个rgb字符串

```javascript
context.shadowColor = 'rgb(50, 50, 50)';
```



### 12.shadowOffsetX && shadowOffsetY

设置阴影的垂直水平偏移大小，默认值是0，忽略Infinity或者NaN值。



### 13.strokeStyle
用来设置描边的样式，可以对路径描边，也可以对形状描边，也可以对文字描边

color
描边设置为颜色。
gradient
描边设置为渐变。
pattern
描边设置为图案。

```javascript
context.strokeStyle = color;
context.strokeStyle = gradient;
context.strokeStyle = pattern;
```



### 14.textAlign

绘制文本的时候，设置文本的对齐方式，有以下几个值



left

文本左对齐。也就是最终绘制的文本内容最左侧位置就是设定的x坐标值

right

文本右对齐。也就是最终绘制的文本内容最右侧位置就是设定的x坐标值

center

文本居中对齐。也就是最终绘制的文本内容的水平中心位置就是设定的x坐标值

start

文本起始方位对齐。如果文本是从左往右排列的，则表示左对齐；如果文本是从右往左排列的（例如设置context.direction为rtl），则表示右对齐

end

文本结束方位对齐。如果文本是从左往右排列的，则表示右对齐；如果文本是从右往左排列的（例如设置context.direction为rtl），则表示左对齐

```javascript
context.textAlign = value;
```



### 15.textBaseline

绘制文本时，可以指定文本对齐的基线，有以下几个值

top

设定的垂直y坐标作为文本em区域（em区域可以看成中文字符占据的区域）的顶部

hanging

hanging主要在藏文和其他印度文字中使用，我们了解即可

middle

设定的垂直y坐标作为文本em区域的垂直中心位置

alphabetic

默认值。表示的是正常文本的基线，可以看成是字母x的下边缘。也就是设定的垂直y坐标就是字母x的下边缘

ideographic

ideographic主要在汉语、日语和韩语中使用。字面直译是表意基线。含义为：如果字符的主体突出在字母基线之下，则这是字符主体的底部。例如汉字“中”比字母x位置更低，因此，底部是汉字主体的底部

bottom

设定的垂直y坐标作为文本em区域的底部

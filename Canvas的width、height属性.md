### width、height

width、height属性用来控制Canvas画布绘制区域的宽高度



#### 语法

下面代码中的canvas为html canvas元素对应DOM元素，此处以设置高度为例，宽度就不重复了

获取高度：

```javascript
var pixel = canvas.height;
```

设置高度：

1.可以在js代码中设置

```javascript
canvas.height = pixel;
```

2.也可以在定义canvas元素的时候设置

```html
<canvas height="100"></canvas>
```



**需要注意的地方**

* 不可设置为小数

设置小数后其实会忽略小数部分，实际表现为高度100

```html
<canvas height="100.1"></canvas>
```

* 不能包含单位，比如

```html
<canvas height="100rem"></canvas>
```

* 高度的默认值

如果未设置高度，默认值会呈现为150

* 用css设置高度时，优先级关系

使用style内联样式的时候，css的属性权重要大于canvas，但实际使用API绘制canvas图像的时候，是以canvas的height属性为基准的


### getContext

此方法返回canvas的绘制上下文，这个上下文对象可以理解为我们实际绘图是所用到的对象，可以以此绘制各种图形和效果，使用的时候以canvas对象调用getContext返回绘图效果

```javascript
const canvas = document.querySelector('canvas');
const context = canvas.getContext('2d');
```





#### 参数1 contextType

* '2d'

返回的对象主要用来2d绘制，也就是平面绘图

* 'webgl'、'webgl2'

此参数可以返回一个WebGLRenderingContext（WebGL渲染上下文）对象，WebGL（全写Web Graphics Library）是一种3D绘图协议，可以为HTML5 Canvas提供硬件3D加速渲染，这样Web开发人员就可以借助系统显卡来在浏览器里更流畅地展示3D场景和模型，无需安装任何其他插件。



#### 参数2 contextAttributes

##### 1.如果contextType参数值是'2d'：
alph

表示Canavs是否包含alpha透明通道，如果设置为false，则表示Canvas不支持全透明或者半透明，在绘制带有透明效果的图形或者图像时候速度会更快一些。



##### 2.如果contextType参数值是'webgl'

alpha
表示Canavs是否包含透明缓冲区。

antialiasBoolean
表示是否需要抗边缘锯齿。如果设置为true，图像呈现质量会好一些，但是速度会拖慢。

depthBoolean
表示绘制缓冲区的缓冲深度至少16位。

failIfMajorPerformanceCaveatBoolean
表示如果用户的系统性能比较差，是否继续常见绘制上下文。

powerPreferenceString
高速用户使用的客户端（如浏览器）我们现在这个WebGL上下文最合适的GPU配置是什么。支持下面关键字值：

'default'
让用户的客户端设备自己觉得那个GPU配置是最合适的。这个是此参数的默认值。

'high-performance'
渲染性能优先，通常更耗掉（如手机，平板等移动设备）。

'low-power'
省电优先，渲染性能权重可以低一些。

premultipliedAlphaBoolean
表示页面合成器将假定绘图缓冲区包含具有alpha预乘（pre-multiplied alpha）颜色。

preserveDrawingBufferBoolean
如果值为true，则不会清除缓冲区并保留其值，直到作者清除或覆盖。

stencilBoolean
表示绘图缓冲区具有至少8位的模板缓冲区。


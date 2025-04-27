# CanvasRenderingContext2D

浏览器内建对象，用于在画布`Canvas`上渲染`Render`图形或文本`Context2D`

## HTML标签`<canvas>`

```html
<canvas id="mycanvas" width="600px" height="400px"
        style="border: 1px solid #d3d3d3; background-color: #ddd;">
    Your browser does not support the HTML5 canvas tag.
</canvas>
```

## 通过`HTMLCanvasElement.getContext()`获取对象

```js
const canvas = document.getElementById('mycanvas'); // HTMLCanvasElement 对象
const ctx = canvas.getContext('2d'); // CanvasRenderingContext2D 对象
```

## 通过构造器创建对象

```js
if (!window.CanvasRenderingContext2D) {
    alert('not support');
} else {
    const ctx = new CanvasRenderingContext2D();
}
```

## 对象参数设置

```js
// HTMLCanvasElement对象的只读引用
var cv = ctx.canvas;
```

```js
// 设置线宽
ctx.lineWidth = 1.0;

// 设置线末端形状（"butt|round|square"）
ctx.lineCap = 'butt';

// 设置线拐点形状（"miter|bevel|round"）
ctx.lineJoin = 'miter';

// 设置线拐点形状为miter时极限值
ctx.miterLimit = 10.0;

// 设置虚线偏移量
ctx.lineDashOffset = 0.0;
```

```js
// 设置画笔风格（Color颜色|CanvasGradient对象|CanvasPattern对象）
ctx.strokeStyle = 'red';

// 设置填充风格（Color颜色|CanvasGradient对象|CanvasPattern对象）
ctx.fillStyle = 'green';
```

```js
// 设置文本字体样式（如："bold 48px serif"）
ctx.font = '10px sans-serif';

// 设置文本对齐方式（"left|right|center|start|end"）基于坐标点
ctx.textAlign = 'center';

// 设置文本基线（"top|hanging|middle|alphabetic|ideographic|bottom"）
ctx.textBaseline = 'top';

// 设置文本方向（"ltr|rtl|inherit"）
ctx.direction = 'ltr';
```

```js
// 设置阴影模糊效果程度（default level=0）
ctx.shadowBlur = 0;
// 设置阴影颜色（default color=fully-transparent black）
ctx.shadowColor = 'black';
// 设置阴影偏移（default offset=0）
ctx.shadowOffsetX = 0;
ctx.shadowOffsetY = 0;       
```

```js
// 设置图形或图像透明度（范围0.0透明 - 1.0不透明）
ctx.globalAlpha = 0.5;

// 设置图形或图像重合规则
// source-over|source-in|source-out|source-atop|
// destination-over|destination-in|destination-out|destination-atop|
// color|color-dodge|color-burn|lighter|lighten|hard-light|soft-light|xor|
// copy|multiply|screen|overlay|darken|difference|exclusion|hue|saturation|luminosity
ctx.globalCompositeOperation = 'source-over';

// 设置图像是否平铺（true会有一定程度模糊|false）
ctx.imageSmoothingEnabled = true;
```

## 绘制矩形

```js
// 擦除画布矩形区域{ void ctx.clearRect(x, y, width, height) }
ctx.clearRect(0, 0, canvas.width, canvas.height);

// 绘制矩形{ void ctx.strokeRect(x, y, width, height) }
ctx.strokeRect(50, 10, 100, 75);

// 填充矩形{ void ctx.fillRect(x, y, width, height) }
ctx.fillRect(50, 10, 100, 50);
```

## 绘制文本

```js
var str = 'Hello World';

// 绘制文本{ void ctx.strokeText(text, x, y [, maxWidth]) }
ctx.strokeText(str, 200, 10);

// 填充文本{ void ctx.fillText(text, x, y [, maxWidth]) }
ctx.fillText(str, 200, 30);

// 测量文本显示所需宽度（不支持高度测量）{ TextMetrics ctx.measureText(text) }
var txtWidth = ctx.measureText(str).width;
```

## 绘制路径

```js
// 清空路径{ void ctx.beginPath() }
ctx.beginPath();

// 移动到点{ void ctx.moveTo(x, y) }
ctx.moveTo(100, 100);

// 当前点到指定点的直线路径{ void ctx.lineTo(x, y) }
ctx.lineTo(200, 100);

// 当前点到指定点的三次贝塞尔曲线路径，其中cpi为两个控制点{ void ctx.bezierCurveTo(cp1x, cp1y, cp2x, cp2y, x, y) }
ctx.bezierCurveTo(250, 125, 250, 175, 200, 200);

// 当前点到指定点的二次贝塞尔曲线路径，其中cp为控制点{ void ctx.quadraticCurveTo(cpx, cpy, x, y) }
ctx.quadraticCurveTo(250, 250, 200, 300);

// 圆弧路径{ void ctx.arc(x, y, radius, startAngle, endAngle[, anticlockwise=false]) }
ctx.arc(200, 300, 15, Math.PI/2, 0); // xxAngle=弧度，anticlockwise=true 逆时针方向

// 当前点到控制点1，控制点1到控制点2，两线夹角相切的圆弧路径{ void ctx.arcTo(cp1x, cp1y, cp2x, cp2y, radius) }
ctx.arcTo(215, 350, 265, 350, 50);

// 椭圆路径{ void ctx.ellipse(x, y, radiusX, radiusY, rotation, startAngle, endAngle[, anticlockwise]) }
ctx.ellipse(265, 350, 15, 30, 0, 0, 2*Math.PI); // rotation为旋转角度（弧度）

// 矩形路径{ void ctx.rect(x, y, width, height) }
ctx.rect(265, 350, 45, 45);

// 当前点到起始点的路径{ void ctx.closePath() }
ctx.closePath();

// 绘制路径{ void ctx.stroke() / (path) }
ctx.stroke();

// 填充路径{ void ctx.fill() / void ctx.fill(fillRule='nonzero|evenodd') / (path, fillRule) }
ctx.fill(); // 非零环绕或者奇偶环绕规则，决定点是在路径内还是在路径外
ctx.fill('evenodd');

// 剪切路径{ void ctx.clip() / (fillRule='nonzero|evenodd') / (path, fillRule) }
ctx.clip();
ctx.clip('evenodd');
```

## 路径（Path2D）

```js
// Path2D构造器
var path1 = new Path2D();
var path2 = new Path2D(path1);
var path3 = new Path2D('M10 10 h 80 v 80 h -80 Z'); // SVG Path字符串

// 路径内添加路径{ void path.addPath(new_path) }
path3.addPath(path2);

// 路径内绘制新路径{ path3.xxx() xxx=beginPath~closePath等方法 }
path3.rect(265, 350, 45, 45);

ctx.stroke(path3);
ctx.fill(path3, 'nonzero');
```

## 绘制图像

```js
var img = document.createElement("img");
img.src = "test.png";

// 绘制图像
// { void ctx.drawImage(image, dx, dy) 指定左上角坐标 }
// { void ctx.drawImage(image, dx, dy, dWidth, dHeight) 限制大小 }
// { void ctx.drawImage(image, sx, sy, sWidth, sHeight, dx, dy, dWidth, dHeight) 原图像裁减大小 }
img.onload = function() {
    ctx.drawImage(this, 50, 50);
}
```

## 图像数据（ImageData）

```js
// 图像数据构造函数{ new ImageData(array, width, height) / (width, height) }
var imageData = new ImageData(128, 128);

// 图像数据三个只读属性{ ImageData.data / ImageData.height / ImageData.width }
var m_data   = imageData.data;   // Uint8ClampedArray一维数组，RGBA字节（0-255）序列
var m_height = imageData.height;
var m_width  = imageData.width;

// 创建空白透明或复制图像数据{ ImageData ctx.createImageData(width, height) / (imagedata) }
var imageData2 = ctx.createImageData(imageData.data);

// 从画布提取图像数据{ ImageData ctx.getImageData(sx, sy, sw, sh) }
var imageData3 = ctx.getImageData(50, 50, 128, 128);

// 图像数据绘至画布
// { void ctx.putImageData(imagedata, dx, dy) }
// { void ctx.putImageData(imagedata, dx, dy, dirtyX, dirtyY, dirtyWidth, dirtyHeight) 裁减后绘至画布 }
ctx.putImageData(imageData3, 60, 60);
```

## 焦点（Focus）

```js
var btn = document.getElementById('button');
btn.focus();

// 给当前路径或特定路径绘制焦点{ void ctx.drawFocusIfNeeded(element) / (path, element) }
ctx.drawFocusIfNeeded(btn); // element须位于<canvas>标签内

var path = new Path2D();
path.moveTo(150, 150);
path.lineTo(200, 150);
path.lineTo(200, 200);
path.closePath();
ctx.stroke(path);
ctx.drawFocusIfNeeded(path, btn);
```

## 视窗（View）

```js
// 将当前或给定的路径滚动到窗口{ void ctx.scrollPathIntoView() / (path) }
ctx.scrollPathIntoView();
ctx.scrollPathIntoView(path);
```

## 线虚实

```js
// 获取当前线型样式数组{ Array ctx.getLineDash()  }
var arr = ctx.getLineDash();

// 设置线型样式{ void ctx.setLineDash(segments) 数组元素为偶数 }
ctx.setLineDash([5, 10]); // 虚线
ctx.setLineDash([]);      // 实线
```

## 渐变效果（CanvasGradient）

```js
var gradient;
// 沿直线渐变{ CanvasGradient ctx.createLinearGradient(x0, y0, x1, y1) }
gradient = ctx.createLinearGradient(0, 0, 50, 50);
// 沿两个圆放射性渐变{ CanvasGradient ctx.createRadialGradient(x0, y0, r0, x1, y1, r1) }
gradient = ctx.createRadialGradient(200, 200, 15, 200, 200, 45);

// 设置过渡颜色{ void CanvasGradient.addColorStop(offset, color) 偏移取值0~1之间 }
gradient.addColorStop(0, 'red');
gradient.addColorStop(0.5, 'blue');
gradient.addColorStop(1, 'green');

ctx.strokeStyle = gradient;
ctx.fillStyle   = gradient;
```

## 画布模式（CanvasPattern）

```js
// 指定图像绘制模式{ CanvasPattern ctx.createPattern(image, repetition=repeat|repeat-x|repet-y|no-repeat) }
var pattern = ctx.createPattern(img, 'repeat');

ctx.strokeStyle = pattern;
ctx.fillStyle   = pattern;
```

## 点检测

```js
// 判断在当前路径中是否包含检测点
boolean ctx.isPointInPath(x, y);
boolean ctx.isPointInPath(x, y, fillRule);
boolean ctx.isPointInPath(path, x, y);
boolean ctx.isPointInPath(path, x, y, fillRule);

// 检测某点是否在路径的描边线上
boolean ctx.isPointInStroke(x, y);
boolean ctx.isPointInStroke(path, x, y);
```

## 变换

```js
// 旋转
void ctx.rotate(angle);

// 缩放
void ctx.scale(x, y); //缩放因子（倍数）
ctx.scale(-1, 1) // 水平翻转上下文
ctx.scale(1, -1) // 垂直翻转上下文

// 原点平移
void ctx.translate(x, y);

// 变换矩阵（叠加）
void ctx.transform(a, b, c, d, e, f);
// a (m11)水平缩放。
// b (m12)垂直倾斜。
// c (m21)水平倾斜。
// d (m22)垂直缩放。
// e (dx)水平移动。
// f (dy)垂直移动。

void ctx.setTransform(a, b, c, d, e, f);//重新设置当前的变换为单位矩阵
void ctx.resetTransform(); //使用单位矩阵

// 变换矩阵属性
ctx.currentTransform = matrix //matrix.{a,b,c,d,e,f}
```

## 保存

```js
// 将当前绘制状态放入栈中，保存 canvas 全部状态
void ctx.save();

// 状态栈中绘制状态出栈
void ctx.restore();
```

- 保存到栈中的绘制状态有下面部分组成：
  - 当前的变换矩阵
  - 当前的剪切区域
  - 当前的虚线列表
  - 以下属性当前的值：
    - strokeStyle
    - fillStyle
    - globalAlpha
    - lineWidth
    - lineCap
    - lineJoin
    - miterLimit
    - lineDashOffset
    - shadowOffsetX
    - shadowOffsetY
    - shadowBlur
    - shadowColor
    - globalCompositeOperation
    - font
    - textAlign
    - textBaseline
    - direction
    - imageSmoothingEnabled

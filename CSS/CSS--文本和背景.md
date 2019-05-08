# CSS设置文本

> <p style="font-size:18px">文本样式</p>

属性名 | 属性值 | 说明
---|---|---
color<br/>颜色 | #red<br/>#FF00FF<br/>rgb(0,255,255)<br/>rgba(0,0,255,0.5)|预设值，英文颜色<br/>十六进制颜色值<br/>色彩函数(红，绿，蓝)<br/>色彩函数(红，绿，蓝，透明度)
text-align<br/>水平对齐 | left<br/>right<br/>center<br/>justify|左对齐<br/>右对齐<br/>居中对齐<br/>两端对齐
vertical-align<br/>垂直对齐|middle<br/>top<br/>bottom|垂直居中<br/>顶部对齐<br/>底部对齐
text-indent<br/>首行缩进|px<br/>em<br/>rem|像素<br/>相对单位长度<br/>根相对单位长度
line-height<br/>文本行高|px<br/>em<br/>rem|像素<br/>相对单位长度<br/>根相对单位长度
text-decoration<br/>文本装饰|none<br/>underline<br/>overline<br/>line-through|标准文本<br/>下划线<br/>上划线<br/>删除线
text-shadow<br/>文本阴影|color<br/>x-offset<br/>y-offset<br/>blur-radius|阴影颜色<br/>X轴位移<br/>Y轴位移<br/>模糊半径


***

> <p style="font-size:18px">字体样式</p>

属性名 | 属性值 | 说明
---|---|---
font-family<br/>字体类型|"宋体"<br/>"楷体"等<br/>|计算机默认字体<br/>项目引用的自定义字体
font-size<br/>字体大小|px<br/>em<br/>rem|像素<br/>相对单位长度<br/>根相对单位长度
font-style<br/>字体风格|normal<br/>italic<br/>oblique<br/>inherit|正常字体<br/>斜体<br/>字体倾斜<br/>继承父元素风格
font-weight<br/>字体粗细|normal<br/>bold<br/>bolder<br/>lighter<br/>100~900|正常字体<br/>粗体<br/>更粗<br/>更细<br/>值范围：400为正常，700为粗体
letter-spacing<br/>字体间距|px<br/>em<br/>rem|像素<br/>相对单位长度<br/>根相对单位长度

***


# CSS设置背景

> <p style="font-size:18px">背景样式</p>

属性名 | 属性值 | 说明
---|---|---
background-color<br/>背景颜色| #red<br/>#FF00FF<br/>rgb(0,255,255)<br/>rgba(0,0,255,0.5)|预设值，英文颜色<br/>十六进制颜色值<br/>色彩函数(红，绿，蓝)<br/>色彩函数(红，绿，蓝，透明度)
background-position<br/>背景图像起始位置|xpos ypos<br/>x% y%<br/>x:left/center/right<br/>y:top/center/bottom|固定值，单位可以是px/em/rem<br/>相对值<br/>指定X位置<br/>指定Y位置
background-size<br/>背景图像大小|weight height<br/>percentage<br/>cover<br/>contain|固定大小<br/>相对大小<br/>最大填充<br/>最小填充
background-repeat<br/>背景图像重复方式|repeat<br/>repeat-x<br/>repeat-y<br/>no-repeat|正常横纵重复<br/>横向重复<br/>纵向重复<br/>不重复
background-attachment<br/>背景图像是否滚动|scroll<br/>fixed<br/>inherit|滚动<br/>固定<br/>继承父元素设置
background-image<br/>背景图像|url('URL')<br/>none|图像的URL<br/>不显示，默认

***

> <p style="font-size:18px">颜色渐变</p>
> <p style="color:blue">线性渐变：颜色沿着一条直线过度（方向性）：从左到右，从右到左，从上到下 等。</p>

- 渐变兼容（属性前加前缀,用于解析）
    - IE浏览器：-ms-linear-gradient(渐变方向,第一种颜色,第二种颜色,...)
    - Chrome和Safari浏览器：-webkit-linear-gradient(渐变方向,第一种颜色,第二种颜色,...)
    - Opera浏览器：-o-linear-gradient(渐变方向,第一种颜色,第二种颜色,...)
    - Firefox浏览器：-moz-linear-gradient(渐变方向,第一种颜色,第二种颜色,...)

> <p style="color:blue">径向渐变：圆形circle或椭圆形ellipse渐变，颜色不在沿着一条直线变化，而是从一个起点朝所有方向混合。</p>

- 渐变兼容（属性前加前缀,用于解析）
    - IE浏览器：-ms-radial-gradient(渐变形状,第一种颜色,第二种颜色,...)
    - Chrome和Safari浏览器：-webkit-radial-gradient(渐变形状,第一种颜色,第二种颜色,...)
    - Opera浏览器：-o-radial-gradient(渐变形状,第一种颜色,第二种颜色,...)
    - Firefox浏览器：-moz-radial-gradient(渐变形状,第一种颜色,第二种颜色,...)


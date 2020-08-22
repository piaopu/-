# CSS


### 盒模型
Margin(外边距) - 清除边框外的区域，外边距是透明的。
Border(边框) - 围绕在内边距和内容外的边框。
Padding(内边距) - 清除内容周围的区域，内边距是透明的。
Content(内容) - 盒子的内容，显示文本和图像。

##### clientWidth的实际宽度
clientWidth = width+左右padding
##### offsetWidth的实际宽度
offsetWidth = width + 左右padding + 左右border


### 选择器分类
元素选择器 a{}
伪元素选择器 ::before{}
类选择器 .link{}
属性选择器 [type=radio]{} 
伪类选择器 :hover{}
ID选择器 #id{}
组合选择器 [type=checkbox]+label{}
否定选择器 :not(.link){}
通用选择器 *{}

### 选择器权重
选择器本身的权重 加法不进位
ID选择器 #id{} +100
类 属性 伪类 +10
元素 伪元素 +1
其他选择器 +0
其他情况
！important 优先级最高
内联样式优先级高 +1000
相同权重，后写的生效



### 伪元素和伪类的区别
伪元素 ：：before ：：after
伪元素在DOM树中创建了一些抽象元素，这些抽象元素是不存在于文档语言里的。伪元素是真实存在的，可以有内容和样式。
伪类 ：hover ：focus
伪类存在的意义是为了通过选择器找到那些不存在与DOM树中的信息以及不能被常规CSS选择器获取到的信息。伪类相当于选中的一种状态。


### css 中可继承的属性
所有元素可继承：visibility和cursor。
内联元素可继承：letter-spacing、word-spacing、white-space、line-height、color、font、font-family、font-size、font-style、font-variant、font-weight、text-decoration、text-transform、direction。
终端块状元素可继承：text-indent和text-align。
列表元素可继承：list-style、list-style-type、list-style-position、list-style-image。


### margin 参数
margin标记可以带一个、二个、三个、四个参数，各有不同的含义
margin: 20px;（上、下、左、右各20px。）
margin: 20px 40px;（上、下20px；左、右40px。）
margin: 20px 40px 60px;（上20px；左、右40px；下60px。）
margin: 20px 40px 60px 80px;（上20px；右40px；下60px；左80px。）



### display:none   VS   visibility:hidden
display:none和visibility:hidden都能把网页上某个元素隐藏起来，但是两者有区别：
#### 一、display:none
1、不为被隐藏的对象保留其物理空间。html对象在页面上彻底消失（display:none会让元素完全从渲染树中消失，渲染的时候不占据任何空间）。
2、是非继承属性，子孙节点消失由于元素从渲染树消失造成的，通过修改子孙节点，属性无法显示。
3、修改常规文档流元素的display通常会造成文档的重排（reflow）重绘（repaint）。
#### 二、visibility:hidden
1、为隐藏的对象保留其物理空间，html对象仅仅是在视觉上看不见（完全透明），而它所占据的空间位置仍然存在（visibility:hidden不会让元素从渲染树中消失，渲染树元素继续占据空间，只是内容不可见）。
2、是继承，子孙节点消失由于继承了hidden，通过visibility:visible可以让子孙节点显示。
3、修改visibility属性只会造成文档的重绘（repaint）。


### position属性
确定元素位置
static静态/relative相对/absolute绝对/fixed固定
static：默认情况，按照文件流布局
relative：相对元素本身的偏移，不改变原来占据的空间
absolute：脱离文件流，独立存在，就近原则，相对于最近的relative、absolute
fixed：从文件流脱离，不影响其他，独立存在，相对于可视区域viewport

### 为什么要清除浮动？
清浮动是为了清除使用浮动元素产生的影响。浮动的元素，高度会塌陷，而高度的塌陷使页面后面的布局不能正常显示。

### 如何清除浮动？
+ clear清除浮动（添加空div法）在浮动元素下方添加空div,并给该元素写css样式：{clear:both;height:0;overflow:hidden;}
+ 给浮动元素父级设置高度
+ 父级同时浮动（需要给父级同级元素添加浮动）
+ 父级设置成inline-block，其margin: 0 auto居中方式失效
+ 给父级添加overflow:hidden 清除浮动方法
+ 万能清除法 after伪元素 清浮动（现在主流方法，推荐使用）


### BFC (Block formatting context)
直译为块级格式化上下文
W3C对BFC的定义如下：浮动元素和绝对定位元素，非块级盒子的块级容器（例如 inline-blocks, table-cells, 和 table-captions），以及overflow值不为“visible”的块级盒子，都会为他们的内容创建新的BFC（块级格式上下文）。
为了便于理解，我们换一种方式来重新定义BFC。一个HTML元素要创建BFC，则满足下列的任意一个或多个条件即可：
1、float的值不是none。
2、position的值不是static或者relative。
3、display的值是inline-block、table-cell、flex、table-caption或者inline-flex
4、overflow的值不是visible
BFC是一个独立的布局环境，其中的元素布局是不受外界的影响，并且在一个BFC中，块盒与行盒（行盒由一行中所有的内联元素所组成）都会垂直的沿着其父元素的边框排列。


### a:link,a:visited,a:hover,a:active 分别是什么意思?
1. link:连接平常的状态
2. visited:连接被访问过之后
3. hover:鼠标放到连接上的时候
4. active:连接被按下的时候
正确顺序：“爱恨原则”（LoVe/HAte），即四种伪类的首字母:LVHA。再重复一遍正确的顺序：a:link、a:visited、a:hover、a:active


text-shadow 属性中的四个值（length,length,length,color）分别的意义：阴影离开文字的横方向距离，阴影离开文字的纵方向距离，阴影的模糊半径，阴影的颜色


### 响应式设计和布局
响应式网站设计(Responsive Web design)是一个网站能够兼容多个终端，而不是为每一个终端做一个特定的版本
主要方法：隐藏+折行+自适应空间
rem/viewport/media query媒体查询

### flex 弹性盒子
flex 是 Flexible Box 的缩写，意为"弹性布局"，用来为盒状模型提供最大的灵活性。
#### flex属性
flex属性是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto。后两个属性可选。该属性有两个快捷值：auto (1 1 auto) 和 none (0 0 auto)。建议优先使用这个属性，而不是单独写三个分离的属性，因为浏览器会推算相关值。

- flex-grow属性定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大。
- flex-shrink属性定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小。
- flex-basis属性定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为auto，即项目的本来大小。


### CSS3 新特性
#### css3的新选择器
E:nth-child(n) 选择器匹配其父元素的第n个子元素，不论元素类型，n可以使数字，关键字，或公式
E:nth-of-type(n) 选择与之其匹配的父元素的第N个子元素
E:frist-child 相对于父级做参考，“所有”子元素的第一个子元素，并且“位置”要对应
E:frist-of-type 相对于父级做参考，“特定类型”（E）的第一个子元素
E:empty 选择没有子元素的每个E元素
E:target 选择当前活动的E元素
::selection 选择被用户选取的元素部分
属性选择器
E[abc*="def"] 选择adc属性值中包含子串"def"的所有元素

#### 文本
text-shadow:2px 2px 8px #000;参数1为向右的偏移量，参数2为向左的偏移量，参数3为渐变的像素，参数4为渐变的颜色
text-overflow：规定当文本溢出包含元素时发生的事情 text-overflow:ellipsis(省略)
text-wrap：规定文本换行的规则
word-break 规定非中日韩文本的换行规则
word-wrap：对长的不可分割的单词进行分割并换行到下一行
white-space：规定如何处理元素中的空白 white-space:nowrap 规定段落中的文本不进行换行
font-face属性：定义自己的字体


#### 边框
border-raduis 边框的圆角
border-image 边框图片

#### 背景
- rgba
RGBA是RGB色彩模型的一个扩展。在本质上看也是为设置的元素增加了一个 alpha 通道，即除了红绿蓝三种颜色外还增加一个代表透明度的通道，其中 RGB 值分别表示红色、绿色、蓝色，而 alpha 取值则为 0 到 1 （小数位一位）。

- background-image：设置元素的背景图像。
- background-origin：规定背景图片的定位区域。
- background-repeat：设置是否及如何重复背景图像。

- backgrounnd-size: cover/contain
background-size: cover，会使“最大”边进行缩放，另一边同比缩放，铺满容器，超出部分会溢出。
background-size: contain，会使“最小”边进行缩放，另一边同比缩放，不一定铺满容器，会完整显示图片。

#### 渐变
- linear-gradient
background-image:linear-gradient(90deg,yellow 20%,green 80%)
- radial-gradient
background-iamge:radial-gradient(120px at center center,yellow,green)

#### 多列布局
column-count
column-width
column-gap
column-rule

+ 过渡
transition
transition-property:width //property为定义过渡的css属性列表，列表以逗号分隔
transition-duration:2s; //过渡持续的时间
transition-timing-function:ease;
transition-delay:5s //过渡延迟5s进行

#### 动画、旋转
animation
transform ：translate（x,y) rotate(deg) scale(x,y)
translate
scale
rotate
skew（倾斜）

#### flex布局

#### @media媒体查询
@media screen and (max-width: 300px) {
    body {
        background-color:lightblue;
    }
}



### 如何居中div
#### 水平居中
- 水平居中1：给 div 设置一个宽度，然后添加 margin:0 auto; 属性
- 水平居中2：利用 text-align:center 实现

#### 水平垂直居中
- 确定容器的宽高，top left + margin

- 未知容器宽高，利用 transform 属性
div{
  position: absolute;
  width: 500px;
  height: 300px;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: pink;
}

- 利用 flex 布局，实际应用需要考虑兼容性
.container{
  display: flex;
  align-items: center; /* 垂直居中 */
  justify-content: center; /* 水平居中 */
} 



### 如何用纯 CSS 创建一个三角形？
将元素的宽高设为0，只设置 border ,将任意三条边隐藏掉（颜色设为 transparent ）,剩下的就是一个三角形



### width: auto 和 width: 100% 的区别？
·width: 100% 会使元素box的宽度等于父元素的content box的宽度
·width: auto 会时元素撑满整个父元素，margin, border, padding, content 区域会自动分配水平




### 使用 base64 编码的优缺点

base64编码是一种图片处理格式，通过特定的算法将图片编码成一长串字符串，在页面上显示时可用该字符串来代替图片的url属性
##### 使用base64的优点
① 减少一个图片的 HTTP 请求
##### 使用base64的缺点
① 根据base64的编码原理，编码后的大小会比源文件大小大1/3，如果把大图片编码到html/css中，
不仅会造成文件体积增加，影响文件的加载速度，还会增加浏览器对html或css文件解析渲染的时间。
② 使用base64无法直接缓存，要缓存只能缓存包含base64的文件，比如HTML 或CSS，
这相比于直接缓存图片的效果要差很多。
③ ie8以前的浏览器不支持
一般一些网站的小图标可以使用base64图片引入



### px、em、rem区别介绍
px 像素（Pixel）。相对长度单位。像素px是相对于显示器屏幕分辨率而言的。
em 是相对长度单位。相对于当前对象内文本的字体尺寸。如当前对行内文本的字体尺寸未被人为设置，则相对于浏览器的默认字体尺寸。特点是：em的值并不是固定的；em会继承父级元素的字体大小
rem是CSS3新增的一个相对单位（root em，根em），网页中，rem 作为元素尺寸单位时，是相对文档根节点的 font-size 进行计算的

### px 与 rem 的选择？
对于只需要适配少部分手机设备，且分辨率对页面影响不大的，使用px即可 。
对于需要适配各种移动设备，使用rem，例如只需要适配iPhone和iPad等分辨率差别比较挺大的设备。
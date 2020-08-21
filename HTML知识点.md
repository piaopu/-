# HTML
### DOCTYPE的作用
DOCTYPE主要作用是告诉浏览器的解析器使用哪种HTML规范或者XHTML规范来解析页面。
<!DOCTYPE>不存在或者形式不正确会导致HTML或XHTML文档以混杂模式呈现，就是把如何渲染html页面的权利交给了浏览器，有多少种浏览器就有多少种展示方式。
<!DOCTYPE html> 是HTML5中唯一的DOCTYPE
+ 严格模式：又称标准模式，是指浏览器按照W3C标准来解析代码，呈现页面
+ 混杂模式：又称为怪异模式或者兼容模式，是指浏览器按照自己的方式来解析代码，使用一种比较宽松的向后兼容的方式来显示页面。


### HTML5提供的数据存储
localStorage  没有时间限制的数据存储
sessionStorage  针对一个session的数据存储


### 请描述一下 Cookie，sessionStorage 和 localStorage 的区别？

+ Cookie 是网站为了标示用户身份而储存在用户本地终端（Client Side）上的数据（通常经过加密），Cookie 数据始终在同源的 http 请求中携带（即使不需要），会在浏览器和服务器间来回传递。

+ Cookie的处理分为
服务器向客户端发送cookie -> 浏览器将cookie保存 -> 之后每次http请求浏览器都会将cookie发送给服务器端

+ sessionStorage 和 localStorage 不会自动把数据发给服务器，仅在本地保存。

+ 存储大小
- cookie 数据大小不能超过 4k；
- sessionStorage 和 localStorage 虽然也有存储大小的限制，但比 cookie 大得多，可以达到 5M 或更大。

+ 有效期（生命周期）
- localStorage: 存储持久数据，浏览器关闭后数据不丢失除非主动删除数据；
- sessionStorage: 数据在当前浏览器窗口关闭后自动删除；
- cookie: 设置的 cookie 过期时间之前一直有效，即使窗口或浏览器关闭。

+ 共享
- sessionStorage 不能共享，localStorage 在同源文档之间共享，cookie 在同源且符合 path 规则的文档之间共享。


### HTML5 语义化标签
语义化的标签，说明让标签有自己的含义。
特点：
+ 代码结构清晰，方便阅读，有利于团队合作开发；
+ 有利于搜索引擎优化（SEO）；
+ 便于团队开发和维护，语义化更具可读性，遵循W3C标准的团队都遵循这个标准，可以减少差异化。


### HTML5的新变化
+ 取消了一些过时Html4标记
   其中包括纯粹显示效果的标记，譬如`<font>`,`<center>`，它们已被CSS取代。
   HTML5吸取了XHTML2的一些建议，包括一些用来改善文档结构的功能。譬如：header、footer、dialog、aside、figure、等新HTML标签，将使内容创作者更加语义地创建文档，之前的开发者在实现这些功能时一般都是使用div标签。

+ 将内容和展示分离
   b 和 i 标签依然保留，但它们的意义已经和之前有所不同，这些标签的意义只是为了将一段文字标识出来，而不是为了把它们设置成粗体或斜体式样。u、font、center、strike 标签则被完全删除。

+ 全新表单输入对象
   包括日期、URL、Email 地址，其它对象则增加了对非拉丁字符的支持。HTML5还引入了微数据，这种使机器能识别标签标注内容的方法，可使Web语义的处理变得更为简单。总的来说，这些与结构有关的改进使内容创建者可创建更干净、更容易管理的网页，这样的网页对搜索引擎、读屏软件、等更为友好。

+ 全新、更合理的Tag
   多媒体对象将不再全部绑定在object或embed Tag中，而是视频有视频的Tag，音频有音频的Tag。

+ 本地数据库
   这个功能将内嵌一个本地SQL数据库，以加速交互式搜索，缓存以及索引功能。同时，那些离线Web程序也将因此获益匪浅。无需插件丰富动画。

+ Canvas 对象
   将给浏览器带来直接在上面绘制矢量图的能力，这意味着用户可脱离Flash和Silverlight，直接在浏览器中显示图形或动画。

+ 浏览器中的真正程序
   将提供API实现浏览器内的编辑、拖放、各种图形用户界面的能力。内容修饰Tag将被剔除，而使用CSS。

+ HTML5取代Flash在移动设备的地位

+ 强化web页面表现，追加本地数据库


### Canvas vs. SVG
Canvas 和 SVG 都允许在浏览器中创建图形，但是它们在根本上是不同的。
+ SVG 是一种使用 XML 描述 2D 图形的语言。SVG 绘制的图形为矢量图。
+ Canvas 通过 JavaScript 来绘制 2D 图形。Canvas 是逐像素进行渲染的。Canvas 绘制出来的图形为标量图。

矢量图放大多少倍，都不会出现马赛克，永远都是清晰的；
位图放大比原图尺寸的倍数后，就会出现马赛克，不清晰了，看着就模糊了。


### form的作用
+ 直接提交表单
+ 使用submit和reset按钮
+ 便于浏览器保存表单
+ 第三方库可以整体提取
+ 第三方库可以进行表单验证


### 块元素和行内元素
+ 块元素，总是在新行上开始；行内元素，和其他元素在一行；
+ 块元素，能容纳其他块元素或者内联元素；行内元素，只能容纳文本或其他行内元素；
+ 块元素中高度，行高以及顶和底边距都可以控制；行内元素中高，行高及顶和底边距不可改变。

常见块级元素有：h1，h2，h3，h4，h5，h6，p，div，dl，dt，hr，ol，ul，li，form，pre，table，td，th

常见内联元素有：em，strong，span，button，input，label，code，select，img，textarea



### property 和 attribute 的区别
property是DOM中的属性，是JavaScript里的对象；
attribute是HTML标签上的特性，它的值只能够是字符串 / attribute就是dom节点自带的属性，例如html中常用的id、class、title、align等。

attribute是死的，property是活的


### iframe 有那些缺点？
+ iframe 会阻塞主页面的 Onload 事件；
+ 搜索引擎的检索程序无法解读这种页面，不利于 SEO;
+ iframe 和主页面共享连接池，而浏览器对相同域的连接有限制，所以会影响页面的并行加载。


### meta标签
一个常用的针对移动网页优化过的页面的 viewport meta 标签大致如下：
`<meta name="viewport" content="width=device-width, initial-scale=1.0">`

+ width：控制 viewport 的大小，可以指定的一个值，如 600，或者特殊的值，如 device-width 为设备的宽度（单位为缩放为 100% 时的 CSS 的像素）。
+ height：和 width 相对应，指定高度。
+ initial-scale：初始缩放比例，也即是当页面第一次 load 的时候缩放比例。
+ maximum-scale：允许用户缩放到的最大比例。
+ minimum-scale：允许用户缩放到的最小比例。
+ user-scalable：用户是否可以手动缩放。



### 哪些元素可以自闭合？
   `<input>`    `<img>`    `<br>` `<hr>`    `<meta>` `<link>`


### img标签 中 title 属性和 alt 属性的区别？
当图片不输出信息的时候，会显示 alt 信息，鼠标放上去会出现 title 信息；
当图片正常输出的时候，不会出现 alt 信息，鼠标放上去会出现 title 信息。







# Web前端性能优化的N种方法

## 1. 启用压缩功能
许多网络服务器可以通过调用第三方模块或使用内置程序将文件压缩为gzip格式，然后再发送该压缩文件以供下载。这样可以在下载呈现网站所需的资源时，为您节省一些时间。

详见：https://developers.google.com/speed/docs/insights/EnableCompression

## 2. 使用浏览器缓存
如果用户会多次访问您的网站，那么静态资源的浏览器缓存可以节省用户的时间。缓存标头应当应用到所有可缓存的静态资源中，而不仅仅是应用到一小部分静态资源（例如，图片）中。可缓存的资源包括JS和CSS文件、图像文件及其他二进制对象文件（媒体文件和PDF文件等）。通常情况下，HTML不是静态资源，默认情况下不应被视为可缓存资源。您应考虑哪些缓存政策适用于您网站的HTML。
+ 使用Expires和Cache-Control: max-age标头
+ 使用Last-Modifed和ETag标头
+ 使用网址指纹(fingerprint)

详见：https://developers.google.com/speed/docs/insights/LeverageBrowserCaching

## 3. 优化图片
尽量减小图片尺寸，以缩减用户等待资源加载的时间。适当地设置图片的格式并进行压缩可以节省大量的数据字节空间。这样可以为那些网络连接较慢的用户节约时间，还可以为有流量套餐限制的用户节省成本。

您应对所有图片进行基本优化和高级优化。基本优化包括裁剪不必要的区域，将颜色深度降至可接受的最低水平，移除图片评论以及将图片保存为恰当的格式。您可以使用任意图片编辑程序（例如，GIMP）执行基本优化。高级优化包括对JPEG和PNG文件执行进一步的压缩（无损压缩）。

详见：https://developers.google.com/speed/docs/insights/OptimizeImages

## 4. 移除阻止呈现的JavaScript
浏览器必须先解析网页，然后才能将其呈现给用户。如果浏览器在解析过程中遇到系统阻止的外部脚本，必须停止解析并且下载该JavaScript。每次遇到这种情况时，浏览器都会增加一个网络往返过程，这样就会导致首次呈现网页的时间延迟。

建议您以内嵌方式处理呈现首屏区域所需的JavaScript，并让为网页添加其他功能所需的JavaScript延迟加载，直到首屏内容发送完毕为止。请注意，要通过这种方式缩短加载时间，您还必须优化CSS发送过程。
+ 内嵌较小的JavaScript
+ 延迟加载JavaScript(async和defer属性)
+ 服务端渲染

详见：https://developers.google.com/speed/docs/insights/BlockingJS

## 5. 优化CSS发送过程
屏幕显示内容之前，浏览器会阻止外部CSS文件。这会导致额外的网络延迟，并延长屏幕显示内容的时间。
+ 内嵌较小CSS文件
+ 请勿内嵌较大数据URI
+ 请勿内嵌CSS属性

详见：https://developers.google.com/speed/docs/insights/OptimizeCSSDelivery

## 6. 缩减资源（HTML、CSS和JavaScript）的大小
缩减资源大小是指删除不必要的字节（例如，多余的空格、换行符和缩进）。压缩HTML、CSS和JavaScript可提高下载、解析和执行的速度。此外，对于CSS和JavaScript，还可通过以下方式进一步缩小文件体积：在对HTML进行适当更新的过程中重命名变量名称，以确保选择器继续运行。

详见：https://developers.google.com/speed/docs/insights/MinifyResources

## 7. 缩减首屏内容的大小
如果所需的数据量超出初始拥塞窗口的限制，系统就需要在服务器和用户浏览器之间进行更多次的往返。如果用户使用的是延迟时间较长的网络（例如，移动网络），该问题会严重延迟网页的加载。

为提高网页加载速度，请限制呈现网页首屏内容所需的数据（HTML标记、图片、CSS和JavaScript）大小。为此，您可以尝试以下几种方法：
+ 结构化HTML，以便首先加载关键的首屏内容
+ 减少资源所用的数据量

详见：https://developers.google.com/speed/docs/insights/PrioritizeVisibleContent

## 8. 改善服务器响应时间
服务器响应时间表示加载必要HTML以开始呈现服务器所托管网页的时间，其中减去了Google和服务器之间的网络延迟时间。每次运行所用的时间可能会有所不同，但这种差异不应太大。事实上，如果服务器响应时间变化很大的话，则表明性能上可能存在问题。

详见：https://developers.google.com/speed/docs/insights/Server

## 9. 避免目标网页重定向
由于重定向会触发额外的HTTP请求响应周期，并会额外延长往返时间延迟，因此，将应用发出的重定向数量降至最低至关重要。避免HTTP重定向可以缩减用户等待网页加载的时间。我们建议您仔细斟酌自己网站的设计，看看可以在哪些方面提升网站性能。

详见：https://developers.google.com/speed/docs/insights/AvoidRedirects

## 10. Facebook的BigPipe技术
BigPipe提出分块的概念，即根据页面内容位置的不同，将整个页面分成不同的块儿——称为pagelet。该技术的设计者Changhao Jiang 是研究电子电路的博士，可能从微机上得到了启发，将众多pagelet加载的不同阶段像流水线一样在浏览器和服务器上执行，这样就做到了浏览器和服务器的并行化，从而达到重叠服务器端运行时间和浏览器端运行时间的目的。使用BigPipe 不仅可以节省时间，使加载的时间缩短，而且可以同过pagelet的分步输出，使一部分的页面内容更快的输出，从而获得更好的用户体验。

详见：[GitHub](https://github.com/bigpipe/bigpipe) or [BigPipe学习研究](http://www.searchtb.com/2011/04/an-introduction-to-bigpipe.html)

## 11. 预加载技术
预先告知浏览器某些资源可能在将来会被使用到。具体包括以下几种技术：
+ DNS预解析 dns-prefetch
+ 预连接 preconnect
+ 预获取 prefetch
+ subresource
+ 预渲染 prerender
+ 预加载 preload

详见：[前端性能优化 - 资源预加载](http://bubkoo.com/2015/11/19/prefetching-preloading-prebrowsing/)

## 12. 方兴未艾的WebAssembly
WebAssembly是一种新的字节码格式。它的缩写是".wasm"，.wasm 为文件名后缀，是一种新的底层安全的二进制语法。它被定义为“精简、加载时间短的格式和执行模型”，并且被设计为Web 多编程语言目标文件格式。 这意味着浏览器端的性能会得到极大提升，它也使得我们能够实现一个底层构建模块的集合，例如，强类型和块级作用域。 支持WebAssembly的浏览器可以识别二进制格式的文本，它有能力编译比JS文本小得多的二进制包。相比解析js代码，JavaScript引擎破译二进制格式的速度要快得多。 这将给web应用带来类似与本地应用的性能体验。Webassembly让开发者有能力选择之前那些不能用来开发web应用的语言来进行web开发，或者他们也可以继续使用简单易用的JavaScript。

详见：[来谈谈WebAssembly是个啥？为何说它会影响每一个Web开发者？](http://imweb.io/topic/567fd838834878282edc7f9b)

## 13. CSS Sprites
合并CSS图片，有效减少图片的请求次数。

## 14. Icon Font技术
图标字体技术是把一些简单的图标制作成字体，然后让图标变成和字体一样使用。

## 15. CDN加速
CDN（contentdistribute network，内容分发网络）的本质仍然是一个缓存，而且将数据缓存在离用户最近的地方，使用户以最快速度获取数据，即所谓网络访问第一跳。另外，浏览器对与同一域名的并行下载数量是有限制的，使用CDN可有效加快并行下载速度。

## 16. Lazy Load Images
在页面刚加载的时候可以只加载第一屏中的图片，当用户继续往后滚屏的时候才加载后续的图片。比如有jQuery插件[Lazy Load](http://www.appelsiini.net/projects/lazyload)。

## 17. 反向代理
传统代理服务器位于浏览器一侧，代理浏览器将http请求发送到互联网上，而反向代理服务器位于网站机房一侧，代理网站web服务器接收http请求，如下图所示。比如有著名的：Nginx。
![反向代理架构图](http://img.blog.csdn.net/20160521222319255)

## 18. WebSocket与Socket.IO

## 19. CSS选择器优化

## 20. JavaScript代码优化





(未完待续)

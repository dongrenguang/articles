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

(未完待续)

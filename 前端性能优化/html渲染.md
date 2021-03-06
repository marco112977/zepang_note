# html渲染

当用户在浏览器中输入一个网址之后，浏览器请求相关的地址会的带HTML的字符串。然后对HTML字符串由上到下进行词法分析，并且不断的生成dom树，在此过程中，如果发现需要外部资源，将会进行外部资源的加载，比如css，css加载完毕之后也会进行如上的css词法分析并生成css树，这个过程和生成dom的过程是同步的。这也就为什么我们通常会把一些js脚本放在HTML文档的尾部进行加载，一方面是加载js的时候会阻塞渲染，一方面是js脚本中有可能涉及dom节点的操作，避免在dom节点未生成的情况下脚本报错。在dom树和css树完成之后会生成渲染树，然后进行布局，绘画。

# HTML渲染过程的一些特点

- 顺序执行、并发加载

并发加载的时候需要注意的HTTP的客户端对同一个服务器的并发连接数是有限制的，所以一般情况下，为了加载所有的资源，都会给静态资源使用多个cdn域名，这些个域名最后解析的资源都是同一个，以对多个域名的请求来加载更多的资源。

- 是否阻塞

- 依赖关系

- 引入方式

# css阻塞

- css在HTML中通过link标签引入会阻塞页面的渲染，这里说的阻塞是css的加载过程。这就是为了避免页面的闪动我们需要将css link写在head中的原因，就是为了等css加载完毕之后在进行渲染，这样渲染的时候页面是带样式的。

- css加载阻塞js的执行。因为js的执行可以需要css或者会影响css的属性。

- css加载不会阻塞外部脚本的加载

# js阻塞

- 直接引入（不是使用sync 或者 defer）的js阻塞页面渲染。因为js代码有可能会改变dom树或者css树，所以客户端会等js执行完毕之后才会渲染。

- js执行不阻塞资源的加载

- js顺序执行，阻塞后续js逻辑的执行。在顺序引入的情况下，无论哪个提前返回，最后执行都是按照引入的顺序执行。

# 懒加载和预加载

## 懒加载

大部分情况下，我们对于懒加载的定义都是关于图片的懒加载

* 图片进行可视区之后请求图片资源加载
* 减少无效资源加载
* 如果图片的cdn和js的cdn是同一个的情况下，并发加载资源会影响js的加载

## 预加载

* 图片等静态资源在使用之前提前请求
* 资源使用到的时候能从缓存中加载

### 预加载方式
* html标签直接加载
  ```html
  <img src="..." style="display: none" />
  ```
* img对象
  ```js
  var img = new Image()
  img.src = '...'
  ```
* ajax

  这种方式可能存在跨域问题

推荐使用preloadJS库

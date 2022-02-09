# 常用面试提
####  实现跨域有哪些方案
1. jsonp
2. cors
3. node 正向代理
4. nginx反向代理
####  event-bus 类似发布订阅模式
####  前端内存处理；
1. 内存声明后期
    内存分配 变量、函数声明的时候自动分配内存
    内存使用 变量使用，函数调用的时候
    内存回收 js 自动判断回收；
2. js 中的垃圾回收机制
    + 引用技术垃圾回收 缺陷循环递归回收
    + 标记清除回收
3. js 中常见的内存泄漏
    + 全局变量用完要及时赋值为null（不会被清除调）    
    + 未被清除的定时器或者回调
    ```js
        let timer = setTimeout(()=>{

        },1000)
        clearTimeout(timer)  
    ```
    + 闭包
    + dom 的引用要及时删除
4. 如何避免内存泄漏
    1. 减少不必要的全局变量
    2. 使用完数据是及时三处引用
#### 平时工作中比较亮点的地方
    喜欢做笔记，记录自己遇到的问题并怎么一步一步解决的，下次遇到直接解决
+ 你了解浏览事件循环吗（event-loop）?
    [小龙博客]: http://122.51.157.102/post/36  'Event Loop'
+ 前端加载优化方案常用
    [页面性能检测]: https://developers.google.com/speed/pagesspeed/insights/
    + 异步加载、懒加载、预加载大文件
    + 打包压缩  gzip
    + 图片格式优化，压缩
    + 劲量减小cookie的大小
    + 服务端渲染
    + dns 预解析
    ```html
        <!-- 预解析 -->
        <link rel="dns-prefetch" href="xxxxxxx">
        <!-- 预链接 -->
        <link rel="preconnect" href="xxxxxxx">
        <!-- 预加载 -->
        <link rel="preload" as="image" href="xxxxxxx">
    ```
    + 缓存
        1. cdn cdn预热 cdn 刷新
        > cdn预热 首次发布的文件，主动从源站推送到CDN，让用户访问到CDN时不用回客户的源站命中。
        > cdn刷新 就是强制删除CDN节点缓存内容。用户请求这些资源时，CDN节点需要重新回源拉取资源，保证响应的资源与源站一致。

##### object.assige() 方法拷贝对象是对以及数据深拷贝，二级数据浅拷贝；




    
        
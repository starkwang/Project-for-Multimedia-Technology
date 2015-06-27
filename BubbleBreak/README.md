##HTML5消消看小游戏##
[点击这里查看][1]

使用的开源库有

 - [jQuery][2]
 - [fastclick.js][3]
 - [NProgress.js][4]
 - [loaders.css][5]

游戏一共4关，规则如下：

 - 连在一起且颜色一样的小球可以消去
 - 消去独立的小球扣除1000分
 - 消灭完所有的小球，进入下一关


----------
##说明##
##1、加载效果##
加载效果使用了开源的NProgress.js以及loaders.css。

加入一个遮罩层，当背景图片尚未加载完毕时遮住屏幕。

PS：校庆网站http://anniversary.fudan.edu.cn/上的加载效果也是这样实现的。

##2、同色小球查找##
这里使用了类似“路径搜索”的算法，即将小球颜色映射到一个二维数组，然后将搜索过的节点做一个标记。

搜索的同时管理一个新的二维数组，如果搜索过的节点颜色与目标颜色一致，则标记为1。

最后搜索完成，删除被标记为1的节点即可。

##3、移动端点击优化##
在移动端，点击事件存在400ms左右的延迟，导致点击体验下降。

具体参考[这篇文章][6]

这里我们使用了fastclick.js来消除这个延迟，提升移动端的点击体验。

##4、动画##
动画效果使用了jQuery原生提供的animate接口，允许异步执行动画效果，动画完成后可以执行回调函数。
 


  [1]: http://starkwang.github.io/Project-for-Multimedia-Technology/BubbleBreak/
  [2]: http://jquery.com/
  [3]: https://github.com/ftlabs/fastclick
  [4]: http://ricostacruz.com/nprogress/
  [5]: http://connoratherton.com/loaders
  [6]: http://www.linovo.me/front/webapp-300ms.html
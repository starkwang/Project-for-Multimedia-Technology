##GalleryJS图片轮播插件##

[点击这里查看demo][1]

这是一个“图片轮播”效果的插件。


----------
##使用方法##
首先将gallery.js以及它依赖的util.js引入

    <script type="text/javascript" src="gallery.js"></script>
    <script type="text/javascript" src="util.js"></script>

然后在html中加入一个div，id为gallery

    <div id="gallery"></div>

然后就可以初始化gallery

    gallery.init({
        width:"800px",
        height:"500px",
        picture:["img/1.jpg","img/2.jpg","img/3.jpg","img/4.jpg"],
        loop:true,
        timeout:4000,
        backwards:false
    })
    
    gallery.auto(); //设置自动播放




----------
##API##
##gallery.init()##

初始化gallery，使用方法如下：

    gallery.init({
        width:"800px",
        height:"500px",
        picture:["img/1.jpg","img/2.jpg","img/3.jpg","img/4.jpg"],
        loop:true,
        timeout:4000,
        backwards:false
    })

 **参数说明**
 - width 宽度
 - height 高度
 - picture 图片url
 - loop 是否循环播放
 - timeout 循环播放间隔时间（毫秒记）
 - backwards 是否逆顺序播放



----------
##gallery.auto()##
 开始自动播放，间隔为初始化时的设置值
 


----------
##gallery.turnRight()##
切换到右侧图片

----------
##gallery.turnLeft()##
切换到左侧图片


----------
##gallery.go(x)##
切换到第x张的图片


----------


 


 
  [1]: http://starkwang.github.io/Project-for-Multimedia-Technology/GalleryJS/
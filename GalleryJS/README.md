##GalleryJS图片轮播插件##

[点击这里查看demo][1]

这是一个“图片轮播”效果的插件。


----------
##使用方法##
首先将gallery.js以及它依赖的util.js引入，以及gallery.css

    <link href="gallery.css" media="all" rel="stylesheet" />

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

##浏览器支持##
由于使用了CSS3动画的特性，故只能兼容IE10以上的现代浏览器，若动画部分改用jQuery animate重写，可向下兼容到IE6。


----------
##代码文档##

这个插件的原理是在全局环境下构建一个闭包，然后把闭包内部的gallery对象暴露在全局环境中，使外部也可调用gallery对象中包含的方法，整体代码结构如下：

    (function(){    
    
        /*
            一些类方法和私有变量的实现
        */
        
        
        
        //将需要暴露的接口放入gallery对象
        gallery = {
            init : init,
            turnRight : turnRight,
            turnLeft : turnLeft,
            auto : auto,
            go : go
        }
        
        
        //将gallery对象注册到全局
        window.gallery = gallery;
    })()


**DOM操作** 
这个插件中DOM结构较为简单，所以我们直接使用了“文本插入”的方式：

    var picture_template = "<div class=\"gallery-picture\" order=\"{{order}}\" style=\"background:url({{url}});\"></div>";
    
    var buttonbox = "<div id=\"gallery-buttonbox\"><table><tbody><tr></tr></tbody></table></div>"; 
    
    var button_template = "<th><div class=\"gallery-button\" button-order=\"{{order}}\"></div></th>";
我们构建了几个DOM的模板字符串，在初始化的时候会将这些字符串用正则表达式处理后插入DOM，改变DOM结构，然后绑定事件：

    for(var i = 0 ; i < $(".gallery-button").length ; i++){
            addEvent($(".gallery-button")[i],"click",function(){
                var od = parseInt(this.getAttribute("button-order"));
                gallery.go(od);
            })
        }
**动画效果**
动画效果直接使用了CSS3动画的特性，即为DOM对象设置一个transition属性：

    .gallery-picture{
        transition:all 0.5s; //设置transition
        width: inherit;
        height: inherit;
        position: absolute;
        background-size: cover !important;
    }
transition属性允许DOM对象的CSS属性变化时，产生一个渐变动画的效果，所以我们只需要修改图片的left值，即可产生左右移动的效果。
 
  [1]: http://starkwang.github.io/Project-for-Multimedia-Technology/GalleryJS/
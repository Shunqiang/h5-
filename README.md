### 关于移动端开发问题总结

#### 1.meta基础知识
- width viewport 宽度
- initial-scale 初始缩放比例
- user-scalable 是否允许缩放

#### 2.viewport模板-通用
```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0,maximum-scale=1.0, minimum-scale=1.0, user-scalable=no">
    <meta content="yes" name="apple-mobile-web-app-capable"> //删除默认的苹果工具栏和菜单栏
    <meta content="black" name="apple-mobile-web-app-status-bar-style">  //仅针对ios的safari顶端状态条的样式
    <meta content="telephone=no" name="format-detection">  忽略将页面中的数字识别为电话号码
    <meta content="email=no" name="format-detection"> 忽略将页面中的数字识别为邮箱
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>viewport模版</title>
    <link rel="stylesheet" href="./css/style.css">
</head>

<body>
    <div>这是内容</div>
    <script src="js/index.js"></script>
</body>
</html>
```

#### 3.手机端页面自适应布局 rem布局
- 方案一： 直接引入一段js代码
```
(function (doc, win) {
        var docEl = doc.documentElement,
            resizeEvt = 'onorientationchange' in window ? 'onorientationchange' : 'resize',
            recalc = function () {
                var clientWidth = docEl.clientWidth;
                if (!clientWidth) return;
                if(clientWidth>=750){
                    docEl.style.fontSize = '100px';
                }else{
                    docEl.style.fontSize = 100 * (clientWidth / 750) + 'px';
                }
            };

        if (!doc.addEventListener) return;
        win.addEventListener(resizeEvt, recalc, false);
        doc.addEventListener('DOMContentLoaded', recalc, false);
    })(document, window);
```
> 建议页面导航采用flex布局，高度固定，宽度自适应
- 方案二： 直接在sass初始化文件中设置html的根字体大小 html{font-size:100vw/(750/100);}

#### 4.响应式页面
- Media Queries 是响应式设计的核心
> @media screen and (max-width: 980px) {html: 20px;} 
同时配合100%布局实现各种终端的响应式布局

#### 5.-webkit-overflow-scrolling:touch是什么？ 
```
MDN解释的属性值
-webkit-overflow-scrolling 属性控制元素在移动设备上是否使用滚动回弹效果.
auto: 使用普通滚动, 当手指从触摸屏上移开，滚动会立即停止。
touch: 使用具有回弹效果的滚动, 当手指从触摸屏上移开，内容会继续保持一段时间的滚动效果。继续滚动的速度和持续的时间和滚动手势的强烈程度成正比。同时也会创建一个新的堆栈上下文
```
原文链接地址[这里](https://www.cnblogs.com/xiahj/p/8036419.html)讲的很详细，原理就是使用了原生控件来实现，对于有这个属性的网页，会创建一个UIScrollView，提供layer给渲染模块使用。

#### 6.Z-index 和transform导致最大值不一定总是在上面
> 设置父级位overflow：hidden，或者3d transform变换 给元素添加 transform: translateZ(0)属性;

#### 7.移动端滚动穿透问题
> 设置遮罩背景position：fixed; 然后阻止页面默认事件；js还原滚动位置； 参考原文[这里](https://segmentfault.com/a/1190000005617307)

#### 8.WebView手势冲突(eg:轮播图滑动的时候会导致页面滚动对体验也不是很好)
> 方案1:设置document.addEventLister(’touchstart’,fn,{passive:false})；但是这样的话会直接阻止页面的左右滑动，还会阻止页面的上下滑动。
> 方案2: 未了提高用户的体验，这里做个判断，判断用户的手势是下上滑动还是向下滑动的。只有当是水平方向的才阻止事件的默认事件。 参考原文[这里](https://segmentfault.com/q/1010000002585476)

#### 9.移动端布局的时候尽量不要使用fixed布局

#### 10.写字体样式的时候要加上line-height，否则其他机型字体样式可能被截取了

#### 11.react+next.js+react-design-mobile 页面滚动时吸顶效果不能及时反应bug
之前样式
``` body{height:100%;overflow-y:auto;overflow-x:hidden```
之后样式
```body{height:100%;}``` 恢复正常（或者去掉overflow：auto）


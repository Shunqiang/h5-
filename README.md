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
- 方案二： 直接在sass初始化文件中设置html的根字体大小 html{font-size:}


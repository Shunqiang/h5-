### 关于移动端开发问题总结

#### viewport模板
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
- width viewport 宽度
- initial-scale 初始缩放比例
- user-scalable 是否允许缩放

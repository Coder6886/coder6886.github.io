---
layout:     post
title:      测试geogebra嵌入
subtitle:   
date:       2022-08-16
author:     coder6886
header-img: img/post-bg-ios9-web.jpg
catalog: true
usemathjax: true
tags:
    - 数学
---
<meta name=viewport content="width=device-width,initial-scale=1">  
<meta charset="utf-8"/>

<div id="ggb-element">
    <script src="https://www.geogebra.org/apps/deployggb.js">
        var params = {"appName": "graphing", "width": 800, "height": 600, "showToolBar": false, "showAlgebraInput": false, "showMenuBar": false };
        var applet = new GGBApplet(params, true);
        window.addEventListener("load", function() { 
            applet.inject('ggb-element');
        });
    </script>
</div> 

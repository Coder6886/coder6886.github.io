---
layout:     post
title:      geogebra嵌入流程
subtitle:   
date:       2022-08-16
author:     coder6886
header-img: img/post-bg-ios9-web.jpg
catalog: true
usemathjax: true
tags:
    - 数学
---
# 首先登录geogebra账号

# 然后在geogebra上画出你的图案

![geogebra-embed-fig1](/img/geogebra-embed-fig1.png)

# 然后将侧边栏以及底下的虚拟键盘收起。

这是一个重要步骤。

因为geogebra文件的特性是你保存时什么样，显示出来就什么样。

我们不想让看博客的人编辑侧边栏和虚拟键盘，所以就要把这两个收起来。

# 保存文件

![geogebra-embed-fig2](/img/geogebra-embed-fig2.png)

# 然后看一看地址栏目

![geogebra-embed-fig3](/img/geogebra-embed-fig3.png)

画了红框的就是你的id

# 嵌入程序

最后嵌入这样一段程序：

```html
<iframe scrolling="no" src="https://www.geogebra.org/material/iframe/id/y9xxvqpj/width/800/height/600/border/888888/smb/false/stb/false/stbh/false/ai/false/asb/false/sri/true/rc/false/ld/true/sdz/true/ctl/false" width="800" height="600"  style="border: 1px solid #e4e4e4;border-radius: 0px;" frameborder="0"></iframe>
```

其中的各种参数大家都可以改一改试一试

中间的那个`/material/iframe/id`后面跟的就是前面我说的那个id。

# 效果：

<iframe scrolling="no" src="https://www.geogebra.org/material/iframe/id/y9xxvqpj/width/800/height/600/border/888888/smb/false/stb/false/stbh/false/ai/false/asb/false/sri/true/rc/false/ld/true/sdz/true/ctl/false" width="800" height="600"  style="border: 1px solid #e4e4e4;border-radius: 0px;" frameborder="0"></iframe>
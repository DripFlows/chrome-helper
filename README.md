---
title: TS泛型积累
lang: zh-CN
author: frivolous
update: 2020/01/03
---

# 记一次谷歌浏览器截图插件开发

## 起因
因为公司有个需求，就是需要在网页上进行截图报错，既然领导任务经分配下来，那小弟当然就屁颠屁颠跑去调研了。接了任务之后，心中先预想了几种能够实现的方案。

1. 让用户用自己的截图工具（微信/qq等）截图之后提供一个上传的入口
2. 用js来做截图功能
3. 写一个截图工具

当然，身为一个前端小菜鸟，当然先去想通过前端方案去怎么实现了。第一步头脑风暴（其实是百度）了一下js怎么实现网页截图，经过头脑风暴，果然发现js本身是没有截图的api的，但是自然是难不住伟大的程序员的，看到网上其他的js截图方案，大同小异，基本都是把dom元素写入到canvas上，然后把canvas转为img，俺想，这简单啊，网上找个轮子，来自己做一下就成了，心里美滋滋的找了html2canvas插件，然后经过一番折腾之后，发现了这种方案的弊端

1. 无法截取iframe里的内容，原因是在把dom画入到canvas上的时候，js无法把iframe里的dom节点画入
2. 跨域资源图片也无法截图，原因是出于浏览器安全策略，不允许这未经许可拉取远程网站信息而导致的用户隐私泄露
3. 截图不清晰（这个点影响不算大，可以接收）

发现这个三个问题之后，回头看项目，得，这方案没法用了，项目中各种iframe嵌套（小声逼逼）。在找了下，没有找到其他更好的轮子了。于是乎，开始找产品扯皮。一顿巴拉巴拉之后（给产品洗脑安利方案一emmmmm）没成功，产品说方案一用户操作成本太高，体验不好。于是不得已抬出方案三（没做过这种插件，心里没底），然后经过一顿瞎逼分析之后，得出以下几个优劣势：

1. 需要额外的安装插件，用户的学习成本和技术支持的额外支出（就一个缺点）
2. 可拓展性强，以后还可以在此基础上拓展其它功能（可持续发展道路）
3. 可维护性，可以作为一个独立的项目
4. 逼格高（emmmm）

## 过程
既然大佬们已经定好方案了，那小弟只能撸起袖子干了。



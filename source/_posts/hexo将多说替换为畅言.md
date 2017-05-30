title: hexo将多说替换为畅言
date: 2017-05-30 10:46:11
tags: [Tools]
categories: [Tools]
reward: true
---

** 由于多说团队在2017年6月1号停止了对多说的运营，因此需要将博客中使用的多说替换为畅言。 **

### 具体替换办法如下：
1. 如果你没有畅言的账号，则首先去畅言的官网进行注册账号：
畅言网址: http://changyan.kuaizhan.com/

![](/images/reg_changyan.png)

2. 如果你已经注册过畅言的账号了，那么请直接登录即可；
3. 注册登录成功之后，点击进入后台，如图,可以看到已经有APP ID和APP KEY，这两个字符串，等会在配置的时候需要：

![](/images/login-changyan.png)

4. 由于我使用的是hexo的Yilia主题，这里以Yilia主题为主，进行下面的配置，其他主题类似。
在畅言后台找到** 安装畅言 ** 点击展开之后，点击 ** 通用代码安装 **，然后点击右边的复制代码，如图：

![](/images/copy-config.png)

5. 然后编辑你hexo目录下的themes/yilia/layout/_partial/post/duoshuo.ejs文件，将duoshuo.ejs中原来的内容全部删除，使用刚才拷贝的代码替换，替换后的样例如下：
```
<!-- 畅言评论框 start -->
<div id="SOHUCS" sid="<%=title %>" style="padding: 0px 30px 0px 46px;"></div>
<!-- 畅言评论框 end -->
<script type="text/javascript"> 
(function(){ 
var appid = '你的appid'; 
var conf = '你的app key'; 
var width = window.innerWidth || document.documentElement.clientWidth; 
if (width < 960) { 
window.document.write('<script id="changyan_mobile_js" charset="utf-8" type="text/javascript" src="https://changyan.sohu.com/upload/mobile/wap-js/changyan_mobile.js?client_id=' + appid + '&conf=' + conf + '"><\/script>'); } else { var loadJs=function(d,a){var c=document.getElementsByTagName("head")[0]||document.head||document.documentElement;var b=document.createElement("script");b.setAttribute("type","text/javascript");b.setAttribute("charset","UTF-8");b.setAttribute("src",d);if(typeof a==="function"){if(window.attachEvent){b.onreadystatechange=function(){var e=b.readyState;if(e==="loaded"||e==="complete"){b.onreadystatechange=null;a()}}}else{b.onload=a}}c.appendChild(b)};loadJs("https://changyan.sohu.com/upload/changyan.js",function(){window.changyan.api.config({appid:appid,conf:conf})}); } })(); </script>
```
6. 然后就可以使用畅言了
7. 由于我的域名已经备案，没有遇到网上说的不能正常加载畅言的方式，如果你的域名没有备案，具体Hacker方法，请参考：<http://ev1l.cn/2017/05/13/changyancrack/>

** 注意： ** 如果你在配置中还有其他问题，欢迎打赏提问，我收到之后会快速帮你解决！



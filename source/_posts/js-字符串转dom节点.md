---
title: js 字符串转dom节点
date: 2018-12-24 15:12:34
tags:
---

最近在尝试爬取一个网页的数据时，与一般的json格式活着直接返回网页不同，他请求返回的事dom字符串，偷懒先用jquey整理出来的逻辑如下：

## jquery
`function domstrToArray(str) {
    var domArr = $(str);
    var result = [];
    for(var i = 0 ; i < domArr.length; i++){
        // 用className判断是否是要拿到的节点
        if($(domArr[i]).hasClass('posttype')){
            var tmpObj = {
                'date': $(domArr[i]).find('.date').text().replace(/(^↵\s*)|(\s*$)/g, ""),
                'type': $(domArr[i]).find('.type').text().replace(/(^↵\s*)|(\s*$)/g, ""),
                'title': $(domArr[i]).find('h3').text().replace(/(^↵\s*)|(\s*$)/g, ""),
                'readCount':  $(domArr[i]).find('.cw-item-bottom').find('span:eq(0) i').text(),
                'dianzanCount': $(domArr[i]).find('.cw-item-bottom').find('span:eq(1)').text().replace('点赞', ''),
                'commentCount': $(domArr[i]).find('.cw-item-bottom').find('span:eq(2)').text().replace('评论', '')
            };
            result.push(tmpObj);
        }
    }
    return result;
}`


## 原生

### 如果将字符串转为dom节点
1. document.createRange().createContextualFragment:
   ` let frag = document.createRange().createContextualFragment('<div>One</div><div>Two</div>');
    console.log(frag);`
    
    后面查询节点的可以用：
    `let firstDiv = frag.querySelector('div');
     let allDivs = frag.querySelectorAll('div');
    `
    
2. DOMParser
    `let doc = new DOMParser().parseFromString('<div><b>Hello!</b></div>', 'text/html');`
    后面查询节点可以用：
    `let divs = doc.body.querySelectorAll('div');`

代码如下：
`function domstrToArray(str) {
    var dom = document.createRange().createContextualFragment(str);
    var domArr = dom.querySelectorAll('.posttype');
    var result = [];
    for(var i = 0 ; i < domArr.length; i++){
        var tmpObj = {
            'date': domArr[i].querySelector('.date').textContent.replace(/(^↵\s*)|(\s*$)/g, ""),
            'type': domArr[i].querySelector('.type').textContent.replace(/(^↵\s*)|(\s*$)/g, ""),
            'title': domArr[i].querySelector('h3').textContent,
            'readCount':  domArr[i].querySelectorAll('.cw-item-bottom>span')[0].textContent.replace('阅读', ''),
            'dianzanCount': domArr[i].querySelectorAll('.cw-item-bottom>span')[1].textContent.replace('点赞', ''),
            'commentCount': domArr[i].querySelectorAll('.cw-item-bottom>span')[2].textContent.replace('评论', '')
        };
        result.push(tmpObj);
    }
	return result;
}`


## python 中执行nodejs
PyExecJS

1. 安装
 pip install PyExecJS 
 
2. 调用小测试
import execjs
ctx = execjs.compile("""
   function add(x, y) {
      return x + y;
   }
""")
ctx.call("add", 1, 2)

3. 本案例
import execjs
ctx = execjs.compile("""
   function domstrToArray(str) {
    var dom = document.createRange().createContextualFragment(str);
    var domArr = dom.querySelectorAll('.posttype');
    var result = [];
    for(var i = 0 ; i < domArr.length; i++){
        var tmpObj = {
            'date': domArr[i].querySelector('.date').textContent.replace('↵', '').replace(/(^\s*)|(\s*$)/g, ""),
            'type': domArr[i].querySelector('.type').textContent.replace('↵', '').replace(/(^\s*)|(\s*$)/g, ""),
            'title': domArr[i].querySelector('h3').textContent,
            'readCount':  domArr[i].querySelectorAll('.cw-item-bottom>span')[0].textContent.replace('阅读', ''),
            'dianzanCount': domArr[i].querySelectorAll('.cw-item-bottom>span')[1].textContent.replace('点赞', ''),
            'commentCount': domArr[i].querySelectorAll('.cw-item-bottom>span')[2].textContent.replace('评论', '')
        };
        result.push(tmpObj);
    }
	return result;
}
""")
ctx.call("domstrToArray", " <li class=\"posttype clearfix por\" data-pid=\"100420545\" data-type=\"article\">\n            <div class=\"fl title\">\n                <div class=\"date\">\n                    2018-12-13 18:44                <\/div>\n                \n                                    <div class=\"type\">\n                        \u5df2\u53d1\u5e03                                            <\/div>\n                            <\/div>\n                                                    <div class=\"curp posttype-wrap \" data-href=\"http:\/\/t.10jqka.com.cn\/pid_100420545.shtml\" data-statid=\"sns_work_index.feed.article\">\n\n                <div class=\"fl content mt40\">\n                    <div class=\"cw-content-live\">\n                        <div class=\"cw-live-title fl\">\n                                                            <img class=\"articalCover\" src=\"https:\/\/u.thsi.cn\/imgsrc\/sns\/10220929f365aa8011748d5ed84908a9_667_500_small.png\" alt=\"\">\n                                                    <\/div>\n                        <div class=\"cw-live-content fl ml20\">\n                            <h3>\u9ec4\u5b8f\u98de\uff1a\u9a6c\u4e91\u90fd\u5f00\u59cb\u589e\u6301\u5f71\u89c6\u4e1a\u4e86\uff0c\u6295\u8d44\u5f71\u89c6\u80a1\u6709\u4e24\u5927\u5999\u62db\uff01<\/h3>\n                            <p>\u9a6c\u4e91\u90fd\u5f00\u59cb\u589e\u6301\u5f71\u89c6\u4e1a\u4e86\uff0c\u6295\u8d44\u5f71\u89c6\u80a1\u6709\u4e24\u5927\u5999\u62db\uff01<\/p>\n                        <\/div>\n                    <\/div>\n                    <div class=\"cw-item-bottom\">\n                        <span class=\"hotkey\" data-key=\"sns_post_100420545\"><i>0<\/i>\u9605\u8bfb<\/span>\n                        <span>23\u70b9\u8d5e<\/span>\n                        <span>1\u8bc4\u8bba<\/span>\n                    <\/div>\n                <\/div>\n            <\/div>\n            <div class=\"js-share-group poa fz12 hide\" data-valid=\"1\"><i class=\"share-group-icons cw-share-in dib\"><\/i><span>\u5206\u4eab<\/span><\/div>\n        <\/li>")


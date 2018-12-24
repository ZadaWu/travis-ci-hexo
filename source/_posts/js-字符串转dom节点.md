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


---
title: js 字符串转dom节点
date: 2018-12-24 15:12:34
tags: 前端
---

最近在尝试爬取一个网页的数据时，与一般的json格式活着直接返回网页不同，他请求返回的事dom字符串，偷懒先用jquey整理出来的逻辑如下：

## jquery

```
function domstrToArray(str) {
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
}
```


## 原生

### 如果将字符串转为dom节点
1. document.createRange().createContextualFragment:
   
```
let frag = document.createRange().createContextualFragment('<div>One</div><div>Two</div>');
```
 后面查询节点的可以用：
   

```
let firstDiv = frag.querySelector('div');
let allDivs = frag.querySelectorAll('div');
```
    
    
2. DOMParser
    
```
let doc = new DOMParser().parseFromString('<div><b>Hello!</b></div>', 'text/html');
```
    后面查询节点可以用：
    
```
let divs = doc.body.querySelectorAll('div');
```
代码如下：

```
function domstrToArray(str) {
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
}
```


## python 中执行nodejs
PyExecJS

1. 安装
 
```
pip install PyExecJS 
```
 
2. 调用小测试

```
import execjs
ctx = execjs.compile("""
   function add(x, y) {
      return x + y;
   }
""")
ctx.call("add", 1, 2)
```

3. 本案例

```
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
ctx.call("domstrToArray", eleDomStr)
```

我原以为会很顺利，但是运行下来报错：
execjs._exceptions.ProgramError: ReferenceError: document is not defined

因为execjs仅支持js运算，但是js里面的内置的document这些并不支持，所以我只能自己写个后端接口来再python中调用从而来实现这个功能。心累，想哭。

然后我用的是koa框架，用node跑接口的时候发现也是同样的报错：
 ReferenceError: document is not defined

上StackOverflow上发现：

JavaScript doesn't have a default document global. Browsers provide one, but your Node.js code doesn't run in a browser, it runs in the Node.js environment (e.g., as an application on your workstation, or as a server process, etc.).

To run the code you've shown, you'd include your .js file in a page by using a script tag in the HTML, typically at the end of body just before the closing </body> tag:

最后在同事的提示下，用了python中的BeautifulSoup库，用起来真的是6666！

Demo:
    # 通过url获取评论
    
    
```
def getCommandByUrl( pid):
        url = "http://t.10jqka.com.cn/pid_" + pid + ".shtml"

        headers = {'cache-control': 'no-cache'}

        _content = Fetcher.fetch_page_sync_get(url, headers, {},
                                               {'table': '', 'channel': ''})
        soup = BeautifulSoup(_content.text, 'html')
        for li in soup.find_all('li', class_='single-comment'):
            _tmp_comment = []
            userid = li.find_all('div', class_='commenter-name')[0].find_all('a')[0].get('href').split('/')[3]
            username = li.find_all('div', class_='commenter-name')[0].get_text().lstrip().rstrip()
            date = li.find_all('span', class_='comment-time')[0].get_text().lstrip().rstrip()
            text = li.find_all('div', class_='comment-text')[0].get_text().lstrip().rstrip()
            comment_order = li.find_all('span', class_='comment-order')[0].get_text().lstrip().rstrip()
            reply_count = len(li.find_all('div', class_='existed-reply-container'))
            _tmp_comment.append(userid)
            _tmp_comment.append(username)
            _tmp_comment.append(text)
            _tmp_comment.append(date)
            _tmp_comment.append(comment_order)
            _tmp_comment.append(reply_count)
            _tmp_comment.append(pid)
            self._db_table_datas['values'].append(_tmp_comment)
        pass
        
```



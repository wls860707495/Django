# django表单
## 表单流程
当打开网页时  
```
如：127.0.0.1：8000/search
```
网页表单代码为  
```
    <form action="/search" method="get">
        <input type="text" name="q">
        <input type="submit" value="搜索">
    </form>
```
1、django会去urls.py(url(r'^search$', search.search),)中寻找r'^search$'  
2、调用search.search方法进行方法调用，sear函数的代码如下  
```
def search(request):
    request.encoding = 'utf-8'
    if 'q' in request.GET:
        message = '你搜索的内容为: ' + request.GET['q']
    else:
        message = '你提交了空表单'
    return HttpResponse(message)
```
根据name‘q’的值的不同显示HttpResponse中的信息

## 表单为post时需要注意的地方
当使用post进行表单提交及传值时，html中的post表单中必须加入{%csrf_token%}标签。这是Django提供的防止伪装提交请求的功能。POST 方法提交的表格，必须有此标签。其实例代码如下：
```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>菜鸟教程(runoob.com)</title>
</head>
<body>
    <form action="/search-post" method="post">
        {% csrf_token %}
        <input type="text" name="q">
        <input type="submit" value="Submit">
    </form>
 
    <p>{{ rlt }}</p>
</body>
</html>
```
这其中{{rlt}}记号，是为表格处理结果预留位置。

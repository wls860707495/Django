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

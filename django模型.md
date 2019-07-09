# Django模型
在python中定义数据库先定义模型，在models中可直接创建数据库表，需在setting中的InterlizeApp中初始化模型，才能使用。  
```
eg:  
1、django-admin startapp TestModel //在项目运行此语句为创建TestModel模型
2、
from django.db import models                      //此处为在新建的模型TestModel中编写的创建表的代码

# Create your models here.
class Test(models.Model):
    name = models.CharField(max_length=20, blank=True, null=True)

    class Meta:
        db_table = "tesang"            
3、 在工程的settings文件中的INSTALLED_APPS中初始化并建立模型
4、$python manage.py makemigrations TestModel                   //执行以下命令来创建模型表
   $python manage.py migrate TestModel

```

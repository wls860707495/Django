# python常用函数及基础语法
## mean函数
mean()：取平均值   
```
设数据x=np.array([1,2,3],[2,3,4],[3,4,5],[4,5,6])
num1 = np.mat(x)                    //其中np指的是numpy，而mat更类似于matlab中，更适用于矩阵的计算。
np.mean(num1)          //对所有元素取平均值
np.mean(now2,0)    //压缩行，对各列求平均值
np.mean(now2,1)    //压缩列，对各行求平均值
```
## 标识符
其但下划线表示不能直接访问的类的属性，需通过类提供的接口进行访问，不能用 from xxx import * 而导入。  
以双下划线开头的 __foo 代表类的私有成员，以双下划线开头和结尾的 __foo__ 代表 Python 里特殊方法专用的标识，如 __init__() 代表类的构造函数。  
## 注释
多行注释使用三个单引号(''')或三个双引号(""")   
## 标准数据类型
```

    Numbers（数字）
    String（字符串）
    List（列表）
    Tuple（元组）
    Dictionary（字典）

```
如果你要实现从字符串中获取一段子字符串的话，可以使用 [头下标:尾下标] 来截取相应的字符串，其中下标是从 0 开始算起，可以是正数或负数，下标可以为空表示取到头或尾。[头下标:尾下标] 获取的子字符串包含头下标的字符，但不包含尾下标的字符。  
```
eg:

```
## python列表
初始化:list = []
常用的列表截取与字符串等一致，即还是list[x:x];   
常用函数：--->此处源码均需看，后加   
```
list.append(obj):在列表末尾添加新的对象
list.count(obj):统计某个元素在列表中出现的次数
list.extend(seq):在列表末尾一次性追加另一个序列中的多个值（用新列表扩展原来的列表）
list.index(obj):从列表中找出某一个值第一个匹配项的索引值
list.insert(index ,obj):将对象插入列表
list.pop([index=-1]):移除列表中的一个元素（默认最后一个元素），并返回该元素的值
list.remove(obj):移除列表中某个值的第一个匹配项
list.reverse():逆置列表中的元素
list.sort(cmp=None,key=None,reverse=False):对原列表进行排序
```
python中的self相当于this指针  
## super()函数
主要是解决多继承问题以及，一旦涉及到多继承，那么就会涉及到调用顺序的问题以及重复调用的问题，使用super()函数可以很好的避免这些问题。下面为菱形调用例子：    
```
class A():
    def __init__(self):
        print('enter A')
        print('leave A')


class B(A):
    def __init__(self):
        print('enter B')
        super().__init__()
        print('leave B')


class C(A):
    def __init__(self):
        print('enter C')
        super().__init__()
        print('leave C')


class D(B, C):
    def __init__(self):
        print('enter D')
        super().__init__()
        print('leave D')


d = D()


运行实例：
enter D
enter B
enter C
enter A
leave A
leave C
leave B
leave D
```
## 元组
元组类似于列表，使用（）进行标识，但元组不能进行二次赋值，仅仅只是只读列表。
## 字典
字典是无序的对象集合。其与列表两者之间的区别在于：字典当中的元素是通过键来存取的，而不是通过偏移存取。  
字典用"{}"标识。字典由索引(key)和它对应的值value组成。Java中的哈希表。
```
eg:tinydict = {'name': 'john','code':6734, 'dept': 'sales'}
 print tinydicr['name']
 结果为 john
```







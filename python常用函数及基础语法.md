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
## 需要注意的运算符
```
**  返回x的y次幂
//  返回商的整数部分(向下取整)
<>  判断两个对象是否不相等
and   x and y   如果 x 为 False，x and y 返回 False，否则它返回 y 的计算值 
or    x or y   如果 x 是非 0，它返回 x 的值，否则它返回 y 的计算值
not   not x   如果 x 为 True，返回 False 。如果 x 为 False，它返回 True
\  转义运算符
*  可用做重复输出运算符
```
## 循环
while: 用于循环执行程序，即在某条件下，循环执行某段程序，以处理需要重复处理的相同任务。  
for  :  for循环可以遍历任何序列的项目，如一个列表或者一个字符串
```
eg1：
for letter in 'Python':     # 第一个实例
   print '当前字母 :', letter

结果：
      当前字母 : P
      当前字母 : y
      当前字母 : t
      当前字母 : h
      当前字母 : o
      当前字母 : n
eg2:
fruits = ['banana', 'apple',  'mango']
for index in range(len(fruits)):
   print '当前水果 :', fruits[index]
   
结果:
      当前水果 : banana
      当前水果 : apple
      当前水果 : mango

```
## python中可变与不可变对象
```
eg1:
    def ChangeInt(a):
       a = 10
       return  a
    b = 2
    ChangeInt(b)
    print(b)  # 结果是 2
eg2:
    def ChangeInt(a):
       a = 10
       return  a
    b = 2
    a = ChangeInt(b)
    print(a)  # 结果是 10  
```
即python中a、b这些符号仅是有着类似于指针的作用，指向‘=’右侧创建的对象。  
对于可变与不可变类型的传参：
```
    不可变类型：类似 c++ 的值传递，如 整数、字符串、元组。如fun（a），传递的只是a的值，没有影响a对象本身。比如在 fun（a）内部修改 a 的值，只是修改另一个复制的对象，不会影响 a 本身。

    可变类型：类似 c++ 的引用传递，如 列表，字典。如 fun（la），则是将 la 真正的传过去，修改后fun外部的la也会受影响
```
## python中range()函数
python range() 函数可创建一个整数列表，一般用在 for 循环中。 
range(start, stop[, step])此处为range()函数的用法。 
```
    start: 计数从 start 开始。默认是从 0 开始。例如range（5）等价于range（0， 5）;  
    stop: 计数到 stop 结束，但不包括 stop。例如：range（0， 5） 是[0, 1, 2, 3, 4]没有5  
    step：步长，默认为1。例如：range（0， 5） 等价于 range(0, 5, 1)  
```
下面为实例
```
eg1:
    range(0, 10, 3)  # 步长为 3
   结果：
        [0, 3, 6, 9]
        
eg2:
    x = 'runoob'
    for i in range(len(x)) :
       print(x[i])

    结果：
         r
         u
         n
         o
         o
         b
```
对于python中的函数,若其属性值里有self，那么调用其自身函数时需要前面加self.来调用，如：
```
eg:
   def x(self,n):
      if n>0:
         self.x(n-1)
```
## python文件I/O
### open函数
```
eg:
  file object = open(file_name [, access_mode][, buffering])
参数含义：  
  file_name：file_name变量是一个包含了你要访问的文件名称的字符串值。
  access_mode：access_mode决定了打开文件的模式：只读，写入，追加等。所有可取值见如下的完全列表。这个参数是非强制的，默认文件访问模式为只读(r)。
  buffering:如果buffering的值被设为0，就不会有寄存。如果buffering的值取1，访问文件时会寄存行。如果将buffering的值设为大于1的整数，表明了这就是的寄存区的缓冲大小。如果取负值，寄存区的缓冲大小则为系统默认。
```
### write()方法
```
    fo = open("foo.txt", "w")
    fo.write( "www.runoob.com!\nVery good site!\n")
 
    # 关闭打开的文件
    fo.close()
    
文件内容显示：
    $ cat foo.txt 
    www.runoob.com!
    Very good site!
```


# Python多线程
## 两种创建方式
### 函数式：调用thread模块中的start_new_thread()函数来产生新线程
```
            thread.start_new_thread ( function, args[, kwargs] )
```
其中，function --> 线程函数;args --> 传递给线程函数的参数，他必须是个tuple（元组）类型;kwargs --> 可选参数。  
下为实例：  
```
import _thread
import time



def print_time(threadname,delay):
    count = 0
    while count < 5:
        time.sleep(delay)
        count += 1
        print ("%s: %s" % (threadname,time.ctime(time.time())))

try:
    _thread.start_new_thread(print_time,("Thread-1",2,))
    _thread.start_new_thread( print_time, ("Thread-2", 4, ) )
except:
    print("Error: unable to start thread")
while 1:
    pass

```
### Threading模块
Threading模块创建线程，会直接从threading.Thread继承，然后重写__init__方法和run方法:
```
import threading
import time

exitFlag = 0


class myThread(threading.Thread):  # 继承父类threading.Thread
    def __init__(self, threadID, name, counter):
        threading.Thread.__init__(self)
        self.threadID = threadID
        self.name = name
        self.counter = counter

    def run(self):  # 把要执行的代码写到run函数里面 线程在创建后会直接运行run函数
        print("Starting " + self.name)
        print_time(self.name, self.counter, 5)
        print( "Exiting " + self.name)

def print_time(threadName, delay, counter):
    while counter:
        if exitFlag:
            (threading.Thread).exit()
        time.sleep(delay)
        print("%s: %s" % (threadName, time.ctime(time.time())))
        counter -= 1


# 创建新线程
thread1 = myThread(1, "Thread-1", 1)
thread2 = myThread(2, "Thread-2", 2)

# 开启线程
thread1.start()
thread2.start()

print("Exiting Main Thread")
```
## 线程同步
对线程的执行顺序进行限制，例如：防止多个线程对同一个数据进行修改时出现错误。
```
import threading
import time
 
class myThread (threading.Thread):
    def __init__(self, threadID, name, counter):
        threading.Thread.__init__(self)
        self.threadID = threadID
        self.name = name
        self.counter = counter
    def run(self):
        print "Starting " + self.name
       # 获得锁，成功获得锁定后返回True
       # 可选的timeout参数不填时将一直阻塞直到获得锁定
       # 否则超时后将返回False
        threadLock.acquire()
        print_time(self.name, self.counter, 3)
        # 释放锁
        threadLock.release()
 
def print_time(threadName, delay, counter):
    while counter:
        time.sleep(delay)
        print "%s: %s" % (threadName, time.ctime(time.time()))
        counter -= 1
 
threadLock = threading.Lock()
threads = []
 
# 创建新线程
thread1 = myThread(1, "Thread-1", 1)
thread2 = myThread(2, "Thread-2", 2)
 
# 开启新线程
thread1.start()
thread2.start()
 
# 添加线程到线程列表
threads.append(thread1)
threads.append(thread2)
 
# 等待所有线程完成
for t in threads:
    t.join()
print "Exiting Main Thread"
```
对于join()方法可以防止主线程结束后会强行关闭子线程。在python中一般情况下主线程执行完毕后子线程会继续执行。
### 线程优先级队列（Queue）
Queue模块中的常用方法:
```
  Queue.qsize() 返回队列的大小
  Queue.empty() 如果队列为空，返回True,反之False
  Queue.full() 如果队列满了，返回True,反之False
  Queue.full 与 maxsize 大小对应
  Queue.get([block[, timeout]])获取队列，timeout等待时间
  Queue.get_nowait() 相当Queue.get(False)
  Queue.put(item) 写入队列，timeout等待时间
  Queue.put_nowait(item) 相当Queue.put(item, False)
  Queue.task_done() 在完成一项工作之后，Queue.task_done()函数向任务已经完成的队列发送一个信号
  Queue.join() 实际上意味着等到队列为空，再执行别的操作
```
实例：
```
import queue
import threading
import time

exitFlag = 0

class myThread(threading.Thread):
    def __init__(self, threadID, name, q):
        threading.Thread.__init__(self)
        self.threadID = threadID
        self.name = name
        self.q = q

    def run(self):
        print("Starting " + self.name)
        process_data(self.name, self.q)
        print("Exiting " + self.name)

def process_data(threadName, q):
    while not exitFlag:
        queueLock.acquire()
        if not workQueue.empty():
            data = q.get()
            queueLock.release()
            print("%s processing %s" % (threadName, data))
        else:
            queueLock.release()
        time.sleep(1)

threadList = ["Thread-1", "Thread-2", "Thread-3"]
nameList = ["One", "Two", "Three", "Four", "Five"]
queueLock = threading.Lock()
workQueue = queue.Queue(10)
threads = []
threadID = 1

# 创建新线程
for tName in threadList:
    thread = myThread(threadID, tName, workQueue)
    thread.start()
    threads.append(thread)
    threadID += 1

# 填充队列
queueLock.acquire()
for word in nameList:
    workQueue.put(word)
queueLock.release()

# 等待队列清空
while not workQueue.empty():
    pass

# 通知线程是时候退出
exitFlag = 1

# 等待所有线程完成
for t in threads:
    t.join()
print("Exiting Main Thread")

```
## 注
python中的多线程因为GIL锁实际每次只能有一个核在执行python代码，不能像java那样执行多线程。



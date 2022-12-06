---
layout: post
title: python 多线程与多进程
tag: [python, 多线程,多进程]
author: Ranok
color: brown
permalink: process
# thumbnail: "assets/img/thumbnails/feature-img/openstack.png"
---

进程是计算机中的程序关于某数据集合上的一次运行活动，是系统进行资源分配和调度的基本单位，是操作系统结构的基础。线程是进程中的一部分，也是进程的的实际运作单位，它也是操作系统中的最小运算调度单位。

---
## 前言
多线程与多进程还是比较实用的。本博客以应用为目的展示两个基础的类。

## 多进程 Process

process模块是一个创建进程的模块，借助这个模块，就可以完成进程的创建。<br>
```python
from multiprocessing import Process
```
#### 参数介绍
```python
Process(group=None, target=None, name=None, args=(), kwargs={})
```

1. `group`——参数未使用，值始终为`None`
2. `target`——表示调用对象，即子进程要执行的任务
3. `args`——表示调用对象的位置参数元组，args=(1,2,'egon',)
4. `kwargs`——表示调用对象的字典，kwargs={'name':'egon','age':18}
5. `name`——为子进程的名称

#### 方法介绍
1. `obj.start()`：启动进程，并调用该子进程中的obj.run()
2. `obj.run()`：进程启动时运行的方法，正是它去调用target指定的函数，我们自定义类的类中一定要实现该方法
3. `obj.terminate()`：强制终止进程obj，不会进行任何清理操作，如果obj创建了子进程，该子进程就成了僵尸进程，使用该方法需要特别小心这种情况。如果obj还保存了一个锁那么也将不会被释放，进而导致死锁
4. `obj.is_alive()`：如果obj仍然运行，返回`True`
5. `obj.join([timeout])`：主线程等待obj终止（强调：是主线程处于等的状态，而obj是处于运行的状态）。`timeout`是可选的超时时间，需要强调的是，obj.join只能join住start开启的进程，而不能join住run开启的进程

#### 属性介绍
1. `obj.daemon`：默认值为False，如果设为True，代表obj为后台运行的守护进程，当obj的父进程终止时，obj也随之终止，并且设定为True后，obj不能创建自己的新进程，必须在
2. `obj.start()`：之前设置
3. `obj.name`：进程的名称
4. `obj.pid`：进程的`pid`
5. `obj.exitcode`：进程在运行时为`None`、如果为–N，表示被信号N结束(了解即可)
6. `obj.authkey`：进程的身份验证键,默认是由`os.urandom()`随机生成的32字符的字符串。这个键的用途是为涉及网络连接的底层进程间通信提供安全性，这类连接只有在具有相同的身份验证键时才能成功（了解即可）

#### 使用案例
```python
from multiprocessing import Process
import os

def worker(arg):
    # 返回父子进程的pid
    print(os.getpid(), os.getppid())


if __name__ == "__main__":
    print('I am parent process')
    jobs = []
    for i in range(5):
        p = Process(target=worker, args=(i,))
        jobs.append(p)
        p.start()
```
#### 方法介绍

{% include aligner.html images="blog-img/process/threading.png" column=1 %}

#### 使用样例
##### 利用函数使用多线程
```python
from threading import Thread
a = 0
def work():
    global a
    a += 1
    print(a，end=’’)

if __name__ == '__main__':
    childs = []
    for i in range(5):
        childs.append(Thread(target=work))
        childs[-1].start()
```

程序运行结果：<br>
`1 2 3 4 5`<br>
如果创建的不是线程而是进程则资源不会共享，运行结果会是：<br>
`1 1 1 1 1`

##### 利用类重写Thrrad方法实现多线程
```python
from threading import Thread
import time
num = 0
childs = []
class MyThread(Thread):
    def run(self):
        self.t = num

        for _ in range(3):
            print(self.t, '线程正在工作')
            time.sleep(0.5)


for i in range(3):
    num = i + 1
    childs.append(MyThread())
    childs[-1].start()
```
运行结果之一：<br>
1 线程正在工作<br>
2 线程正在工作<br>
3 线程正在工作<br>
132 线程正在工作 线程正在工作 <br>
线程正在工作<br>
<br>
13 线程正在工作<br>
2 线程正在工作<br>
 线程正在工作<br>

可以看到输出**十分的杂乱**，说明确实是多线程输出。

#  第一章 Python介绍与安装

##  01 Python语言的特点

* Python语言的特点
  * 语法简单
  * 类库丰富
  * 开放源码
  * 可扩展
  * 跨平台

##  02 Python的发展历史与版本

* Python历史版本
  * 1990年Python诞生
  * 2000年Python2.0发布
  * 2008年Python3.0发布
  * 2010年Python2.7发布（最后一个2.x版本）
* 相关网站
  * 官方版本：https://www.python.org
  * 发行版本：Anaconda
    * 官网地址：https://www.anaconda.com/download
    * 清华大学镜像：https://mirror.tuna.tsinghua.edu.cn/help/anaconda
* 学习Python的利器
  * Python的官方文档
  * iPython
  * jupyter notebook
  * Sublime Text 
  * pyCharm
  * Pip

##  03 Python的安装

* Mac系统安装Python
  * 官方网站下载程序
  * 双击下一步，根据提示继续安装
* Mac系统安装pyCharm
  * 官方网站下载（收费版|免费社区版），学习下载免费版即可
  * 双击安装

#  第二章 Python的基础语法

##  04 Python程序的书写规则

* 注释：以#号开头
* 导入模块：使用import关键字
* Python的缩进

##  05 基础数据类型

*  数据类型
  * 整数（int）8
  * 浮点数（float）8.8
  * 字符串（str）"8" "你好"
  * 布尔值（bool）True False
* 判断数据类型
  * type('8') 
  * type(8.8)
  * type(8)
  * type(True)
* 数据类型转换
  * int("9")
  * str(9)

##  06 变量定义和常用操作

* 案例网络带宽计算器
  * byte：计算机存储数据的单位
  * bit：线路速速计算单位
* 变量 a = 123
  * "a"为变量名称
  * “=” 为变量赋值
  * “123” 为变量的得到的值
* 变量的命名：临时变量：单独的一个字母；
  * 字母和下划线开头，中间可以是字母，数字，下划线

#  第三章 序列

##  07 序列的概念

* 序列：是指他的成员嗾使有序排列的，可以通过下标偏移量访问到他的一个或几个成员，字符串、列表、元组都属于序列。
  * 字符串:"12qwer"
  * 列表:[12,12,34]
  * 元组:(12,123,90)

## 08 字符串的定义和使用

* 定义：str = "qwerty"

## 09 字符串的常用操作

* 序列的基本操作
  * 成员关系操作符(in、not in)： 对象 [not] in 序列
  * 连接操作符（+）：序列+ 序列
  * 重复操作符（/*/）：序列 * 整数
  * 切片操作符（[:]）：序列[0：整数]

##  10 元组的定义和常用操作

* 定义：("天蝎座","天秤座")
* 元组的嵌套
* 元组与列表的区别：
  * 元组使用()号，列表使用[]号
  * 元组中元素不可以变更，列表中元素可以变更

##  11 列表的定义和常用操作

* 列表
  * 可以进行修改
  * 使用append方法添加元素

#  第四章 条件与循环

##  12 条件语句

* 条件语句：if
  * 关键字
  * 判断条件表达式
  * 判断为真实执行代码块

~~~python
if 表达式:
	代码块
elif 表达式：
	代码块
else:
    代码块
~~~

## 13 for循环

* 循环语句

~~~~Python
for 迭代变量 in 可迭代对象
	代码块
    
for i in range(1,10)
	print(i)
~~~~

##  14 while循环

* 循环语句
  * 通常情况与if语句配合使用

~~~Python
while True
	代码块
    break
~~~

##  15 for循环中的if嵌套

```python
for i in range(1,10):
    if i == 9:
        print(i)
        break
```

##  16 while循环中的if嵌套

```python
n = 0
while i < 9:
    n += 1
print(n)
```

#  第五章 映射与字典

##  17 字典的定义与常用操作

* 映射的类型：字典

  * 字典包含哈希值和指向的对象
  * {"哈希值":"对象"}

* 字典操作

  ~~~python
  # 定义字典
  dick = {"x":1,"y":2}
  # 字典添加值
  dick["z"] = 3
  ~~~

## 18 列表推导式与字典推导式

* 列表推导式

  * ```python
    [i + 1 for i in range(0,19)]
    ```

* 字典推导式

  * ~~~python
    {i: 0 for i in range(0, 10)}
    ~~~

#  第六章 文件与输出

##  19 文件的内建函数

* 文件内建函数和方法
  * open() 打开文件
  * read() 输入
  * readline() 输入一行
  * seek() 文件内移动
  * write() 输出
  * close() 关闭文件 

示例代码：

~~~python
# 文件操作
file = open("text.txt", "w")
file.write("你好时间")
file.close()

# 文件读取
filer = open("text.txt")
print(filer.read())
filer.close()
~~~

##  20 文件的常用操作

* 文件的常用操作
  * 读取一行
  * 读取多行
  * 文件内移动

示例代码：

~~~python
# 读取一行
file = open("text.txt")
print(file.readline())
file.close()
# 读取多行
files = open("text.txt")
for line in files.readlines():
    print(line)
files.close()
# 控制文件内指针位置
file = open("text.txt")
print(file.tell())
print(file.readline(1))
print(file.tell())

file.seek(0)
print(file.tell())
print(file.readline())
print(file.tell())
~~~

#  第七章 错误与异常

##  21 异常的检测与处理

* 错误 不等于 异常

  * 异常是在出现错误是采用正常控制流以外的动作
  * 异常的处理一般是：检测到错误，引发异常；对异常进行捕获操作

* ~~~~python
  try:
  <检测异常>
  except Exception[]:
  <异常处理码>
  finally:
  ~~~~

示例代码：

~~~python
# 异常
try:
    year = int(input("输入年份"))
except ValueError as e:
    print("输入年份异常 %s" + str(e))
finally:
    print("无论是否成功，都执行")
~~~

#  第八章 函数

##  22 函数的定义与常用操作

* 函数：是对程序逻辑进行机构化的一种编程方法

  * 函数定义

    * ~~~python
      def 函数名称():
          代码
          return 需要返回的内容
      ~~~

  * 函数调用

    * ~~~
      函数名称()
      ~~~

##  23 函数的可变长参数

~~~python
# 可变长参数
def test(first, *other):
    print(first + len(other))


test(12, 13, 14)
~~~

##  24 函数的变量作用域

~~~python
# 变量的作用域

var1 = 123


def func():
    var1 = 456
    print(var1)


func()
print(var1)
~~~

##  25 函数的迭代器与生成器

~~~python
# 函数迭代器和生成器
list = [1, 2, 3, 4, 5]
it = iter(list)
print(next(it))

for i in range(10, 20, 4):
    print(i)
    
def ferange(start, stop, step):
    x = start
    while x <= stop:
        # 生成器
        yield x
        x += step


for i in ferange(10, 20, 0.5):
    print(i)
~~~

##  26 lambda表达式

~~~python
# 普通函数
def add(x, y):
    return x + y


print(add(3, 5))
#lambda表达式
add2 = lambda x, y: x + y

print(add2(1, 2))
~~~

##  27 Python的内建函数

~~~~python
# 内建函数
# filter函数
a = [1, 2, 3, 4, 5]
print(list(filter(lambda x: x > 2, a)))
# map函数
b = [1, 2, 3, 4]
c = [5, 6, 7, 8]
print(list(map(lambda x, y: x + y, b, c)))
# reduce函数
from functools import reduce

print(reduce(lambda x, y: x + y, [1, 2, 3, 4], 10))
# zip函数
for i in zip([1, 2, 3], [4, 5, 6]):
    print(i)

dicta = {"a": "b", "c": "d"}
dicta1 = zip(dicta.values(), dicta.keys())
print(dict(dicta1))
~~~~

##  28 闭包的定义

 ~~~python
def sum(a):
    def add(b):
        return a + b

    return add


num1 = sum(2)
print(type(num1))
print(num1(4))
 ~~~

##  29 闭包的使用

~~~~python
def a_line(a, b):
    def arg_y(x):
        return a * x + b

    return arg_y


line = a_line(2, 3)
for i in range(1, 4):
    print(line(i))
~~~~

## 30 装饰器的定义

~~~python
import time


def timmer(func):
    def wapper():
        startTime = time.time()
        func()
        endTime = time.time()
        print("运行了 %s 秒" % (endTime - startTime))

    return wapper


@timmer
def i_can_sleep():
    time.sleep(3)


i_can_sleep()
~~~

##  31 装饰器的使用

~~~~python
def new_tips(st):
    def tips(func):
        def wapper(a, b):
            print(st)
            print("start %s" % func.__name__)
            func(a, b)
            print("stop")

        return wapper

    return tips


@new_tips("add")
def add(a, b):
    return a + b


@new_tips("sub")
def sub(a, b):
    return a - b


add(1, 2)
sub(3, 2)
~~~~

##  32 自定义上下文管理器

* 上下文管理器

~~~~python
with open("text.txt") as f:
    for line in f:
        print(line)
~~~~

# 第九章 模块

##  33 模块的定义

* 模块是在代码量变得相当大之后，为了将需要重复使用的又组织的代码放在一起，这部分代码可以附加到现有的程序中，附加的过程叫做导入（import）

  * ~~~
    import 模块名称
    from 模块名称 import 方法名
    ~~~

#  第十章 语法规范

##  34 PEP8编码规范

~~~
The Zen of Python, by Tim Peters
Beautiful is better than ugly.
Explicit is better than implicit.
Simple is better than complex.
Complex is better than complicated.
Flat is better than nested.
Sparse is better than dense.
Readability counts.
Special cases aren't special enough to break the rules.
Although practicality beats purity.
Errors should never pass silently.
Unless explicitly silenced.
In the face of ambiguity, refuse the temptation to guess.
There should be one-- and preferably only one --obvious way to do it.
Although that way may not be obvious at first unless you're Dutch.
Now is better than never.
Although never is often better than *right* now.
If the implementation is hard to explain, it's a bad idea.
If the implementation is easy to explain, it may be a good idea.
Namespaces are one honking great idea -- let's do more of those!
~~~

#  第十一章 面向对象编程

##  35 类与实例

~~~python
class User():
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def print_role(self):
        print("%s ： %s" % (self.name, self.age))


user1 = User("jack", "14")
user2 = User("tom", 20)

user1.print_role()
user2.print_role()
~~~

##  36 如何增加类的属性和方法

~~~~python
class User():
    def __init__(self, name, age, sex):
        self.__name = name  # 变量是属性
        self.age = age
        self.sex = sex

    def print_role(self):
        # 函数是方法
        print("%s %s %s" % (self.__name, self.age, self.sex))

    def updateName(self, newName):
        self.name = newName


class Monster():
    pass


user1 = User("jack", "14", "男")
user2 = User("tom", 20, "女")

user1.print_role()
user2.print_role()
user1.updateName("pony")
user1.print_role()
~~~~

##  37 类的继承

~~~python
class Monster():
    def __init__(self, hp=100):
        self.hp = hp

    def run(self):
        print("移动到一个位置")

    def who(self):
        print("我是父类")


class Animels(Monster):
    def __init__(self, hp=10):
        super().__init__(hp)


class Boss(Monster):
    def __init__(self, hp=1000):
        super().__init__(hp)

    def who(self):
        print("我是子类")


ani = Animels()
print(ani.hp)
ani.run()

boss = Boss()
boss.who()

print(type(a1))
print(type(ani))
print(type(boss))

print(isinstance(a1, Monster))
~~~



## 38 类的使用-自定义with语句

~~~python
class TestWith():
    def __enter__(self):
        print("开始运行")

    def __exit__(self, exc_type, exc_val, exc_tb):
        if exc_tb is None:
            print("end1")
        else:
            print("is %s" % exc_tb)


with TestWith():
    raise NameError("name错误")
~~~

#  第十二章 多线程编程

##  39 多线程编程的定义

~~~python
import threading
import time
from threading import current_thread


def myThread(arg1, arg2):
    print(current_thread().getName(), "start")
    print("%s %s" % (arg1, arg2))
    time.sleep(1)
    print(current_thread().getName(), "stop")


for i in range(1, 10, 1):
    t = threading.Thread(target=myThread, args=(i, i + 1))
    t.start()

print(current_thread().getName(), "end")
~~~

~~~python
class MyThread(threading.Thread):
    def run(self):
        print(current_thread().getName(), "start")
        print("run")
        print(current_thread().getName(), "stop")


t1 = MyThread()
t1.start()
t1.join()
~~~



##  40 经典的生产者与消费者问题

~~~~python
from threading import Thread,current_thread
import time
import random
from queue import Queue

queue = Queue(5)

class ProducerThread(Thread):
    def run(self):
        name = current_thread().getName()
        nums = range(100)
        global queue
        while True:
            num = random.choice(nums)
            queue.put(num)
            print('生产者 %s 生产了数据 %s' %(name, num))
            t = random.randint(1,3)
            time.sleep(t)
            print('生产者 %s 睡眠了 %s 秒' %(name, t))

class ConsumerTheard(Thread):
    def run(self):
        name = current_thread().getName()
        global queue
        while True:
            num = queue.get()
            queue.task_done()
            print('消费者 %s 消耗了数据 %s' %(name, num))
            t = random.randint(1,5)
            time.sleep(t)
            print('消费者 %s 睡眠了 %s 秒' % (name, t))


p1 = ProducerThread(name = 'p1')
p1.start()
p2 = ProducerThread(name = 'p2')
p2.start()
p3 = ProducerThread(name = 'p3')
p3.start()
c1 = ConsumerTheard(name = 'c1')
c1.start()
c2 = ConsumerTheard(name = 'c2')
c2.start()
~~~~



#  第十三章 标准库

##  41 Python标准库的定义

* 通过Python的官方网站查看

##  42 正则表达式库re

* 文字的处理功能re

~~~Python
import re

p = re.compile("a")
print(p.match("b"))
~~~

##  43 正则表达式的元字符



##  44 正则表达式分组功能实例



##  45 正则表达式库函数match与search的区别



##  46 正则表达式库替换函数sub()的实例



##  47 日期与时间函数库



##  48 数学相关库



##  49 使用文件行对文件和文件夹操作



##  50 文件夹操作库os.path



#  第十四章 机器学习

##  51 机器学习的一般流程与Numpy安装



##  52 Numpy的数组与数据类型



##  53 Numpy的数据和标量的计算



##  54 Numpy数组的索引与切片



##  55 Pandas安装与Series结构



##  56 Series的基本操作



##  57 Dataframe的基本操作



##  58 层次化索引



##  59 Matplotlib的安装与绘图



##  60 机器学习分类原理



##  61 Tensorflow的安装



##  62 根据特征分类的模型和代码



#  第十五章 爬虫

##  63 网页数据的采集与urllib库



##  64 网页常见的两种请求方式get和post



##  65 http头部信息模拟



##  66 requests库额基本使用



##  67 结合正则表达式爬取图片连接



##  68 BeautifulSoup的安装与使用



##  69 使用爬虫爬取新闻网站



##  70 使用爬虫爬取图片链接并下载图片



#  第十六章 综合案例

 ##  71 如何分析源代码并设计合理的代码结构


---
title: python 基础知识
date: 2024-09-01 12:01:51
tags:
    - 机器学习
comments: true
top_img: py基础/img1.png
cover: py基础/img1.png
---

![alt text](py基础/img1.png)

## 基础知识
### 运算和循环
1）这里使用：莫烦python学习：https://mofanpy.com/tutorials/python-basic/interactive-python/

2）运算

| +    | 加     | 3+4=7     |
| :--- | ------ | --------- |
| -    | 减     | 3-4=-1    |
| *    | 乘     | 3*4=12    |
| /    | 除     | 3/2=1.5   |
| %    | 取模   | 103%100=3 |
| **   | 幂     | 3**2=9    |
| //   | 取整除 | 10//3=3   |

3）条件判断

```py
today = 4
if today == 1:
    print("周一")
elif today == 2:
    print("周二")
elif today == 3:
    print("周三")
else:
    print("周一周二周三之外的一天")
```

4）for和while循环

| for   | 天然适合在有限的循环中 |
| ----- | ---------------------- |
| while | 可以被用在无限循环中   |

```py
# range(3, 10, 2) 表示3开始，到10之前，每2次出一次数。
for i in range(3, 10, 2):
    print("新文件-" + str(i))
```

| break    | 紧急弹出       |
| -------- | -------------- |
| continue | 算了，我接着来 |

```py
count = 0
guess_num = 10
while guess_num != 20:
    guess_num += 1
    count += 1
    if count > 10:
        break
    print(guess_num)
```

```py
for i in range(10):
    if i % 2 == 0:
        continue    # 跳过偶数
    print(i)
```

### 数据类型

* list列表

  ```py
  files = ["f1.txt", "f2.txt", "f3.txt", "f4.txt", "f5.txt"]
  print("files[0] ", files[0])
  print("files[3] ", files[3])
  print("files[-1] ", files[-1])
  print("files[-3] ", files[-3])
  
  print("files[:3] ", files[:3])
  print("files[2:4] ", files[2:4])
  print("files[-3:] ", files[-3:])
  ```

  **在列表中，你可以存放不同类型的元素，字符，数字，甚至列表里还能有列表。** 所以这个抽屉还挺万能的。

  ```py
  l = [1, "file", ["2", 3.2]]
  print(l)
  l[2][0] = "new string"
  print(l)
  ```

* Dict 字典

  * 可以理解为List是抽屉，Dict是为抽屉贴标签，后续找东西就可以根据标签找。

  ```py
  files = {"ID": 111, "passport": "my passport", "books": [1,2,3]}
  print(files)
  print(files["books"])
  
  files["ID"] = 222
  print(files)
  ```

* Tuple 元组
  * 元组有它一个唯一的独特性，就是它里面的东西不可变，定下来就定下来了，不让你变。

```py
files = ("file1", "file2", "file3")
print(files[1])
files[1] = "file4"   # 这里会报错
```

* set 合集
  * set 里面只会存在非重复的元素

```py
my_files = set(["file1", "file2", "file3"])
print(my_files)
my_files.add("file3")
print(my_files)
my_files.add("file4")
print(my_files)
my_files.remove("file3")
print(my_files)

# {'file1', 'file2', 'file3'}
# {'file1', 'file2', 'file3'}
# {'file4', 'file1', 'file2', 'file3'}
# {'file4', 'file1', 'file2'}
```

```py
print("my_files", my_files)
your_files = {"file1", "file3", "file5"}
print("your_files", your_files)
print("交集 ", your_files.intersection(my_files))
print("并集 ", your_files.union(my_files))
print("补集 ", your_files.difference(my_files))
```

6）在循环中使用

```py
# List
files = ["f1.txt", "f2.txt", "f3.txt", "f4.txt", "f5.txt"]
for f in files:
    if f == "f3.txt":
        print("I got f3.txt")

# Dict 字典
files = {"ID": 111, "passport": "my passport", "books": [1,2,3]}
for key in files.keys():
    print("key:", key)

for value in files.values():
    print("value:", value)

for key, value in files.items():
    print("key:", key, ", value:", value)
```

7）自带功能

* 往列表里面添加和pop值。

  ```py
  files = []
  for i in range(5):
      files.append("f"+str(i)+".txt") # 添加
      print("has", files)
  
  for i in range(len(files)):
      print("pop", files.pop())   # 从最后一个开始 pop 出
      print("remain", files)
  
  # 输出：
  has ['f0.txt']
  has ['f0.txt', 'f1.txt']
  has ['f0.txt', 'f1.txt', 'f2.txt']
  has ['f0.txt', 'f1.txt', 'f2.txt', 'f3.txt']
  has ['f0.txt', 'f1.txt', 'f2.txt', 'f3.txt', 'f4.txt']
  pop f4.txt
  remain ['f0.txt', 'f1.txt', 'f2.txt', 'f3.txt']
  pop f3.txt
  remain ['f0.txt', 'f1.txt', 'f2.txt']
  pop f2.txt
  remain ['f0.txt', 'f1.txt']
  pop f1.txt
  remain ['f0.txt']
  pop f0.txt
  remain []
  ```

  常用的功能函数

  ```py
  
  files = ["f1.txt", "f2.txt"]
  
  # 扩充入另一个列表
  files.extend(["f3.txt", "f4.txt"])
  print("extend", files)
  
  # 按位置添加
  files.insert(1, "file5.txt")     # 添加入第1位（首位是0哦）
  print("insert", files)
  
  # 移除某索引
  del files[1]
  print("del", files)
  
  # 移除某值 
  files.remove("f3.txt")
  print("remove", files)
  
  ```

  字典也是，也有额外的一些常用功能，比如`get()`, `update()`等，我下面在补充一下。

  ```py
  files = {"ID": 111, "passport": "my passport", "books": [1,2,3]}
  
  # 按key拿取，并在拿取失败的时候给一个设定好的默认值
  print('files["ID"]:', files["ID"])
  print('files.get("ID"):', files.get("unknown ID", "不存在这个 ID"))
  
  # 将另一个字典补充到当前字典
  files.update({"files": ["1", "2"]})
  print('update:', files)
  
  # pop 调一个item，和列表的 pop 类似
  popped = files.pop("ID")
  print('popped:', popped)
  print("remain:", files)
  
  ```



### Function 函数

1）定义函数：

```py
def f():
  pass
```

2）参数列表

```py
def f(x, a, b, c):
    return a*x**2 + b*x + c*1
print(f(2, 1, 1, 0))    # 忽略参数名，按顺序传参
print(f(x=2, a=1, b=1, c=0)) # 写上参数名，按名字传参
print(f(a=1, c=0, x=2, b=1)) # 若用参数名，可以打乱顺序传

# 默认值
def f(x, a=1, b=1, c=0):
    return a*x**2 + b*x + c*1
print(f(2, a=2))
print(f(2))
```

3）全局和局部变量

| 变量        | 特点                    |
| :---------- | :---------------------- |
| 全局 global | 函数里外都能用 （公用） |
| 局部 local  | 仅在函数内有用 （私有） |

这里注意

```py
filename = "f1.txt"
def modify_name():
    filename = "f2.txt"
    print("local filename:", filename)
modify_name()
print("global filename:", filename)  

# 输出：
# local filename: f2.txt
# global filename: f1.txt
```

问题：为什么我在 `modify_name()` 里面修改了 `filename`，而且在里面打印出来时，它的确也被修改了， 但是在外面打印 `filename` 的时候却没有变化？

答：因为自私的 `modify_name()` 想自己在内部搞一套标准， 你外面有啥不要紧，如果我自己也搞一个一样的东西，那我就觉得自己这个更重要，就不看外面的东西了。所以local的`filename`就是 `modify_name()` 自己那一套。

如果需要改变呢：

```py
filename = "f1.txt"
def modify_name():
    global filename  # 提出申请
    filename = "f2.txt"
    print("local filename:", filename)
modify_name()
print("global filename:", filename)  

# 输出：
# local filename: f2.txt
# global filename: f2.txt
```

modify_name()` 必须先向外面打一个申请报告，向外面申请自己要去修改公用的 `filename`。 



### Class类

1）定义class

用 `class File` 来创建一个大概念（类），**注意我们通常约定类的名字要首字母大写**。 然后用 `my_file = File()` 来创建一个具体的文件。

```py
class File:
    def __init__(self):
        self.name = "f1"
        self.create_time = "today"

my_file = File()
print(my_file.name)
print(my_file.create_time)
```

`self` 是作为类自己的一个索引，不管你在定义类的时候，想要获取这个类的什么属性或功能，都可以通过 `self` 来获取。 比如这个 `File` 类中，获取类自己的 `create_time`，就写成了 `self.create_time`。

`__init__`每当你进行一次 `my_file = File()` 这种操作的时候，把类给实例化的时候， `File` 类都会触发一次 `__init__` 功能，所以这是一个功能，用于初始化一些设置。



2）class的功能

初始化 `File()` 的时候传入你要 `__init__` 的参数。

```py
class File:
    def __init__(self, name, create_time="today"):
        self.name = name
        self.create_time = create_time

my_file = File("my_file")
print(my_file.name)
print(my_file.create_time)
```




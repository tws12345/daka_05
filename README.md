# daka_05
字典、集合和序列

字典

1.可变类型与不可变类型
    序列是以连续的整数为索引，与此不同的是，字典以"关键字"为索引，关键字可以是任意不可变类型，通常用字符串或数值。
    字典是 Python 唯一的一个 映射类型，字符串、元组、列表属于序列类型。
    那么如何快速判断一个数据类型 X 是不是可变类型的呢？两种方法：

    i = 1
    print(id(i))  # 140732167000896
    i = i + 2
    print(id(i))  # 140732167000960

    l = [1, 2]
    print(id(l))  # 4300825160
    l.append('Python')
    print(id(l))  # 4300825160
    整数 i 在加 1 之后的 id 和之前不一样，因此加完之后的这个 i (虽然名字没变)，但不是加之前的那个 i 了，因此整数是不可变类型。
    列表 l 在附加 'Python' 之后的 id 和之前一样，因此列表是可变类型。


    print(hash('Name'))  # -9215951442099718823

    print(hash((1, 2, 'Python')))  # 823362308207799471

    print(hash([1, 2, 'Python']))
    # TypeError: unhashable type: 'list'

    print(hash({1, 2, 3}))
    # TypeError: unhashable type: 'set'
    数值、字符和元组 都能被哈希，因此它们是不可变类型。
    列表、集合、字典不能被哈希，因此它是可变类型。

2.字典的定义
    字典 是无序的 键:值（key:value）对集合，键必须是互不相同的（在同一个字典之内）。

    dict 内部存放的顺序和 key 放入的顺序是没有关系的。
    dict 查找和插入的速度极快，不会随着 key 的增加而增加，但是需要占用大量的内存。
    字典 定义语法为 {元素1, 元素2, ..., 元素n}


3.创建和访问字典


    brand = ['李宁', '耐克', '阿迪达斯']
    slogan = ['一切皆有可能', 'Just do it', 'Impossible is nothing']
    print('耐克的口号是:', slogan[brand.index('耐克')])  
    # 耐克的口号是: Just do it
    dic = {'李宁': '一切皆有可能', '耐克': 'Just do it', '阿迪达斯': 'Impossible is nothing'}
    print('耐克的口号是:', dic['耐克'])  
    # 耐克的口号是: Just do it

    通过字符串或数值作为key来创建字典。

    dic1 = {1: 'one', 2: 'two', 3: 'three'}
    print(dic1)  # {1: 'one', 2: 'two', 3: 'three'}
    print(dic1[1])  # one
    print(dic1[4])  # KeyError: 4

    dic2 = {'rice': 35, 'wheat': 101, 'corn': 67}
    print(dic2)  # {'wheat': 101, 'corn': 67, 'rice': 35}
    print(dic2['rice'])  # 35
    注意：如果我们取的键在字典中不存在，会直接报错KeyError。

    通过元组作为key来创建字典，但一般不这样使用。

    dic = {(1, 2, 3): "Tom", "Age": 12, 3: [3, 5, 7]}
    print(dic)  # {(1, 2, 3): 'Tom', 'Age': 12, 3: [3, 5, 7]}
    print(type(dic))  # <class 'dict'>
    通过构造函数dict来创建字典。

    dict() 创建一个空的字典。
    通过key直接把数据放入字典中，但一个key只能对应一个value，多次对一个key放入 value，后面的值会把前面的值冲掉。

    dic = dict()
    dic['a'] = 1
    dic['b'] = 2
    dic['c'] = 3

    print(dic)
    # {'a': 1, 'b': 2, 'c': 3}

    dic['a'] = 11
    print(dic)
    # {'a': 11, 'b': 2, 'c': 3}

    dic['d'] = 4
    print(dic)
    # {'a': 11, 'b': 2, 'c': 3, 'd': 4}
    dict(mapping) new dictionary initialized from a mapping object's (key, value) pairs


    dic1 = dict([('apple', 4139), ('peach', 4127), ('cherry', 4098)])
    print(dic1)  # {'cherry': 4098, 'apple': 4139, 'peach': 4127}

    dic2 = dict((('apple', 4139), ('peach', 4127), ('cherry', 4098)))
    print(dic2)  # {'peach': 4127, 'cherry': 4098, 'apple': 4139}
    dict(**kwargs) -> new dictionary initialized with the name=value pairs in the keyword argument list. For example: dict(one=1, two=2)

    这种情况下，键只能为字符串类型，并且创建的时候字符串不能加引号，加上就会直接报语法错误。
    dic = dict(name='Tom', age=10)
    print(dic)  # {'name': 'Tom', 'age': 10}
    print(type(dic))  # <class 'dict'>

4.字典的内置方法

    dict.fromkeys(seq[, value]) 用于创建一个新字典，以序列 seq 中元素做字典的键，value 为字典所有键对应的初始值。


    seq = ('name', 'age', 'sex')
    dic1 = dict.fromkeys(seq)
    print(dic1)
    # {'name': None, 'age': None, 'sex': None}

    dic2 = dict.fromkeys(seq, 10)
    print(dic2)
    # {'name': 10, 'age': 10, 'sex': 10}

    dic3 = dict.fromkeys(seq, ('小马', '8', '男'))
    print(dic3)
    # {'name': ('小马', '8', '男'), 'age': ('小马', '8', '男'), 'sex': ('小马', '8', '男')}

    dict.keys()返回一个可迭代对象，可以使用 list() 来转换为列表，列表为字典中的所有键。
    dic = {'Name': 'lsgogroup', 'Age': 7}
    print(dic.keys())  # dict_keys(['Name', 'Age'])
    lst = list(dic.keys())  # 转换为列表
    print(lst)  # ['Name', 'Age']

    dict.values()返回一个迭代器，可以使用 list() 来转换为列表，列表为字典中的所有值。
    dic = {'Sex': 'female', 'Age': 7, 'Name': 'Zara'}
    print(dic.values())
    # dict_values(['female', 7, 'Zara'])

    print(list(dic.values()))
    # [7, 'female', 'Zara']

    dict.items()以列表返回可遍历的 (键, 值) 元组数组。
    dic = {'Name': 'Lsgogroup', 'Age': 7}
    print(dic.items())
    # dict_items([('Name', 'Lsgogroup'), ('Age', 7)])

    print(tuple(dic.items()))
    # (('Name', 'Lsgogroup'), ('Age', 7))

    print(list(dic.items()))
    # [('Name', 'Lsgogroup'), ('Age', 7)]

    dict.get(key, default=None) 返回指定键的值，如果值不在字典中返回默认值。
    dic = {'Name': 'Lsgogroup', 'Age': 27}
    print("Age 值为 : %s" % dic.get('Age'))  # Age 值为 : 27
    print("Sex 值为 : %s" % dic.get('Sex', "NA"))  # Sex 值为 : NA
    print(dic)  # {'Name': 'Lsgogroup', 'Age': 27}

    dict.setdefault(key, default=None)和get()方法 类似, 如果键不存在于字典中，将会添加键并将值设为默认值。
    dic = {'Name': 'Lsgogroup', 'Age': 7}
    print("Age 键的值为 : %s" % dic.setdefault('Age', None))  # Age 键的值为 : 7
    print("Sex 键的值为 : %s" % dic.setdefault('Sex', None))  # Sex 键的值为 : None
    print(dic)  
    # {'Age': 7, 'Name': 'Lsgogroup', 'Sex': None}
    key in dict in 操作符用于判断键是否存在于字典中，如果键在字典 dict 里返回true，否则返回false。

    dic = {'Name': 'Lsgogroup', 'Age': 7}

    # in 检测键 Age 是否存在
    if 'Age' in dic:
        print("键 Age 存在")
    else:
        print("键 Age 不存在")

    # 检测键 Sex 是否存在
    if 'Sex' in dic:
        print("键 Sex 存在")
    else:
        print("键 Sex 不存在")

    # not in 检测键 Age 是否存在
    if 'Age' not in dic:
        print("键 Age 不存在")
    else:
        print("键 Age 存在")

    # 键 Age 存在
    # 键 Sex 不存在
    # 键 Age 存在
    dict.pop(key[,default])删除字典给定键 key 所对应的值，返回值为被删除的值。key 值必须给出。若key不存在，则返回 default 值。
    del dict[key] 删除字典给定键 key 所对应的值。


    dic1 = {1: "a", 2: [1, 2]}
    print(dic1.pop(1), dic1)  # a {2: [1, 2]}

    # 设置默认值，必须添加，否则报错
    print(dic1.pop(3, "nokey"), dic1)  # nokey {2: [1, 2]}

    del dic1[2]
    print(dic1)  # {}

    dict.popitem()随机返回并删除字典中的一对键和值，如果字典已经为空，却调用了此方法，就报出KeyError异常。
    dic1 = {1: "a", 2: [1, 2]}
    print(dic1.popitem())  # (1, 'a')
    print(dic1)  # {2: [1, 2]}

    dict.clear()用于删除字典内所有元素。
    dic = {'Name': 'Zara', 'Age': 7}
    print("字典长度 : %d" % len(dic))  # 字典长度 : 2
    dic.clear()
    print("字典删除后长度 : %d" % len(dic))  
    # 字典删除后长度 : 0

    dict.copy()返回一个字典的浅复制。
    dic1 = {'Name': 'Lsgogroup', 'Age': 7, 'Class': 'First'}
    dic2 = dic1.copy()
    print("dic2")  
    # {'Age': 7, 'Name': 'Lsgogroup', 'Class': 'First'}

    直接赋值和 copy 的区别
    dic1 = {'user': 'lsgogroup', 'num': [1, 2, 3]}
    # 引用对象
    dic2 = dic1  
    # 浅拷贝父对象（一级目录），子对象（二级目录）不拷贝，还是引用
    dic3 = dic1.copy()  

    print(id(dic1))  # 148635574728
    print(id(dic2))  # 148635574728
    print(id(dic3))  # 148635574344

    # 修改 data 数据
    dic1['user'] = 'root'
    dic1['num'].remove(1)

    # 输出结果
    print(dic1)  # {'user': 'root', 'num': [2, 3]}
    print(dic2)  # {'user': 'root', 'num': [2, 3]}
    print(dic3)  # {'user': 'runoob', 'num': [2, 3]}
    dict.update(dict2)把字典参数 dict2 的 key:value对 更新到字典 dict 里。

    dic = {'Name': 'Lsgogroup', 'Age': 7}
    dic2 = {'Sex': 'female', 'Age': 8}
    dic.update(dic2)
    print(dic)  
    # {'Sex': 'female', 'Age': 8, 'Name': 'Lsgogroup'}
    
5.练习题：

    1、字典基本操作
    字典内容如下:
    dic = {
        'python': 95,
        'java': 99,
        'c': 100
        }

    用程序解答下面的题目：
    字典的长度是多少
    请修改’java’ 这个key对应的value值为98
    删除 c 这个key
    增加一个key-value对，key值为 php, value是90
    获取所有的key值，存储在列表里
    获取所有的value值，存储在列表里
    判断 javascript 是否在字典中
    获得字典里所有value 的和
    获取字典里最大的value
    获取字典里最小的value
    字典 dic1 = {‘php’: 97}， 将dic1的数据更新到dic中

    dic = {
        'python': 95,
        'java': 99,
        'c': 100
        }
    #字典的长度是多少
    print(len(dic))
    #请修改'java' 这个key对应的value值为98
    dic['java']=98
    print(dic)
    #删除 c 这个key
    dic.pop('c')
    print(dic)
    #增加一个key-value对，key值为 php, value是90
    dic.setdefault('php',90)
    print(dic)
    #获取所有的key值，存储在列表里
    a=list(dic.keys())
    print(a)
    #获取所有的value值，存储在列表里
    a=list(dic.values())
    print(a)
    #判断 javascript 是否在字典中
    if 'javascript' in dic:
        print("javascript在字典中")
    else:
        print("javascript不存在")
    #获得字典里所有value 的和
    print(sum(dic.values()))
    #获取字典里最大的value
    print(max(dic.values()))
    #获取字典里最小的value
    print(min(dic.values()))
    #字典 dic1 = {'php': 97}， 将dic1的数据更新到dic中
    dic1={'php':97}
    dic.update(dic1)
    print(dic)

    
    
    {'python': 95, 'java': 98, 'c': 100}
    {'python': 95, 'java': 98}
    {'python': 95, 'java': 98, 'php': 90}
    ['python', 'java', 'php']
    [95, 98, 90]
    javascript不存在
    283
    98
    90
    {'python': 95, 'java': 98, 'php': 97}

    2、字典中的value

    有一个字典，保存的是学生各个编程语言的成绩，内容如下

    data = {
            'python': {'上学期': '90', '下学期': '95'},
            'c++': ['95', '96', '97'],
            'java': [{'月考':'90', '期中考试': '94', '期末考试': '98'}]
            }
    各门课程的考试成绩存储方式并不相同，有的用字典，有的用列表，但是分数都是字符串类型，请实现函数transfer_score(score_dict)，将分数修改成int类型


    def transfer_score(data):
        # your code here
        for i in list(data.values()):
            if isinstance(i,dict):
                #i.values()=int(list(i.values()))
                for j in int(i.keys()):
                    i[j]=int(i[j])
            elif isinstance(i,list):
                i=int(i)
            else:
                i=int(i)

    data1 = {
            'python': {'上学期': '90', '下学期': '95'},
            'c++': ['95', '96', '97']
            }
    print(data1)
    a=list(data1.values())
    print(a[0]) 
    print(isinstance(a[0],dict))
    b=list(a[0].values())
    print(b)
    b=[int(i) for i in b]
    print(b)
    print(data1)

    print(list(data1.values()))
    for i in list(data.values()):
        if isinstance(i,dict):
        #i.values()=int(list(i.values()))
            for j in list(i.keys()):
                i[j]=int(i[j])

    print(data1)


    
    
集合

        python 中 set 与 dict 类似，也是一组 key 的集合，但不存储 value 。由于 key 不能重复，所以，在 set 中，没
        有重复的 key 。
        注意， key 为不可变类型，即可哈希的值。

1.集合的创建
    1. 先创建对象再加入元素。
    2. 在创建空集合的时候只能使用 s = set() ，因为 s = {} 创建的是空字典。

    直接把一堆元素用花括号括起来 {元素1, 元素2, ..., 元素n} 。
    重复元素在 set 中会被自动被过滤。

    def transfer_score(data):
     # your code here
    num = {}
    print(type(num)) # <class 'dict'>
    num = {1, 2, 3, 4}
    print(type(num)) # <class 'set'>
    basket = set()
    basket.add('apple')
    basket.add('banana')
    print(basket) # {'banana', 'apple'}


    basket = {'apple', 'orange', 'apple', 'pear', 'orange', 'banana'}
    print(basket) # {'banana', 'apple', 'pear', 'orange'}

    使用 set(value) 工厂函数，把列表或元组转换成集合。
    a = set('abracadabra')
    print(a) 
    # {'r', 'b', 'd', 'c', 'a'}
    b = set(("Google", "Lsgogroup", "Taobao", "Taobao"))
    print(b) 
    # {'Taobao', 'Lsgogroup', 'Google'}

    去掉列表中重复的元素

    lst = [0, 1, 2, 3, 4, 5, 5, 3, 1]
    temp = []
    for item in lst:
     if item not in temp:
     temp.append(item)
    print(temp) # [0, 1, 2, 3, 4, 5]
    a = set(lst)
    print(list(a)) # [0, 1, 2, 3, 4, 5]
    从结果发现集合的两个特点：无序 (unordered) 和唯一 (unique)。
    由于 set 存储的是无序集合，所以我们不可以为集合创建索引或执行切片(slice)操作，也没有键(keys)可用来获取
    集合中元素的值，但是可以判断一个元素是否在集合中。

 2.访问集合中的值
 
     可以使用 len() 內建函数得到集合的大小。
     可以使用 for 把集合中的数据一个个读取出来。
     可以通过 in 或 not in 判断一个元素是否在集合中已经存在

 3.集合的内置方法
 
    set.add(elmnt) 用于给集合添加元素，如果添加的元素在集合中已存在，则不执行任何操作。

    thisset = set(['Google', 'Baidu', 'Taobao'])
    print(len(thisset)) # 3
    thisset = set(['Google', 'Baidu', 'Taobao'])
    for item in thisset:
     print(item)
    # Baidu
    # Google
    # Taobao
    thisset = set(['Google', 'Baidu', 'Taobao'])
    print('Taobao' in thisset) # True
    print('Facebook' not in thisset) # True
    fruits = {"apple", "banana", "cherry"}
    fruits.add("orange")
    print(fruits) 
    # {'orange', 'cherry', 'banana', 'apple'}
    fruits.add("apple")
    print(fruits) 
    # {'orange', 'cherry', 'banana', 'apple'}

    1set.update(set) 用于修改当前集合，可以添加新的元素或集合到当前集合中，如果添加的元素在集合中已
    存在，则该元素只会出现一次，重复的会忽略。

    x = {"apple", "banana", "cherry"}
    y = {"google", "baidu", "apple"}
    x.update(y)
    print(x)
    # {'cherry', 'banana', 'apple', 'google', 'baidu'}
    y.update(["lsgo", "dreamtech"])
    print(y)
    # {'lsgo', 'baidu', 'dreamtech', 'apple', 'google'}

    set.remove(item) 用于移除集合中的指定元素。如果元素不存在，则会发生错误。
    fruits = {"apple", "banana", "cherry"}
    fruits.remove("banana")
    print(fruits) # {'apple', 'cherry'}

    set.discard(value) 用于移除指定的集合元素。 remove() 方法在移除一个不存在的元素时会发生错误，
    而 discard() 方法不会。

    fruits = {"apple", "banana", "cherry"}
    fruits.discard("banana")
    print(fruits) # {'apple', 'cherry'}

    set.pop() 用于随机移除一个元素。

    fruits = {"apple", "banana", "cherry"}
    x = fruits.pop()
    print(fruits) # {'cherry', 'apple'}
    print(x) # banana

    由于 set 是无序和无重复元素的集合，所以两个或多个 set 可以做数学意义上的集合操作。
    set.intersection(set1, set2 ...) 返回两个集合的交集。
    set1 & set2 返回两个集合的交集。
    set.intersection_update(set1, set2 ...) 交集，在原始的集合上移除不重叠的元素。


    a = set('abracadabra')
    b = set('alacazam')
    print(a) # {'r', 'a', 'c', 'b', 'd'}
    print(b) # {'c', 'a', 'l', 'm', 'z'}
    c = a.intersection(b)
    print(c) # {'a', 'c'}
    print(a & b) # {'c', 'a'}
    print(a) # {'a', 'r', 'c', 'b', 'd'}
    a.intersection_update(b)
    print(a) # {'a', 'c'}

    set.union(set1, set2...) 返回两个集合的并集。
    set1 | set2 返回两个集合的并集。

    a = set('abracadabra')
    b = set('alacazam')
    print(a) # {'r', 'a', 'c', 'b', 'd'}
    print(b) # {'c', 'a', 'l', 'm', 'z'}
    print(a | b) # {'l', 'd', 'm', 'b', 'a', 'r', 'z', 'c'}
    c = a.union(b)
    print(c) # {'c', 'a', 'd', 'm', 'r', 'b', 'z', 'l'}

    set.difference(set) 返回集合的差集。
    set1 - set2 返回集合的差集。
    set.difference_update(set) 集合的差集，直接在原来的集合中移除元素，没有返回值。
    a = set('abracadabra')
    b = set('alacazam')
    print(a) # {'r', 'a', 'c', 'b', 'd'}
    print(b) # {'c', 'a', 'l', 'm', 'z'}
    c = a.difference(b)
    print(c) # {'b', 'd', 'r'}
    print(a - b) # {'d', 'b', 'r'}
    print(a) # {'r', 'd', 'c', 'a', 'b'}
    a.difference_update(b)
    print(a) # {'d', 'r', 'b'}

    set.symmetric_difference(set) 返回集合的异或。
    set1 ^ set2 返回集合的异或。
    set.symmetric_difference_update(set) 移除当前集合中在另外一个指定集合相同的元素，并将另外一个
    指定集合中不同的元素插入到当前集合中。
    a = set('abracadabra')
    b = set('alacazam')
    print(a) # {'r', 'a', 'c', 'b', 'd'}
    print(b) # {'c', 'a', 'l', 'm', 'z'}
    c = a.symmetric_difference(b)
    print(c) # {'m', 'r', 'l', 'b', 'z', 'd'}
    print(a ^ b) # {'m', 'r', 'l', 'b', 'z', 'd'}
    print(a) # {'r', 'd', 'c', 'a', 'b'}
    a.symmetric_difference_update(b)
    print(a) # {'r', 'b', 'm', 'l', 'z', 'd'}

    set.issubset(set) 判断集合是不是被其他集合包含，如果是则返回 True，否则返回 False。
    set1 <= set2 判断集合是不是被其他集合包含，如果是则返回 True，否则返回 False。
    x = {"a", "b", "c"}
    y = {"f", "e", "d", "c", "b", "a"}
    z = x.issubset(y)
    print(z) # True
    print(x <= y) # True
    x = {"a", "b", "c"}
    y = {"f", "e", "d", "c", "b"}
    z = x.issubset(y)
    print(z) # False
    print(x <= y) # False

    set.issuperset(set) 用于判断集合是不是包含其他集合，如果是则返回 True，否则返回 False。
    set1 >= set2 判断集合是不是包含其他集合，如果是则返回 True，否则返回 False。
    set.isdisjoint(set) 用于判断两个集合是不是不相交，如果是返回 True，否则返回 False。


4.集合的转换

    x = {"f", "e", "d", "c", "b", "a"}
    y = {"a", "b", "c"}
    z = x.issuperset(y)
    print(z) # True
    print(x >= y) # True
    x = {"f", "e", "d", "c", "b"}
    y = {"a", "b", "c"}
    z = x.issuperset(y)
    print(z) # False
    print(x >= y) # False
    x = {"f", "e", "d", "c", "b"}
    y = {"a", "b", "c"}
    z = x.isdisjoint(y)
    print(z) # False
    x = {"f", "e", "d", "m", "g"}
    y = {"a", "b", "c"}
    z = x.isdisjoint(y)
    print(z) # True
    se = set(range(4))
    li = list(se)
    tu = tuple(se)
    print(se, type(se)) # {0, 1, 2, 3} <class 'set'>
    print(li, type(li)) # [0, 1, 2, 3] <class 'list'>
    print(tu, type(tu)) # (0, 1, 2, 3) <class 'tuple'>

5.不可变集合

    Python 提供了不能改变元素的集合的实现版本，即不能增加或删除元素，类型名叫 frozenset 。需要注意的
    是 frozenset 仍然可以进行集合操作，只是不能用带有 update 的方法。
    frozenset([iterable]) 返回一个冻结的集合，冻结后集合不能再添加或删除任何元素。


练习题：

    1. 怎么表示只包含⼀个数字1的元组。
        a=(1,)
        print(a,type(a))
        
        (1,) <class 'tuple'>
    2. 创建一个空集合，增加 {‘x’,‘y’,‘z’} 三个元素。
        a=set()
        a.add('x')
        a.add('y')
        a.add('z')
        print(a)         
        {'z', 'y', 'x'}
    3. 列表['A', 'B', 'A', 'B']去重。
        a=['A','B','A','B']
        b=set(a)
        print(list(b))
        ['A', 'B']
    4. 求两个集合{6, 7, 8}，{7, 8, 9}中不重复的元素（差集指的是两个集合交集外的部分）。
        a={6,7,8}
        b={7,8,9}
        print(a-b)
        print(b-a)
        print(a^b)
            {6}
            {9}
            {9, 6}
    5. 求{'A', 'B', 'C'}中元素在 {'B', 'C', 'D'}中出现的次数。
        a={'A','B','C'}
        b={'B','C','D'}
        c=a&b
        print(c)
        print(len(c))

            {'C', 'B'}
            2

序列

1.针对序列的内置函数

list(sub) 把一个可迭代对象转换为列表。

    a = frozenset(range(10)) # 生成一个新的不可变集合
    print(a) 
    # frozenset({0, 1, 2, 3, 4, 5, 6, 7, 8, 9})
    b = frozenset('lsgogroup')
    print(b) 
    # frozenset({'g', 's', 'p', 'r', 'u', 'o', 'l'})


tuple(sub) 把一个可迭代对象转换为元组。

    a = tuple()
    print(a) # ()
    b = 'I Love LsgoGroup'
    b = tuple(b)
    print(b) 
    # ('I', ' ', 'L', 'o', 'v', 'e', ' ', 'L', 's', 'g', 'o', 'G', 'r', 'o', 'u', 'p')
    c = [1, 1, 2, 3, 5, 8]
    c = tuple(c)
    print(c) # (1, 1, 2, 3, 5, 8)

str(obj) 把obj对象转换为字符串
    a = 123
    a = str(a)
    print(a) # 123

    len(s) 返回对象（字符、列表、元组等）长度或元素个数。
    a. s -- 对象。

    a = list()
    print(len(a)) # 0
    b = ('I', ' ', 'L', 'o', 'v', 'e', ' ', 'L', 's', 'g', 'o', 'G', 'r', 'o', 'u', 'p')
    print(len(b)) # 16
    c = 'I Love LsgoGroup'
    print(len(c)) # 16

max(sub) 返回序列或者参数集合中的最大值

    print(max(1, 2, 3, 4, 5)) # 5


 min(sub) 返回序列或参数集合中的最小值
 
    print(min(1, 2, 3, 4, 5)) # 1

sum(iterable[, start=0]) 返回序列 iterable 与可选参数 start 的总和。

    print(sum([1, 3, 5, 7, 9])) # 25
    print(sum([1, 3, 5, 7, 9], 10)) # 35

sorted(iterable, key=None, reverse=False) 对所有可迭代的对象进行排序操作。

    a. iterable -- 可迭代对象。
    b. key -- 主要是用来进行比较的元素，只有一个参数，具体的函数的参数就是取自于可迭代对象中，指定可
    迭代对象中的一个元素来进行排序。
    c. reverse -- 排序规则， reverse = True 降序 ， reverse = False 升序（默认）。
    d. 返回重新排序的列表。
    x = [-8, 99, 3, 7, 83]
    print(sorted(x)) # [-8, 3, 7, 83, 99]
    print(sorted(x, reverse=True)) # [99, 83, 7, 3, -8]
    t = ({"age": 20, "name": "a"}, {"age": 25, "name": "b"}, {"age": 10, "name": "c"})
    x = sorted(t, key=lambda a: a["age"])
    print(x)
    # [{'age': 10, 'name': 'c'}, {'age': 20, 'name': 'a'}, {'age': 25, 'name': 'b'}]

reversed(seq) 函数返回一个反转的迭代器。
    a. seq -- 要转换的序列，可以是 tuple, string, list 或 range。
    s = 'lsgogroup'
    x = reversed(s)
    print(type(x)) # <class 'reversed'>
    print(x) # <reversed object at 0x000002507E8EC2C8>
    print(list(x))
    # ['p', 'u', 'o', 'r', 'g', 'o', 'g', 's', 'l']
    t = ('l', 's', 'g', 'o', 'g', 'r', 'o', 'u', 'p')
    print(list(reversed(t)))
    # ['p', 'u', 'o', 'r', 'g', 'o', 'g', 's', 'l']
    r = range(5, 9)
    print(list(reversed(r)))
    # [8, 7, 6, 5]
    x = [-8, 99, 3, 7, 83]
    print(list(reversed(x)))
    # [83, 7, 3, 99, -8]
    enumerate(sequence, [start=0])

    用于将一个可遍历的数据对象(如列表、元组或字符串)组合为一个索引序列，同时列出数据和数据下标，
    一般用在 for 循环当中。

    seasons = ['Spring', 'Summer', 'Fall', 'Winter']
    a = list(enumerate(seasons))
    print(a) 
    # [(0, 'Spring'), (1, 'Summer'), (2, 'Fall'), (3, 'Winter')]
    b = list(enumerate(seasons, 1))
    print(b) 
    # [(1, 'Spring'), (2, 'Summer'), (3, 'Fall'), (4, 'Winter')]
    for i, element in a:
     print('{0},{1}'.format(i, element))

zip(iter1 [,iter2 [...]])

    a. 用于将可迭代的对象作为参数，将对象中对应的元素打包成一个个元组，然后返回由这些元组组成的对
    象，这样做的好处是节约了不少的内存。
    b. 我们可以使用 list() 转换来输出列表。
    c. 如果各个迭代器的元素个数不一致，则返回列表长度与最短的对象相同，利用 * 号操作符，可以将元组
    解压为列表。
    a = [1, 2, 3]
    b = [4, 5, 6]
    c = [4, 5, 6, 7, 8]
    zipped = zip(a, b)
    print(zipped) # <zip object at 0x000000C5D89EDD88>
    print(list(zipped)) # [(1, 4), (2, 5), (3, 6)]
    zipped = zip(a, c)
    print(list(zipped)) # [(1, 4), (2, 5), (3, 6)]
    a1, a2 = zip(*zip(a, b))
    print(list(a1)) # [1, 2, 3]
    print(list(a2)) # [4, 5, 6]


练习题：

    1. 怎么找出序列中的最⼤、⼩值？
        a=[1,4,5,3,8,7,5]
        print(max(a))
        print(min(a))
            8
            1

    2. sort() 和 sorted() 区别
        1、sort()只能应用在列表list上，而sorted可以对所有可迭代的对象进行排序的操作
         2、sort方法会在原list上直接进行排序，不会创建新的list。而sorted方法不会对原来的数据做任何改动，排序后的结果是新生成的。如果我们不需要原来的数据而且数据是list类型，可以用          sort方法，能够节省空间。否则要用sorted方法。
    3. 怎么快速求 1 到 100 所有整数相加之和？
        a=sum(range(1,100))
        print(a)

    4. 求列表 [2,3,4,5] 中每个元素的立方根。
        def square3(x):
        higher=x
        lower=1
        step=
            return

        a=[2,3,4,5]
        for i in a:
            print(square2(i))
    5. 将[‘x’,‘y’,‘z’] 和 [1,2,3] 转成 [(‘x’,1),(‘y’,2),(‘z’,3)] 的形式。
            a=['x','y','z']
            b=[1,2,3]
            c=list(zip(a,b))
            print(c)
            [('x', 1), ('y', 2), ('z', 3)]








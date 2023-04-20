[TOC]

# python基础

## 数据与变量

1. Python可以处理任意大小的整数

   > 对于很大的数，允许在数字中间以`_`分隔，因此，10_000_000_000`和`10000000000`是完全一样的

2. 科学计数法：把10用e替代，1.23x10^9^就是`1.23e9`，或者`12.3e8`

3. Python还允许用 *r* 表示'内部的字符串默认不转义

   ```python
   print('\\\t\\')
   \       \
   
   print(r'\\\t\\')
   \\\t\\
   ```

4. python是动态语言

   > 可以把任意数据类型赋值给变量，同一个变量可以反复赋值，而且可以是不同类型的变量
   >
   > ```python
   > a=12   
   > a=true
   > a="test"
   > ```

5. 除法

   - 10 / 3  =3.3333333333333335
   - 10 // 3 =3
   - 10 % 3 =1

## 字符串和编码

1. 最早只有127个字符被编码到计算机里：大小写英文字母、数字和一些符号，这个编码表被称为==ASCII==编码（一个字节）

2. 中国制定了GB2312编码，用来把中文编进去，日本把日文编到Shift_JIS里，韩国把韩文编到Euc-kr里……结果就是，在多语言混合的文本中，显示出来会有乱码

3. ==Unicode字符集==应运而生。Unicode把所有语言都统一到一套编码里（常用的是==UCS-16==编码，用两个字节表示一个字符，非常偏僻的字符需要4个字节）

4. Unicode编码转化为“可变长编码”的**==UTF-8编码==**

   > UTF-8编码把一个Unicode字符根据不同的数字大小编码成1-6个字节，常用的英文字母被编码成1个字节，汉字通常是3个字节，只有很生僻的字符才会被编码成4-6个字节

5. ord()函数获取字符的编码（十进制），chr() 函数把十进制编码转换为对应的字符

   ```python
   >>> ord('A')
   65
   >>> ord('中')
   20013
   >>> chr(66)
   'B'
   >>> chr(25991)
   '文'
   ```

6. 以Unicode表示的str通过**encode()**方法可以编码为指定的bytes,要把bytes变为str，就需要用**decode()**方法

   ```python
   'ABC'.encode('ascii')
   b'ABC'
   '中文'.encode('utf-8')
   b'\xe4\xb8\xad\xe6\x96\x87'
   
   b'ABC'.decode('ascii')
   'ABC'
   b'\xe4\xb8\xad\xe6\x96\x87'.decode('utf-8')
   '中文'
   ```

7. **len()**函数可以计算字符串包含多少字符，若字符串转换为bytes，则计算字节数

   ```python
   >>> len('ABC')
   3
   >>> len('中文')
   2
   
   >>> len(b'ABC')
   3
   >>> len(b'\xe4\xb8\xad\xe6\x96\x87')
   6
   >>> len('中文'.encode('utf-8'))
   6
   ```

### 格式化   

- 占位符

```python
   >>> 'Hello, %s' % 'world'
'Hello, world'
   >>> 'Hi, %s, you have $%d.' % ('Michael', 1000000)
   'Hi, Michael, you have $1000000.'
```

   常见占位符如下：

| **占位符** |    **替换内容**     |
| :--------: | :-----------------: |
|     %d     |        整数         |
|     %f     |       浮点数        |
|     %s     |       字符串        |
|     %x     |    十六进制整数     |
|    %.nf    | 保留n位小数的浮点数 |

- format()

> format()方法，它会用传入的参数依次替换字符串内的占位符{0}、{1}……

```python
>>> 'Hello, {0}, 成绩提升了 {1:.1f}%'.format('小明', 17.125)
'Hello, 小明, 成绩提升了 17.1%'
```

- f-string

```python
>>> r = 2.5
>>> s = 3.14 * r ** 2
>>> print(f'The area of a circle with radius {r} is {s:.2f}')
The area of a circle with radius 2.5 is 19.62
```

> 字符串如果包含=={a}== *（a为变量名）*，就会以对应的变量替换

## list和tuple

### 列表list

> list是一种有序的可变集合，可以随时添加和删除其中的元素

```python
>>> classmates = ['Michael', 'Bob', 'Tracy']
>>> classmates
['Michael', 'Bob', 'Tracy']

>>> classmates.append('Adam')
>>> classmates
['Michael', 'Bob', 'Tracy', 'Adam']
```

1. list索引从0开始，==索引可以为负数==，-1表示倒数第一个，-n表示倒数第n个
2. **pop()** 方法用于删除末尾元素，**pop(i)**方法用于删除指定索引元素
3. list中的元素可以是不同数据类型（甚至可以是另一个list）

### 元组tuple

> 元组tuple和list非常类似，但是tuple一旦初始化就不能修改

```python
>>> classmates = ('Michael', 'Bob', 'Tracy')
```

- 定义空元组时，可以写成 *t=()*,但是定义一个元素时，不能写成*t=(1)*

  > 该情况的括号会被看成数学公式中的小括号，（1）的运算结果为1，所以t为整数
  >
  > > 应该按如下定义
  > >
  > > ```python
  > > >>> t = (1,)
  > > >>> t
  > > (1,)
  > > ```

## for-in循环

1. 结构： **for x in arr**  

   > x为变量，arr为list或tuple

2. 遍历1到n：**for x in range(n)**

   - `range(101)`：产生0到100范围的整数，==取不到101==
   - `range(1, 101)`：产生1到100范围的整数，相当于前面是闭区间后面是开区间。
   - `range(1, 101, 2)`：可以用来产生1到100的奇数，其中2是步长，即每次数值递增的值。
   - `range(100, 0, -2)`：可以用来产生100到1的偶数，其中-2是步长，即每次数字递减的值。

## 函数

1. 定义函数

   **def  func( …… ):**

   > def为关键字，func为函数名，括号内为参数列表

2. 函数参数

```python
# 在参数名前面的*表示args是一个可变参数
def add(*args):
    total = 0
    for val in args:
        total += val
    return total

# 在调用add函数时可以传入0个或多个参数
print(add())    # 0
print(add(1))    # 1
print(add(1, 2))    # 3
print(add(1, 2, 3))    # 6
print(add(1, 3, 5, 7, 9))    # 25
```


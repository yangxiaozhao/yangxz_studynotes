# JavaScript-Learning

## JavaScript简介

- 特点：

  1. 解释型动态语言
  2. 类似于C和Java的语法结构
  3. 基于原型的面向对象
  4. 严格区分大小写

- JavaScript的使用

  1. 标签引用

     ![image-20230430162003904](C:\Users\Zhao\AppData\Roaming\Typora\typora-user-images\image-20230430162003904.png)

  2. 文件引用

     ![image-20230430162028749](C:\Users\Zhao\AppData\Roaming\Typora\typora-user-images\image-20230430162028749.png)
  
- JavaScript的输出

  1. 页面输出

     ```javascript
     <script>
         document.write("Hello,World!");
     </script>
     ```

  2. 控制台输出

     ```javascript
     <script>
         console.log("输出一条日志");//最常用
         console.info("输出一条信息");
         console.warn("输出一条警告");
         console.error("输出一条错误");
     </script>
     ```

  3. 弹出窗口输出

     ```javascript
     <script>
         alert("Hello,World!");
     </script>
     ```



## JavaScript基础语法

### 标识符

- **第一个字符**必须是一个**字母**、**下划线**（ _ ）或一个**美元符号**（ $ ）。
- 其它字符可以是**字母、下划线、美元符号或数字**。
- 按照惯例，ECMAScript 标识符采用**驼峰命名法**。
- 标识符不能是关键字和保留字符。

### 字面量、变量

> 字面量实际上就是一些固定的值，比如：1、2 、3、true、false、null、NaN、“hello”，字面量都是不可以改变的，由于字面量不是很方便使用，所以在JavaScript中很少直接使用字面量，使用的而是变量。

![image-20230430162750823](C:\Users\Zhao\AppData\Roaming\Typora\typora-user-images\image-20230430162750823.png)

### 数据类型

JavaScript中一共有5种基本数据类型：

- 字符串型（String）

- 数值型（Number）

- 布尔型（Boolean）

- undefined型（Undefined）

- null型（Null）

  除此之外的类型都称为Object

- *<u>Object</u>*

-----

- `typeof 数据`  ： 检查一个变量的数据类型

### 强制类型转换

- **转换成String类型**

  1. 调用被转换数据类型的toString()方法，不会影响到原变量，会将转换的结果返回

     ```javascript
     var a = 123;
     a = a.toString();
     console.log(a);
     console.log(typeof a);
     ```

  2. 调用String()函数，并将被转换的数据作为参数传递给函数

     ```javascript
     var a = 123;
     a = String(a);     // '123'
     console.log(a);		
     console.log(typeof a);     
     
     var b = undefined;
     b = String(b);      // 'undefined'
     console.log(b);
     console.log(typeof b);   
     
     var c = null;
     c = String(c);    // 'null'
     console.log(c);
     console.log(typeof c);    
     ```

- **转换为Number类型**

  1. 使用Number()函数

     - 字符串 --> 数字
       - 如果是纯数字的字符串，则直接将其转换为数字
       - 如果字符串中有非数字的内容，则转换为NaN
       - 如果字符串是一个空串或者是一个全是空格的字符串，则转换为0
     - 布尔 --> 数字
       - true 转成 1
       - false 转成 0
     - null --> 数字
       - null 转成 0

     - undefined --> 数字
       - undefined 转成 NaN

  2. parseInt() 把一个字符串转换为一个整数

     ```javascript
     var a = "123";
     a = parseInt(a);
     console.log(a);
     console.log(typeof a);
     ```

  3. parseFloat() 把一个字符串转换为一个浮点数

     ```javascript
     var a = "123.456";
     a = parseFloat(a);
     console.log(a);
     console.log(typeof a);
     ```

- **转换为Boolean类型**

  > 将其它的数据类型转换为Boolean，只能使用Boolean()函数

  - 使用Boolean()函数
    - 数字 —> 布尔
      - 除了0和NaN，其余的都是true
    - 字符串 —> 布尔
      - 除了空串，其余的都是true
    - null和undefined都会转换为false
    - 对象也会转换为true



### 运算符

> 算术运算符（y=5）

| 运算符 | 描述 | 例子             | x 运算结果 | y 运算结果 |
| ------ | ---- | ---------------- | ---------- | ---------- |
| /      | 除法 | x=y/2            | 2.5        | 5          |
| ++     | 自增 | x=++y<br />x=y++ | 6<br />5   | 6 <br />6  |
| –      | 自减 | x=–y<br />x=y–   | 4 <br/>5   | 4 <br />4  |

> 比较运算符

- 使用 `==`来做相等运算
  - 当使用==来比较两个值时，如果值的类型不同，则**会自动进行类型转换**，将其转换为相同的类型，然后在比较
- 使用 `!=`来做不相等运算
  - 用来判断两个值是否不相等，如果不相等返回true，否则返回false， != **会对变量进行自动的类型转换**，如果值的类型不同，则会自动进行类型转换
- 使用 `===`来做全等运算
  - 用来判断两个值是否全等，它和相等类似，不同的是它**不会**做自动的类型转换，如果两个值的类型不同，直接返回false
- 使用 `!==`来做不全等运算
  - 用来判断两个值是否不全等，它和不等类似，不同的是它**不会**做自动的类型转换，如果两个值的类型不同，直接返回true

### 运算符优先级

> 由上到下依次减小，对于同级运算符，采用从左向右依次执行的方法

![image-20201013115557984](https://img-blog.csdnimg.cn/img_convert/695dff6b3d3117760c6fba7c0b09895b.png)

### 分支语句

**if 语句、switch语句、for 循环、while循环、do-while循环、break、continue的用法与Java一致**

----

### 对象基础

- Object类型，也称为一个对象，是JavaScript中的引用数据类型。
  - 它是一种复合值，将很多值聚合到一起，可以通过名字访问这些值。
  - 可以看做是属性的无序集合，每个属性都是一个名/值对。对象除了可以创建自有属性，还可以通过从一个名为原型的对象那里继承属性。
  - 除了字符串、数字、true、false、null和undefined之外，JavaScript中的值都是对象。

#### 创建对象

1. 方法一：

   ```JavaScript
   var person = new Object();
   person.name = "孙悟空";
   person.age = 18;
   console.log(person);
   ```

2. 方法二：

   ```JavaScript
   var person = {
       name: "孙悟空",
       age: 18
   };
   console.log(person);
   ```

#### 访问属性

![image-20230430165955177](C:\Users\Zhao\AppData\Roaming\Typora\typora-user-images\image-20230430165955177.png)

#### 删除属性

> 删除对象的属性可以使用delete关键字，格式如下：

`delete 对象.属性名`

#### 遍历对象属性

```JavaScript
var person = {
    name: "zhangsan",
    age: 18
}

for (var personKey in person) {
    var personVal = person[personKey];
    console.log(personKey + ":" + personVal);
}
```

### 函数

#### 函数创建

1. 使用 **函数对象** 来创建一个函数（几乎不用）

   `var 函数名 = new Function("执行语句");`

   ```javascript
   var fun = new Function("console.log('这是我的第一个函数');");
   ```

   

2. 使用 **函数声明** 来创建一个函数（比较常用）

   `function 函数名([形参1,形参2,...,形参N]) {
       语句...
   }`

   ```javascript
   function fun(){
       console.log("这是我的第二个函数");
   }
   ```

3. 使用 **函数表达式** 来创建一个函数（比较常用）

   `var 函数名  = function([形参1,形参2,...,形参N]) {
       语句....
   }`

   ```javascript
   var fun  = function() {
       console.log("这是我的第三个函数");
   }
   ```

#### 函数返回值

> 可以使用 return 来设置函数的返回值，return后的值将会作为函数的执行结果返回

```javascript
function sum(num1, num2) {
    return num1 + num2;
}

var result = sum(10, 20);
console.log(result);
```

#### 嵌套函数

---

嵌套函数：**在函数中声明**的函数就是嵌套函数，嵌套函数只能在**当前**函数中可以访问，在当前函数外无法访问。

----

#### 立即执行函数

> 函数定义完，立即被调用，这种函数叫做立即执行函数，立即执行函数往往只会执行一次
>
> ```javascript
> (function () {
>     alert("我是一个匿名函数");
> })();
> ```

#### 对象中的函数（方法）

> 如果一个函数作为一个对象的属性保存，那么我们称这个函数是这个对象的方法

```javascript
var person = {
    name: "zhangsan",
    age: 18,
    sayHello: function () {
        console.log(name + " hello")
    }
}

person.sayHello();
```

#### this对象

> 解析器在每次调用函数都会向函数内部传进一个**隐含的参数this**，this指向一个**函数执行的上下文对象**，根据函数的调用方式的不同，this会指向不同的对象

- 以函数的形式调用时，this永远都是window
- 以方法的形式调用时，this就是调用方法的那个对象

### 对象进阶

> 引例：我们想要创建多个对象

#### 工厂方法创建对象

```JavaScript
// 使用工厂模式创建对象
function createPerson(name, age) {
    // 创建新的对象
    var obj = new Object();
    // 设置对象属性
    obj.name = name;
    obj.age = age;
    // 设置对象方法
    obj.sayName = function () {
        console.log(this.name);
    };
    //返回新的对象
    return obj;
}

for (var i = 1; i <= 1000; i++) {
    var person = createPerson("person" + i, 18);
    console.log(person);     		// Object
}
```

### 用构造函数创建对象

> 上述工厂方法所创建的对象类型都是Object，我们既想实现创建对象的功能，又希望能明确创建的对象类型，就用到了构造函数
>
> > 每一个构造函数都可以理解为一个类别，用构造函数所创建的对象也称为类的实例

```javascript
// 使用构造函数来创建对象
function Person(name, age) {
    // 设置对象的属性
    this.name = name;
    this.age = age;
    // 设置对象的方法
    this.sayName = function () {
        console.log(this.name);
    };
}

var person1 = new Person("孙悟空", 18);
var person2 = new Person("猪八戒", 19);
var person3 = new Person("沙和尚", 20);

console.log(person1);       // Person
console.log(person2);       // Person
console.log(person3);       // Person
```

- 构造函数
  - 构造函数就是一个普通的函数，创建方式和普通函数没有区别
  - 构造函数习惯上首字母大写
  - 普通函数是直接调用，而构造函数需要使用new关键字来调用
- 构造函数执行创建对象的过程
  - 调用构造函数，它会立刻创建一个新的对象
  - 将新建的对象设置为函数中this，**在构造函数中可以使用this来引用新建的对象**
  - 逐行执行函数中的代码
  - 将新建的对象作为返回值返回

#### 原型



#### 原型链



#### hasOwnProperty方法



#### 对象继承



## JavaScript常用对象



## JavaScript DOM



## JavaScript BOM



## JavaScript高级语法



## JavaScript新特性






































































































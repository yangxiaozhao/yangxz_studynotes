# Java ContinueLearning  

[TOC]

## 类，抽象类，接口

类： 关键字 class  ，可继承父类的成员及方法，关键字 extends

```java
public class Fu{
    int a;
    public void fu(){……}
}
public class Zi extends Fu{
    public void fu(){……}      // 可改写父类方法
}
```

抽象类：关键字 abstract class ，含有抽象方法（只声明，不做任何实现，关键字 abstract ）的类为抽象类，抽象类不可被实例化，可继承父类抽象类，抽象类被继承后，其子类必须实现父类的所有抽象方法，否则子类依然为抽象类，无法实例化

```java
public abstract class Fu{
    private int a;
    public abstract void fu();      //只声明
    public void m(){……}             
}
public class Zi extends Fu{
    public void fu(){……}
}
```

接口：关键字 interface ，接口中数据均为 public static final 类型，方法均为抽象方法且只能是public abstract ，可继承父类接口，关键字 extends，实现接口使用关键字 implements

```java
public interface CPU{
    public void use();       //可省略关键字abstract
}
public class PC implements CPU{
    public void use(){……}
}
```

## 枚举类

> Java 枚举是一个特殊的类，一般表示一组常量，比如一年的 4 个季节，一个星期的 7 天，方向有东南西北等。

Java 枚举类使用 enum 关键字来定义，各个常量使用逗号来分割，例如定义一个颜色的枚举类。

```java
enum Color{
    RED,BLUD,GREEN;
}

public class Test{
    public static void main(String[] abs){
        Color c=Color.GREEN;
        System.out.println(c);
    }
}
```

枚举类跟普通类一样可以有自己的变量、方法和构造函数，构造函数只能使用 private 访问修饰符，所以外部无法调用。

```java
enum Color{
    RED, GREEN, BLUE;
    
    private Color(){
        System.out.println("Constructor called for : " + this.toString());
    }
 
    public void colorInfo(){
        System.out.println("Universal Color");
    }
}
 
public class Test{    
    public static void main(String[] args){
        Color c1 = Color.RED;
        System.out.println(c1);
        c1.colorInfo();
    }
}
```

运行结果

![image-20220825104145016](https://cdn.jsdelivr.net/gh/yangxiaozhao/TyporaImg@master/img202302281104377.png)

## Vector类

Vector 类实现了一个动态数组。Vector 主要用在事先不知道数组的大小，或者是需要一个可以改变大小的数组的情况

> Vector 类支持 4 种构造方法：
>
> ```java 
> Vector()                          //创建一个默认的向量，默认大小为 10
> Vector(int size)                 //创建指定大小的向量
> Vector(int size,int incr)       //创建指定大小的向量，并且增量用 incr 指定。增量表示向量每次增加的元素数目
> Vector(Collection c)           //创建一个包含集合 c 元素的向量
> ```

用例

```Java
import java.util.Enumeration;
import java.util.Vector;

public class vector {
   public static void main(String args[]) {
      Vector v = new Vector(3, 2);
      System.out.println("Initial size: " + v.size());           // v.size() : 返回Vector中的组件数
      System.out.println("Initial capacity: " +v.capacity());       //v.capacity(): 返回Vector的当前容量
      v.addElement(new Integer(1));
      v.addElement(new Integer(2));
      v.addElement(new Integer(3));
      v.addElement(new Integer(4));
      System.out.println("Capacity after four additions: " +v.capacity());
      System.out.println("First element: " +(Integer)v.firstElement());
      System.out.println("Last element: " +(Integer)v.lastElement());
      if(v.contains(new Integer(3)))
         System.out.println("Vector contains 3.");
      Enumeration vEnum = v.elements();                   // v.elements() : 返回此向量组件的枚举
      System.out.println("\nElements in vector:");
      while(vEnum.hasMoreElements())
         System.out.print(vEnum.nextElement() + " ");
      System.out.println();
   }
}
```

运行结果

![image-20220825104436687](https://cdn.jsdelivr.net/gh/yangxiaozhao/TyporaImg@master/img202302281115459.png)

## String类

1、charAt() : char charAt（int index），返回index索引处的字符

```java
String x="good";
System.out.println(x.charAt(3));   //输出'd'
```



2、concat() : String concat(String s) , 将字符串s加到调用该方法的字符串尾部

```java
String x="good";
System.out.println(x.concat(" idea!"));    /输出good idea!
```

3、equals() 和 equalsIgnoreCase() , 比较字符串是否相同，后者忽略大小写

```java
String x="good";
x.equals("good");                  //ture
x.equals("GOOD");                  //false
x.equalsIgnoreCase("good");        //true
x.equalsIgnoreCase("GOOD");        //true
```

4、endsWith() 和startsWith() , 判断字符串是否以指定的参数字符串结尾||开始

```java
String x="this is a good idea!";
boolean a=x.endsWith("idea!")      //true
boolean b=x.startsWith("that")     //false
```

5、indexOf() 和 lastIndexOf() , 查找指定字符串在调用该方法的字符串中首次（最后）出现的位置，若字符串不存在则返回-1

```Java
String s="hello";
System.out.print(s.indexOf("l"));    //输出2
System.out.print(s.indexOf("w"));    //输出-1
System.out.print(s.indexOf("l"));    //输出3
System.out.print(s.indexOf("w"));    //输出-1
```

String 对象是不可变的，每一个类似修改String对象的操作实际都是创建了新对象，所以大规模拼接String对象等操作惠产生大量垃圾，消耗内存且占用时间，故引入StringBuilder类和StringBuffer类

> StringBuilder是在Java SE5.0中引人的，在此之前Java使用的是StringBuffer类，二者的区别是: StringBuilder 类是单线程的，StringBuffer 是多线程安全的，支持并发访问，因此StringBuffer的开销会大些。所以，在非多线程的情况下，应该优先选择
> StringBuilder类。下 面以StringBuilder为例，进行介绍StringBuffer的使用

## StringBuilder类的常用方法

1、append() : append(String s) 、append(int i) 、append(boolean b)

将指定数据转换为字符串后追加到调用该方法的字符串后面

2、insert() : insert(int i,String s)

插入操作，插入位置由 i 确定

3、delete() : delete(int s,int e)

删除从索引 i 到索引 e 的子串

4、reverse() : reverse()

将字符串逆置

## for each 循环

> 格式：
>
> for(数据类型 变量 ：数组（集合））{
>
> }

```
int[] a= {1,2,3,4,5};
for(int i:a) {
	System.out.print(i);
}                                   //输出 12345
```

## List类

1、void add(int index , Object element)

在指定位置 index 上插入元素 element

2、Object get(int index)

返回指定位置 index 上的元素

3、Object remove(int index)

删除指定位置 index 上的元素

4、Object set(int index , Object element)

用元素element替换index处的元素，并返回旧元素

5、int indexOf(Object obj) 和 int lastIndexOf(Object obj) ,

查找指定元素在列表中首次（最后）出现的位置，若元素不存在则返回-1

```java
List list=new ArrayList();
// ArrayList 是 List 的实现类
```

## 异常  

> 异常体系的根为Throwable，其有两个子类：Error和Exception

### Error

程序无法从error修复，故不必处理该类异常

### Exception

> exception分为两类：RuntimeException（运行时异常，也称未检查异常）和非RuntimeException（编译时异常，也称已检查异常）

#### 一、常见的RuntimeException：

1， ClassCastException        类型强制转换异常，当试图将对象强制转换为不是实例的子类时，抛出该异常

> Object x = new Integer(0);
> System.out.println((String)x);

2，ArithmeticException             算术异常类，一个整数“除以零”时，抛出异常

> int a=5/0;

3, NullPointerException               空指针异常类，当应用程序试图在需要对象的地方使用 null 时，抛出异常

> String s=null;
> int size=s.size();

4, IndexOutOfBoundsException       指示索引或者为负，或者超出字符串的大小，抛出异常;

> StringIndexOutOfBoundsException
> "hello".indexOf(-1);

5，ArrayIndexOutOfBoundsException     数组下标越界异常，当使用的数组下标超出数组允许范围时，抛出该异常

6，IllegalArgumentException参数异常
抛出的异常表明向方法传递了一个不合法或不正确的参数

7，NumberFormatException数字格式异常
当试图将一个String转换为指定的数字类型，而该字符串确不满足数字类型要求的格式时，抛出该异常

8，ClassNotFoundException找不到类异常
当应用试图根据字符串形式的类名构造类，而在遍历CLASSPAH之后找不到对应名称的class文件时，抛出该异常

9，ArrayStoreException数组存储异常
当向数组中存放非数组声明类型对象时抛出

#### 二、常见的非RuntimeException

1，NoSuchMethodException           方法未找到异常

2，IOException                                   输入输出异常

3，EOFException                                文件已结束一场

4，FileNotFoundException               文件未找到异常

5，NumberFormatException           字符串转换为数字异常

6，SQLException                                操作数据库异常

### try-catch-finally语句

1、try语句：放置可能出现异常的代码，这段代码可能会产生一个或多个异常，这些异常由后面的catch负责捕获、处理，所以一个try语句可以跟一个或多个catch语句

2、catch语句：每个catch语句捕获处理一个异常，异常发生时，程序会中断正常流程，离开try去执行catch中的程序

3、finally语句：该语句为可选，一旦存在，无论是否出现异常，finally都要被执行

### throws

若当前方法不知道如何处理异常，可以使用throws声明将异常抛出，交给当前方法的上一层调用者

```java
public static void main(String[] abs) throws ParseException
    …………
}                                                         //若出现ParseException异常，其将被抛给JVM
```

### 自定义异常与throw

1、自定义异常要有能标识异常状况的名字，且要继承Exception类，其内部至少有两个构造方法：无参构造、带String参数的带参构造，将此字符串传递给父类Exception的相同构造方法

```Java
public class EmailExistException extends Exception{
    public EmailExistException(){}
    public EmailExistException (String msg){
        super(msg);
    }
}
```

2、自定义异常要用throw自行抛出，throw抛出的不是类，而是对象，throw一次只能抛出一个对象

```java
public static void main(String[] abs) {
		Scanner scn=new Scanner(System.in);
		 System.out.print("请输入新建邮箱：");
		    String email=scn.next();
		    try{
		        if(email.equalsIgnoreCase("934783419@qq.com"))
		        	throw new EmailExistException("该邮箱已存在");
		    }catch(EmailExistException e) {
		    	e.printStackTrace();
		    }
}
```

![image-20220825104642543](https://cdn.jsdelivr.net/gh/yangxiaozhao/TyporaImg@master/img202302281115804.png)

## 图形用户界面（GUI)

### AWT组件与应用

> java构建GUI使用Java.awt 下的AWT类和 java.swing下的Swing类。AWT依靠本地方法实现，运行方法快，但功能相对较少，Swing是基于AWT的java程序，功能丰富，但运行较慢

#### AWT的组成

1、组件（Component）

组件分为基本组件和容器，基本组件不能再容纳其他组件

2、容器（Container）

容器本身也是一种组件，但容器具有容纳基本组件和容器的功能

3、布局管理器（LayoutManager）

#### AWT的容器

> AWT 主要提供了两种容器类型：Window（窗口）和Panel（面板），Window可独立存在，Panel不能独立存在，用于容纳其他组件，并存在于容器中

###### 1、Window

> 屏幕上显示窗口的容器有：Window、Frame（窗体）、Dialog（对话框），其中Frame和Dialog是Window的子类

| **Window** | 没有边界、标题栏、菜单栏，且大小不可调整，主要是作为父类存在 |
| ---------- | ------------------------------------------------------------ |
| **Frame**  | **有边界、标题栏、菜单栏，大小可以调整**                     |
| **Dialog** | **有边界、标题栏，大小可以调整，不支持菜单栏**               |

（1）Frame的构建方法：

Frame() : 构造一个新的、最初不可见的Frame对象

Frame(String title) : 创建一个新的、最初不可见的、具有指定标题的Frame对象

（2）Dialog的构建方法：

Dialog(Frame owner) : 构造一个最初不可见的、无模式的Dialog，它指定Dialog的所有者Frame和一个空标题

Dialog(Frame owner, String title) : 构造一个最初不可见的、无模式的Dialog，它指定Dialog的所有者Frame和标题

Dialog(Frame owner, String title , boolean modal) : 构造一个最初不可见的Dialog，它指定Dialog的所有者Frame和标题和模式

（3）设置Frame和Dialog的大小和可见性

> 设置大小：
>
> setSize（int width, int height）: 设置大小
>
> setBounds(intx, inty, intwidth, intheight) :  设置左上角的位置和大小
>
> pack() : 自动确定大小，确保容器中的组件与容器大小相适应
>
> > 设置可见性（Frame和Dialog默认不可见）：
> >
> > setVisible(true) : 设置可见

```java
public class Test {
	public static void main(String[] abs) {
		Frame frame=new Frame("Frame窗口");
		frame.setBounds(50,50,300,120);
		frame.setVisible(true);
		    }
}
```

![image-20220825104736326](https://cdn.jsdelivr.net/gh/yangxiaozhao/TyporaImg@master/img202302281115152.png)

###### 2、Panel

panel是一个同样的容器，代表一个区域，这个区域可以容纳其他组件。它没有边框，不能移动，不能改变大小，不能作为顶层容器的容器，不能独立存在。只能嵌套在其他容器（Window或Panel）内部，用来分割大容器的布局，作为大容器的一部分实现各区域的单独管理，从而设计出比较复杂的容器结构。若要使Pandel可见，必须将其添加到Window中。

```java
public class Test {
	public static void main(String[] abs) {
		Frame frame=new Frame("Frame窗口");     //左上角的标题
		frame.setBounds(50,50,300,120);        // 50,50为窗口左上角距页面左上角的距离，300，120为窗口的大小
		Panel panel=new Panel(); 
		panel.add(new Label("name"));    
		panel.add(new TextField(20));
		frame.add(panel);
		frame.setVisible(true);
		    }
}
```

![image-20220825105538751](https://cdn.jsdelivr.net/gh/yangxiaozhao/TyporaImg@master/img202302281115272.png)

#### 布局管理器

> 布局管理器负责容器内的组件的大小、位置、顺序、间隔等，每一个容器都会引用一个布局管理器实例，通过它自动进行组件的布局管理。一个容器被创建后会有相应的默认布局管理器。Window、Frame、Dialog的默认布局管理器是BorderLayout，Panel的默认布局管理器FlowLayout。除此之外还有GridLayout和GardLayout。

###### 1、BorderLayout

边界布局BorderLayout将容器分为五个区域：BorderLayout.EAST、BorderLayout.WEST、BorderLayout.SOUTH、BorderLayout.NORTH、BorderLayout.CENTER 。向BorderLayout布局的容器中添加组件时，要指定位置，否则默认中间。BorderLayout的构造方法：

```
BorderLayout(): 构造一个组件之间没用间距的布局
BorderLayout(inthgap,intvgap):构造一个具有指定组件距的布局
```

BorderLayout的一个区域只能放置一个组件，后添加的组件会覆盖原组件，若想放置多个组件，需将其用Panel装载，再将Panel填至指定区域

###### 2、FlowLayout

流式布局FlowLayout按照组件添加次序顺序排放组件（从左到右，从上到下，一个接一个放置），FlowLayout的构造方法：

```
FlowLayout(): 使用默认的对齐方式和间距（居中对齐、水平和垂直间隔5像素）
FlowLayout(align): 指定对其方式（FlowLayout.CENTER、FlowLayout.LEFT、FlowLayout.RIGHT）  //用括号里的替换aligin
FlowLayout(align,inthgap,intvgap): 指定对齐方式和间距
```

###### 3、GridLayout

网格布局GridLayout将容器分成等长等大的若干网格，每个网格放置一个组件。默认从左到右，从上到下依次添加组件，GridLayout中组件的大小有所处区域决定，每个组件占满所处区域。GridLayout的构造方法：

```
GridLayout(): 所有组件分布在一行（每个组件占一列）
GridLayout(int rows,int cols): 指定行数、列数，使用默认行距列距
GridLayout(int rows,int cols,inthgap,intvgap): 指定行数、列数、行距、列距
```

###### 4、GardLayout

卡片布局GardLayout将容器中的多个组件看成一叠卡片（组件重叠），在任何时候只有其中一张是可见的，这张卡片占据容器的整个区域。GardLayout的构造方法：

```
GardLayout(): 创建默认的卡片布局管理器
GardLayout(inthgap,intvgap): 指定卡片与容器左右边距和上下边距
```

> first（Container target) 、last（Container target) 、previous（Container target) 、next（Container target) 等方法显示容器target中的指定组件，show（Container target, String name）显示target中指定名字的组件

#### 布局管理器的使用方法

> 以Panel，FlowLayout为例

![image-20220320170756918](C:\Users\杨小照\AppData\Roaming\Typora\typora-user-images\image-20220320170756918.png)

### GUI实例--计算器

```java
import java.awt.*;

public class Test {
	public static void main(String[] abs) {
		Frame frame=new Frame("计算器");
		TextField field=new TextField(20);
		Button[] button=new Button[20];
		String str="C^!±789×456/123-.0=+";
		for(int i=0;i<str.length();i++) {
			button[i]=new Button(str.substring(i, i+1));
		}
		Panel northPanel=new Panel();
		northPanel.add(field);
		Panel centerPanel=new Panel();
		GridLayout grid=new GridLayout(5,4,2,2);
		centerPanel.setLayout(grid);
		for(int i=0;i<button.length;i++) {
			centerPanel.add(button[i]);
		}
		frame.add(northPanel,BorderLayout.NORTH);
		frame.add(centerPanel,BorderLayout.CENTER);
		frame.pack();
		frame.setLocation(300,200);
		frame.setVisible(true);
	}
}
```

![image-20220825105638058](https://cdn.jsdelivr.net/gh/yangxiaozhao/TyporaImg@master/img202302281116305.png)

### 事件处理

> 事件源（EventSource）：每个可以触发事件的组件
>
> 事件对象（ActionEvent）：发生的事件会被封装为事件对象，事件对象中包含事件源对象
>
> 事件监听器（EventListencer）：每一种事件对应专门的事件监听器，监听器负责观察事件的发生并处理事件
>
> > 事件源与事件监听器之间要通过 ” 注册 “ 这个动作发生关联，即为一个事件源指定一个或多个事件监听器。被指定的事件              监听器将观察其管辖范围内的事件是否在该事件源上发生，事件源一但发生该事件，监听器立即调用其定义的事件处理器（EventHandler）做出响应   

```java
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.TextEvent;
import java.awt.event.TextListener;

public class Test {
	Frame frame=new Frame("自言自语");          //定义全局组件
	TextArea area=new TextArea();
	TextField field=new TextField(26);
	Button button=new Button("发送");
    
	public Test() {                             //在构造方法中完成组件拼接
		area.setFont(new Font("Times New Roman",Font.BOLD,14));     //setFont为设置字体格式
		area.setEditable(false);
		Panel CenterPanel=new Panel();
		Panel SouthPanel=new Panel();
		CenterPanel.add(area);
		SouthPanel.add(field);
		SouthPanel.add(button);
		frame.add(SouthPanel,BorderLayout.SOUTH);
		frame.add(CenterPanel,BorderLayout.CENTER);
	}
	
	private class FieldButtonAction implements ActionListener{     //文本框和按钮的监听器
		public void actionPerformed(ActionEvent e) {
			area.append(field.getText()+"\n");
			field.setText("");
		}
	}
	
	private class FiledChangeAction implements TextListener{      //文本框的监听器
		public void textValueChanged(TextEvent e) {
			if(field.getText().equals("hehe")){
				area.append("\\(^o^)/\n");
				field.setText("");
			}
		}
	}
	public void addEventHandler() {                          //为事件源注册事件监听器
		button.addActionListener(new FieldButtonAction());
		field.addActionListener(new FieldButtonAction());
		field.addTextListener(new FiledChangeAction());
	}
	
	public static void main(String[] abs) {                   //主函数
		Test test=new Test();
		test.addEventHandler();
		test.frame.pack();
		test.frame.setVisible(true);
	}
}

```

#### 适配器实现监听

> 有些事件监听器有很多需要实现的方法，如WindowListener监听器有七个方法。但某一个应用未必需要处理所有的方法，此时可以使用事件适配器，事件适配器是事件监听器的空实现，即实现了监听器的所有方法，但方法体内没用任何代码，需要事件监听器时，可以继承对应事件监听器的事件适配器，有针对的改写相应的方法
>
> > WindowListener对应的适配器是WIndowAdapter，其他监听器类似

```java
private class WindowClose extends WindowAdapter{
		public void windowClosing(WindowEvent e) {
			System.exit(0);
		}
	}
public void show() {
	Frame frame=new Frame("AdapterTest");
	frame.setBounds(300, 200, 200, 200);
	frame.setVisible(true);
	frame.addWindowListener(new WindowClose());
}
public static void main(String[] abs) {
		new Test().show();
}
```

### GUI实例-计算器（改进）

```java
package calculator;
import java.awt.*;
import java.awt.event.*;
public class Calculator {
	Frame frame;
	TextField field;
	Button[] button;
	double op1=0,op2=0;
	String operator="";
	boolean flag=true;
	public Calculator() {            //构造方法
		frame=new Frame("计算器");
		field=new TextField(25);
		button=new Button[20];
		String str="C^!±789×456/123-.0=+";
		for(int i=0;i<str.length();i++) {
			button[i]=new Button(str.substring(i, i+1));
		}
	}
	
	public static void main(String[] abs) {       //主方法
		new Calculator().Show();
	}
	
	public void init() {                     //创建组件
        Panel northPanel=new Panel();
		northPanel.add(field);
		Panel centerPanel=new Panel();
		GridLayout grid=new GridLayout(5,4,2,2);
		centerPanel.setLayout(grid);
		for(int i=0;i<button.length;i++) {
			centerPanel.add(button[i]);
		}
		frame.add(northPanel,BorderLayout.NORTH);
		frame.add(centerPanel,BorderLayout.CENTER);
	}
	
	public void Show() {                     //显示计算器
		init();
		frame.setBounds(300,200,300,280);
		frame.setVisible(true);
		addEventHandler();
	}
	
	public class WindowClose extends WindowAdapter{        //监听关闭键
		public void windowClosing(WindowEvent e) {
			System.exit(0);
		}
	}
	
	public class CalculatorAction implements ActionListener{      //监听按钮
		public void actionPerformed(ActionEvent e) {
			String command=e.getActionCommand();
			if("0123456789.".indexOf(command)!=-1) {
				if(flag) {
					field.setText(command);
				}else {
					field.setText(field.getText()+command);
				}
				flag=false;
			}
			else if("+-×/^!".indexOf(command)!=-1) {
					op1=Double.valueOf(field.getText());
					field.setText("");
					operator=command;
			}
			else if("=".indexOf(command)!=-1) {
				double op=0;
				String text=field.getText();
				if(text!=null&&op1==0) {
				}
				else if(text.length()>0) {
					op2=Double.valueOf(text);
					if(operator.equals("+")) {
						op=op1+op2;
					}
					else if(operator.equals("-")) {
						op=op1-op2;
					}
					else if(operator.equals("×")) {
						op=op1*op2;
					}
					else if(operator.equals("/")) {
						op=op1/op2;
					}
					else if(operator.equals("^")) {
						op=Math.pow(op1, op2);
					}
					field.setText(String.valueOf(op));
				}else {
					op=1;
					for(int i=2;i<=op1;i++) {
						op=op*i;
					}
					field.setText(String.valueOf(op));
				}
				flag=true;
			}
			else if("C".indexOf(command)!=-1) {
				op1=op2=0;
				operator="";
				flag=true;
				field.setText("");
			}
			else {   
				warning();
			}
		}
	}
	
	public void warning() {
	Frame f=new Frame("FBI Warning !");
	f.setBounds(350,250,260,100);
	TextField t=new TextField("运算符"+"±"+"尚未定义！",11);
	t.setEditable(false);
	Panel p=new Panel();
	p.add(t,BorderLayout.CENTER);
	f.add(p);
	f.setVisible(true);
	f.addWindowListener(new WindowClose());
	}
	
	public void addEventHandler() {                         //实现监听
		frame.addWindowListener(new WindowClose());
		for(int i=0;i<button.length;i++) {
			button[i].addActionListener(new CalculatorAction());
		}
	}
}
```

### Swing组件

Swing开发GUI不依赖本地平台的GUI，不必采用各平台GUI的交集，因此可以提供大量图形界面组件，远超于AWT，故实际开发中基本通过Swing组件开发

- Swing对AWT组件都提供了相应的实现，通常在AWT组件名前加上＂Ｊ＂就变成了对应的Swing组件。
- 大部分Swing组件都是JComponent抽象类的子类，JComponent是java.awt.Component的子类，所以理论上Swing的所有组件都可以作为容器使用。
- JPanel没有从Panel下继承，而是被Swing重写，位于swing包下，含义与用法不变
- JWindow、JFrame、JDialog直接继承了AWT组件



Swing中的常用组件：

- 顶层容器：JFrame、JDialog、JWindow
- 中间容器：JPanel、JScrollPane、JMenuBar、JToolBar
- 基本组件：JButton、JComboBox、JList、JMenu、JTree
- 可编辑信息的显示组件：JTextField、JTextArea、JPasswordField、JTable
- 不可编辑信息的显示组件：JLabel、JToolTip
- 特殊对话框组件：JFileChooser、JColorChooser

Swing的事件处理机制与AWT相同，只是Swing中又提供了更多的事件监听器

### 综合实践-用户管理系统与常用Swing组件的应用

```java
/****
        待做
****/
```

## 多线程

进程与线程

- 对于一个CPU而言，操作系统一次只能处理一个程序
- 操作系统中运行的每一个任务对应一个进程，进程是操作系统进行资源分配和调度的一个独立单元
- 线程是进程的执行单元，线程在进程中是独立的、并发的执行流。当进程被初始化后，主线程就被创建了，主线程从程序入口main() 方法开始运行
- 进程内可以创建多个线程，每个线程互相独立

### 线程的概念

每个线程拥有自己独立的程序计数器、栈内存创建新线程时这些数据区会一同被创建

程序计数器用于记录每个线程执行到的指令位置；栈内存区保存线程中每个被调用方法的相关性（局部变量、操作数等）

线程不独立拥有进程资源（堆内存区、方法区）每个线程与父进程的其他线程共享该进程资源

操作系统可以同时执行多个任务，每个任务就是进程；进程中可以同时执行多个任务，这些子任务就是线程

创建进程需要为其分配独立的内存单元及相关资源，相较而言线程创建简单的多

进程之间不能内存共享，线程之间内存共享则非常容易

并行指同一时刻有多个指令在CPU上同时执行，只有多核处理器的系统才存在并行

并发指同一时刻只能有一条指令执行，多个进程指令被迅速地轮换



### 线程的创建和执行

线程是java.lang.Thread的实例，常用方法如下：

- void run(): 该方法需要被重写，代表了线程的执行体。
- void start():  启动调用该方法的线程（由JVM调用）
- **static** Thread currentThread():  静态方法，返回当前正在运行的线程对象的引用
- final StringgetName(): 获取线程的名称。
- **static** void sleep ( long millis ) throws InterruptedException: 在指定的毫秒数内让当前正在运行的线程休眠。
- **static** void yield(): 暂停当前正在运行的线程，让出CPU资源。
- final intgetPriority():  获取线程的优先级。
- final void join() throws InterruptedException: 令当前线程“ 加入到”调用join()方法的线程的尾部。
  **创建线程有两种方式: 继承Thread类和实现Runnable接口。**

#### 继承Thread类创建线程

1. 定义Thread的子类，重写run() 方法，run() 方法的方法体代表了线程需要完成的任务
2. 创建线程对象
3. 线程对象调用start() 类启动该线程
   运行结果

```java
public class FThread extends Thread {
	public void run() {
		for(int i=0;i<5;i++) {
			System.out.println(this.getName()+":"+(char)(i+'A'));
			for(int k=0;k<400000000;k++);
		}
	}
	public static void main(String[] abs) {
		Thread t1=new FThread();
		Thread t2=new FThread();
		for (int i=0;i<10;i++) {
			System.out.println(Thread.currentThread().getName()+":"+i);
			for(int j=0;j<500000000;j++);
			if(i==1) t1.start();
			if(i==2) t2.start();
		}
	}
}
```

> 根据程序，i=1时t1线程启动，i=2时t2线程启动，但实际运行结果说明线程启动后不一定立刻执行，因为线程的何时执行不是用户控制的，在每个线程内事件以可预测的顺序发生，但是不同的线程的操作会按照不可预测的方式混杂。若多次运行程序，可能得到不同的输出结果。

多线程程序只有当所有线程都结束时程序才会结束

#### 实现Runnable接口创建线程

实现java.lang.Runnable 接口，Runnable接口只有一个run() 方法。

Runnable接口与Thread类之间没有继承关系，所以不能直接赋值。

需要一个Thread实例，实现对Runnable对象的封装，即：Thread提供线程的支持，Running实现类提供线程执行体

```java
public class SThread implements Runnable {
	public void run() {
		for(int i=0;i<5;i++) {
			System.out.println(Thread.currentThread().getName()+":"+i);
		}
	}
	public static void main(String[] abs) {
		Runnable target =new SThread();
		Thread t1=new Thread(target);
	    Thread t2=new Thread(target);
		for (int i=0;i<10;i++) {
			System.out.println(Thread.currentThread().getName()+":"+i);
			for(int j=0;j<500000000;j++);
			if(i==1) t1.start();
			if(i==2) t2.start();
		}
	}
}
```

运行结果

![image-20220825110320440](https://cdn.jsdelivr.net/gh/yangxiaozhao/TyporaImg@master/img202302281116756.png)

### 线程的状态和生命周期

线程生命周期包括：**新建、就绪、运行、阻塞、死亡**等五个状态

#### 新建和就绪状态

新建状态（new）：创建Thread实例后，只是知道了要调用哪个run()方法，这个Thread对象与其他的 Java对象没有区别，这个状态称   为”新建“

就绪（runnable）：使用 start() 方法启动线程，为线程创建属于它的内存资源，这样，线程就进入”就绪“状态

#### 运行状态（running）

处于就绪状态的线程获得CPU时间片，开始执行run()方法中的线程执行体。线程就进入运行状态（running）

系统会给每个可执行的线程一个时间片来处理任务，时间片用完后线程被换下，选择下一个线程时，系统会考虑线程的优先级

如果一个线程的执行体比较长，无法在一个时间片内执行完毕，则它在运行过程中会被中断，以使其他线程获得执行机会。线程因失去时间片而中断会返回runnable状态

running状态的线程可以调用yield()方法主动放弃执行，从running状态进入runnable状态

#### 阻塞状态（blocked）

睡眠、资源阻塞、等待三种状态的组合体，阻塞状态（blocked）的特点：线程依然是活的，但当前缺少运行它的条件，不可运行，如果发生某个特定事件，它将返回runnable状态

睡眠：线程调用sleep()方法睡眠一段时间

资源阻塞：线程在等待一种资源，如线程调用了阻塞式的I/O方法（等待输入流等）

等待：线程调用wait()方法后等待其他线程的唤醒通知

线程阻塞后，其他线程可获得执行机会，被阻塞的线程接触阻塞后，返回runnable状态，必须重新等待线程再次被调度

对应情况接触阻塞的特定事件

睡眠：睡眠时间到

资源阻塞（线程调用了阻塞式的I/O方法）：阻塞式I/O方法已返回

等待：收到其他线程发出的notify通知

#### 死亡状态（dead）

线程的run()方法执行结束，线程正常结束；线程执行过程抛出一个未捕获的异常或错误，线程异常结束

结束后线程处于dead状态，此时线程可能还是活得Thread对象，但它不可再执行，若dead状态的Thread对象再次调用start()方法，则会出现运行时异常**IllegalThreadStateException**

> 下图来自廖雪峰老师JAVA教程
>
> ![image-20230401103445222](https://cdn.jsdelivr.net/gh/yangxiaozhao/TyporaImg@master/img202304011034315.png)

### 中断线程

1. 中断一个线程：在其他线程中对目标线程调用`interrupt()`方法，目标线程需要反复检测自身状态是否是interrupted状态，如果是，就立刻结束运行。

2. 如果线程处于等待状态，例如，在**main线程**中调用**t.join()**会让main线程进入等待状态，此时，如果对main线程调用**interrupt()**，join()方法会立刻抛出InterruptedException，因此，目标线程只要捕获到join()方法抛出的InterruptedException，就说明有其他线程对其调用了interrupt()方法，通常情况下该线程应该立刻结束运行。

   ```Java
   public class Main {
       public static void main(String[] args) throws InterruptedException {
           Thread t = new MyThread();
           t.start();
           Thread.sleep(1000);
           t.interrupt(); // 中断t线程，但是此时t线程应该正处在等待hello线程的状态（hello。join()），抛出										InterruptedException异常
           t.join(); // 等待t线程结束
           System.out.println("end");
       }
   }
   
   class MyThread extends Thread {
       public void run() {
           Thread hello = new HelloThread();
           hello.start(); // 启动hello线程
           try {
               hello.join(); // 等待hello线程结束
           } catch (InterruptedException e) {
               System.out.println("interrupted!");
           }
           hello.interrupt();   // 若无此句，t线程中断后hello线程依然会持续运行
       }
   }
   
   class HelloThread extends Thread {
       public void run() {
           int n = 0;
           while (!isInterrupted()) {
               n++;
               System.out.println(n + " hello!");
               try {
                   Thread.sleep(100);
               } catch (InterruptedException e) {
                   break;
               }
           }
       }
   }
   ```

3. **volatile关键字**解决的是可见性问题：当一个线程修改了某个共享变量的值，其他线程能够立刻看到修改后的值。

### 守护线程



## 日志

1. Java标准库内置了日志包`java.util.logging`（JDK Logging）

   - 日志级别（SEVERE、WARNING、INFO、CONFIG、FINE、FINER、FINEST）
   - 默认级别为INFO
   - INFO级别以下的日志不会被打印

2. Commons Logging是一个第三方日志库

   > 默认情况下，Commons Loggin自动搜索并使用Log4j（另一个日志系统），如果没有找到Log4j，再使用JDK Logging

   - 日志级别（FATAL、ERROR、WARNING、INFO、DEBUG、TRACE）
   - 默认级别为INFO

   > 如果在静态方法中引用`Log`，通常直接定义一个静态类型变量

   ```java
   // 在静态方法中引用Log:
   public class Main {
       static final Log log = LogFactory.getLog(Main.class);
   
       static void foo() {
           log.info("foo");
       }
   }
   ```

   > 在实例方法中引用`Log`，通常定义一个实例变量：

   ```java
   // 在实例方法中引用Log:
   public class Person {
       protected final Log log = LogFactory.getLog(getClass());
   
       void foo() {
           log.info("foo");
       }
   }
   ```

   - 推荐使用==LogFactory.getLog(getClass())==而非==LogFactory.getLog(Person.class)==（便于子类继承）

3. Log4j是一种非常流行的日志框架，它是一个组件化设计的日志系统

![image-20230228105950644](https://cdn.jsdelivr.net/gh/yangxiaozhao/TyporaImg@master/img202302281059694.png)

> 当我们使用Log4j输出一条日志时，Log4j自动通过不同的Appender把同一条日志输出到不同的目的地。输出日志的过程中，通过Filter来过滤哪些log需要被输出，哪些log不需要被输出（例如仅输出“ERROR”级别的日志）。最后，通过Layout来格式化日志信息（例如自动添加日期、时间等信息）。

==**Commons Logging负责充当日志API，Log4j负责日志底层**==

## 注解

> 常见注解

- @Override	重写方法
- @Deprecated      不推荐程序员使用    、
- @SuppressWarings(str)   抑制编译警告
  - 该注释需要添加参数 

#### 元注解（*注解其他注解*）

1. **@Target** ：用于描述注解的使用范围(即:被描述的注解可以用在什么地方)
2. **@Retention**：表示需要在什么级别保存该注释信息。用于描述注解的生命周期
   (SOURCE< CLASS< **RUNTIME**)
3. @Document：说明该注解将被包含在javadoc中
4. @Inherited：说明子类可以继承父类中的该注解

#### 自定义注解

关键字：@interface

> public @interface 注解名 {  定义内容 }

![image-20230412234330596](https://cdn.jsdelivr.net/gh/yangxiaozhao/TyporaImg@master/img202304122343717.png)

```java
public class test{
	@MyAnnotation(name="aaa",{"ncepu"})
    public void test(){}
}

@Target({ElementType.TYPE,ElementType.METHOD})
@Retention(RetentionPolicy.RUNTIME)
@interface MyAnnotation{
    String name(); // 参数：参数类型+参数名()
    int age() default 0;
    int id() default -1; //如果默认值为-1，代表不存在
    String[] schools();
}
```



## 反射

### Class类

#### Class与class

每加载一种 **class**，JVM就为其创建一个 **Class** 类型的实例，并关联起来

```java
Class cls=new Class(String);
```

> JVM持有的每个 Class 实例都指向一个数据类型（class 或 interface）

![](https://cdn.jsdelivr.net/gh/yangxiaozhao/TyporaImg@master/img202303091631874.png)

#### Class的方法

##### 获取Class实例

1. 直接通过一个`class`的静态变量`class`获取：

   ```java
   Class cls=String.class;
   ```

2. 通过实例变量提供的`getClass()`方法获取：

   ```java
   String str="Hello";
   Class cls=str.getClass();
   ```

3. 如果知道一个`class`的完整类名，可以通过静态方法`Class.forName()`获取：

   ```java
   Class cls = Class.forName("java.lang.String");
   ```

   > 获取Class实例后，可直接通过该`Class`实例来创建对应类型的实例：
   >
   > ```java
   > Class cls = String.class;
   > String s = (String) cls.newInstance();		//相当于String s=new String();
   > ```
   >
   > 通过`Class.newInstance()`可以创建类实例，它的局限是：只能调用`public`的无参数构造方法。

##### 访问字段

> 对任意的一个`Object`实例，只要我们获取了它的`Class`，就可以获取它的一切信息

- Field getField(name)：根据字段名获取某个public的field（包括父类）
- Field getDeclaredField(name)：根据字段名获取当前类的某个field（不包括父类）
- Field[] getFields()：获取所有public的field（包括父类）
- Field[] getDeclaredFields()：获取当前类的所有field（不包括父类）

```Java
public class Main {
    public static void main(String[] args) throws Exception {
        Class stdClass = Student.class;
        // 获取public字段"score":
        System.out.println(stdClass.getField("score"));
        // 获取继承的public字段"name":
        System.out.println(stdClass.getField("name"));
        // 获取private字段"grade":
        System.out.println(stdClass.getDeclaredField("grade"));
    }
}

class Student extends Person {
    public int score;
    private int grade;
}

class Person {
    public String name;
}

/***
结果如下
public int lanqiao.Student.score
public java.lang.String lanqiao.Person.name
private int lanqiao.Student.grade
**/
```

- getName()：返回字段名称，例如，`"name"`；
- getType()：返回字段类型，也是一个`Class`实例，例如，`String.class`；
- getModifiers()：返回字段的修饰符，返回值是一个`int`类型，不同的bit表示不同的含义。

```java
// String类的value字段定义
public final class String {
    private final byte[] value;
}

Field f = String.class.getDeclaredField("value");
f.getName(); // "value"
f.getType(); // class [B 表示byte[]类型
int m = f.getModifiers();
Modifier.isFinal(m); // true
Modifier.isPublic(m); // false
Modifier.isProtected(m); // false
Modifier.isPrivate(m); // true
Modifier.isStatic(m); // false
```

- 利用反射拿到字段的一个Field实例后，我们还可以拿到一个实例对应的该字段的值

```Java
public class Main {

    public static void main(String[] args){
        Object p = new Person("Xiao Ming");
        Class c = p.getClass();
        Field f = c.getDeclaredField("name");
        //不加该句会抛出异常，因为name为Person的private字段，Main类无法访问
        f.setAccessible(true);
        Object value = f.get(p);
        System.out.println(value); // "Xiao Ming"
    }
}

class Person {
    private String name;

    public Person(String name) {
        this.name = name;
    }
}
```

> 通过Field实例可以获取到指定实例的字段值，也可以设置字段的值。
>
> > 设置字段值是通过`Field.set(Object, Object)`实现的，其中第一个`Object`参数是指定的实例，第二个`Object`参数是待修改的值

#### 调用方法

- `Method getMethod(name, Class...)`：获取某个`public`的`Method`（包括父类）
- `Method getDeclaredMethod(name, Class...)`：获取当前类的某个`Method`（不包括父类）
- `Method[] getMethods()`：获取所有`public`的`Method`（包括父类）
- `Method[] getDeclaredMethods()`：获取当前类的所有`Method`（不包括父类）

- `getName()`：返回方法名称，例如：`"getScore"`；
- `getReturnType()`：返回方法返回值类型，也是一个Class实例，例如：`String.class`；
- `getParameterTypes()`：返回方法的参数类型，是一个Class数组，例如：`{String.class, int.class}`；
- `getModifiers()`：返回方法的修饰符，它是一个`int`，不同的bit表示不同的含义。

```Java
public class Main {
    public static void main(String[] args) throws Exception {
        // String对象:
        String s = "Hello world";
        // 获取String substring(int)方法，参数为int:
        Method m = String.class.getMethod("substring", int.class);
        // 在s对象上调用该方法并获取结果:
        String r = (String) m.invoke(s, 6);
        // 打印调用结果:
        System.out.println(r);
    }
}
```

#### 调用构造方法

> 通过反射创建实例，可以用Class.newInstance()方法，但是此方法只能调用该类的 *public无参数构造方法*

==**import java.lang.reflect.Constructor;**==

- `getConstructor(Class...)`：获取某个`public`的`Constructor`；
- `getDeclaredConstructor(Class...)`：获取某个`Constructor`；
- `getConstructors()`：获取所有`public`的`Constructor`；
- `getDeclaredConstructors()`：获取所有`Constructor`。

> 调用非public的Constructor时，必须首先通过setAccessible(true)设置允许访问

```Java
public class Main {
    public static void main(String[] args) throws Exception {
        // 获取构造方法Integer(int):
        Constructor cons1 = Integer.class.getConstructor(int.class);
        // 调用构造方法:
        Integer n1 = (Integer) cons1.newInstance(123);
        System.out.println(n1);

        // 获取构造方法Integer(String)
        Constructor cons2 = Integer.class.getConstructor(String.class);
        Integer n2 = (Integer) cons2.newInstance("456");
        System.out.println(n2);
    }
}
```

#### 获取继承关系

1. 获取Class对象的三种方式

   ```java
   Class cls = String.class; // 获取到String的Class
   
   String s = "";
   Class cls = s.getClass(); // s是String，因此获取到String的Class
   
   Class s = Class.forName("java.lang.String");
   ```

2. 获取父类的Class

   ```Java
   public class Main {
       public static void main(String[] args) throws Exception {
           Class i = Integer.class;
           Class n = i.getSuperclass();
           System.out.println(n);		// Number
           Class o = n.getSuperclass();
           System.out.println(o);		// Object
           System.out.println(o.getSuperclass());		// Null
       }
   }
   ```

3. 获取interface

   >  由于一个类可能实现一个或多个接口，通过Class我们就可以查询到实现的接口类型

   ```Java
   public class Main {
       public static void main(String[] args) throws Exception {
           Class s = Integer.class;
           Class[] is = s.getInterfaces();
           for (Class i : is) {
               System.out.println(i);
           }
       }
   }
   
   /***
   可得Integer实现的接口有
   java.lang.Comparable
   java.lang.constant.Constable
   java.lang.constant.ConstantDesc
   ***/
   ```

   - `getInterfaces()`只返回当前类直接实现的接口类型，并不包括其父类实现的接口类型
   - 获取接口的父接口要用`getInterfaces()`，调用`getSuperclass()`返回的是`null`

### 反射与注解

> 通过反射机制获取注解

```java
import java.lang.annotation.*;
import java.lang.reflect.Field;

// 反射与注解

public class Test2 {
	public static void main(String[] args) throws ClassNotFoundException, NoSuchFieldException, SecurityException {
		Class c=Class.forName("reflection.Student");
		Annotation[] annotations=c.getAnnotations();
		// 输出定义在Student类上的全部注解
		for(Annotation a:annotations)
			System.out.println(a);
		//输出注解的具体value值
		ClassTest classtest=(ClassTest) c.getAnnotation(ClassTest.class);
		System.out.println(classtest.value());
		
		//获得类指定的注解
		Field f=c.getDeclaredField("name");
		FieldTest fieldtest=f.getAnnotation(FieldTest.class);
		System.out.println(fieldtest.colName()+" "+fieldtest.type()+" "+fieldtest.length());
	}
}

@ClassTest("Student")
class Student {
	@FieldTest(colName = "name",type = "String",length = 6)
	private String name;
	
	@FieldTest(colName = "age",type = "int",length = 2)
	private int age;

	public Student(String name, int age) {
		super();
		this.name = name;
		this.age = age;
	}

	public Student() {
		super();
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public int getAge() {
		return age;
	}

	public void setAge(int age) {
		this.age = age;
	}

}

@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@interface ClassTest{
	String value() default "";
}

@Target(ElementType.FIELD)
@Retention(RetentionPolicy.RUNTIME)
@interface FieldTest{
	String colName() default "";
	String type() default "";
	int length() default -1;
}

```

> 运行结果
>
> ![image-20230416095542196](https://cdn.jsdelivr.net/gh/yangxiaozhao/TyporaImg@master/img202304160955306.png)

### 动态代理



## 网络编程

### IP

- **InetAddress类**

``` java
import java.net.InetAddress;
import java.net.UnknownHostException;

// 获取主机地址
public class TestInetAddress {
	public static void main(String[] args) throws UnknownHostException {
		InetAddress ip1=InetAddress.getLocalHost();
		System.out.println(ip1);
		InetAddress ip2=InetAddress.getByName("localhost");
		System.out.println(ip2);
		InetAddress ip3=InetAddress.getByName("10.2.37.213");
		System.out.println(ip3);
	}
}

```

> 输出
>
> ![image-20230417093606572](https://cdn.jsdelivr.net/gh/yangxiaozhao/TyporaImg@master/img202304170936683.png)

### 端口（port）

> Socket：IP+Port

```java
import java.net.InetSocketAddress;

public class TestInetSocketAddress {
	public static void main(String[] args) {
		InetSocketAddress socket1=new InetSocketAddress("127.0.0.1",8080);
		System.out.println(socket1);	
		System.out.println(socket1.getHostName());
		System.out.println(socket1.getPort());
		System.out.println(socket1.getAddress());
	}
}

```

> ![image-20230417102159963](https://cdn.jsdelivr.net/gh/yangxiaozhao/TyporaImg@master/img202304171022015.png)

### 通信协议

**TCP/IP协议簇**

#### TCP通信

1. 服务器端

   ```java
   import java.io.*;
   import java.net.*;
   
   public class TcpServerDemo {
   
   	public static void main(String[] args) {
   		
   		ServerSocket serverSocket = null;
   		Socket socket = null;
   		InputStream is = null;
   		ByteArrayOutputStream baos = null;
   		
   		try {
   			// 服务器地址
   			serverSocket = new ServerSocket(9999);
   			// 等待客户端接入
   			socket=serverSocket.accept();
   			// 读取客户端消息
   			is=socket.getInputStream();
   			// 管道流
   			baos=new ByteArrayOutputStream();
   			byte[] buffer=new byte[1024];
   			int len;
   			while((len=is.read(buffer))!=-1) {
   				baos.write(buffer,0,len);
   			}
   			System.out.println(baos.toString());
   			
   		} catch (IOException e) {
   			// TODO Auto-generated catch block
   			e.printStackTrace();
   		} finally {
   			if(baos!=null) {
   				try {
   					baos.close();
   				} catch (IOException e) {
   					// TODO Auto-generated catch block
   					e.printStackTrace();
   				}
   			}
   			if(is!=null) {
   				try {
   					is.close();
   				} catch (IOException e) {
   					// TODO Auto-generated catch block
   					e.printStackTrace();
   				}
   			}
   			if(socket!=null) {
   				try {
   					socket.close();
   				} catch (IOException e) {
   					// TODO Auto-generated catch block
   					e.printStackTrace();
   				}
   			}
   			if(serverSocket!=null) {
   				try {
   					serverSocket.close();
   				} catch (IOException e) {
   					// TODO Auto-generated catch block
   					e.printStackTrace();
   				}
   			}
   				
   		}
   
   	}
   }
   
   ```

2. 客户端

   ```java
   import java.net.*;
   import java.io.*;
   	
   public class TcpClientDemo {
   	public static void main(String[] args) {
   		
   		Socket socket=null;
   		OutputStream os=null;
   		
   		try {
   			// 知道服务器地址、端口
   			InetAddress serverIP=InetAddress.getByName("localhost");
   			int port =9999;
   			// 创建应该socket连接
   			socket =new Socket(serverIP,port);
   			// 发送消息 IO流
   			os=socket.getOutputStream();
   			os.write("你好，这是一个Java网络通信测试".getBytes());
   		} catch(Exception e) {
   			e.printStackTrace();
   		} finally {
   			if(os!=null) {
   				try {
   					os.close();
   				} catch (IOException e) {
   					// TODO Auto-generated catch block
   					e.printStackTrace();
   				}
   			}
   			if(socket!=null) {
   				try {
   					socket.close();
   				} catch (IOException e) {
   					// TODO Auto-generated catch block
   					e.printStackTrace();
   				}
   			}
   		}
   	}
   }
   
   ```

> 启动服务器、客户端
>
> ![image-20230417112707494](https://cdn.jsdelivr.net/gh/yangxiaozhao/TyporaImg@master/img202304171127544.png)
>
> ==成功输出==



# IO流


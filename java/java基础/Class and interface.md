## 类

### 类继承(只能单继承)

- 子类继承超类的非私有的所有成员(除构造函数外) //包括公有嵌套类
- 子类只能通过父类的相关方法调用父类的私有成员


```java

public class Bicycle {
...
}

public class MountainBike extends Bicycle {
       //子类MountainBike，超类Bicycle
       ...
}


public class Bicycle {
      void byTest() {
           this.test();   
           //this是对当前对象的引用
           super.test();  // 子类只能通过关键字super来访问父类的成员
      ...
}
```

### 子类构造函数

- 用户定义地无参构造函数会覆盖编译器提供的默认构造函数
- 用户定义地有参构造函数会让编译器就不提供默认构造函数

```java

public MountainBike(int startHeight, 
                    int startCadence,
                    int startSpeed,
                    int startGear) {
                    
       //超类构造函数的调用必须在子类构造函数的第一行
       super(startCadence, startSpeed, startGear);//调用父类的有参构造函数   
       seatHeight = startHeight;
} 

public MountainBike(int startHeight){

       super(); //调用父类的无参构造函数 
       seatHeight = startHeight;
} 
```
### 抽象类

1. 用于继承(不能实例话)

- 抽象方法：在一个类中没有实现却声明的方法
```java
abstract void moveTo(double deltaX, double deltaY);
```
- 抽象类:用abstract修饰的类
```java
public abstract class GraphicObject {
   // declare fields
   // declare nonabstract methods
   abstract void draw();
}
```
- 如果类包含抽象方法，则必须用关键字`abstract`声明该类
- 抽象类的子类必须要实现父类中所有的抽象方法，不然就必须声明为abstract







## 接口：可以认为是一种特殊的类

### 接口的定义

- 接口的意义：是对不具有继承关系的同类行为的抽象，以便复用(多态的一种)
- 接口中所有的方法都是默认 public abstract，因此接口中的方法都是抽象的
- 接口中所有变量都是默认 public static final，因此接口中变量就相当于常量
- 所以接口只包含常量，抽象方法、默认方法和静态方法

```java
public interface OperateCar {

       int changeLanes(Direction direction,
                       double startSpeed,
                       double endSpeed);
       int signalTurn(Direction direction,
                      boolean signalOn);
       double E = 2.718282;   
         ......
}

```



### 接口的实现

- 使用接口的类必须实现其接口的所有方法，除非它是抽象类

```java
public class FlyingCar implements OperateCar, FlyCar {
       // ...
       public int startEngine(EncryptedKey key) {
              FlyCar.super.startEngine(key);//调用接口FlyCar的这个方法
              OperateCar.super.startEngine(key);
       }
}
```


### 接口的继承(可以单继承和多继承)

```java
public interface GroupedInterface extends Interface1, Interface2, Interface3 {//多继承

       double E = 2.718282;
       void doSomething (int i, double x);
       int doSomethingElse(String s);
}
```
- 当你要继承的接口含有默认方法时：
1. 不修改
2. 将默认方法声明为抽象方法。
3. 重写默认方法。

### 向接口添加方法
```java
public interface DoIt {//原接口
   void doSomething(int i, double x);
   int doSomethingElse(String s);
}
```
1.创建一个原接口的子接口，在子接口中添加方法
```java
public interface DoItPlus extends DoIt {

   boolean didItWork(int i, double x, String s);
}
```
2.在原接口中将新方法定义为默认方法
```java
public interface DoIt {

   void doSomething(int i, double x);
   int doSomethingElse(String s);
   default boolean didItWork(int i, double x, String s) {//默认方法：由default修饰的方法
     ...
   }
}
```
3. 在原接口中将新方法定义为静态方法
```java
public interface DoIt {

   void doSomething(int i, double x);
   int doSomethingElse(String s);
   static  boolean didItWork(int i, double x, String s) {//静态方法：由static修饰的方法
     ...
   }
}
```

- 不要向接口添加抽象方法(如果有实现该接口的类)，否则所有实现旧的原接口的类都将中断
- 第二，三种使您能够向原接口添加新功能，并确保与为未修改的原接口的编写的类能正常使用(而且这些类可以使用新功能)



## 类与接口共性

### 子类重写父类的方法

- 返回值和形参都不能改变
> 实现接口的类是该接口的子类，该接口是这个类的父类 
> 接口的子类实现接口的方法也叫重写

```java

public class MountainBike extends Bicycle {
       @Overide  //可以作为程序员地一种保护措施
       //重写的方法都用@Overide标记
       public int Test(){
             //新的实现
       }
       ...
}
```
- 子类方法的访问权限一定要大于等于父类方法的访问权限
- 子类方法声明的任何异常必须是父类方法所声明异常的同类或子类
- 只能重写继承了的方法，且父类中fianl,static修饰的方法不能重写


### instanceof 运算符

```
    boolean bool=ren instanceof Person;
    //判断引用变量ren引用的对象的类型是不是Person类型
    //是的话为true
    //Person可以是类可以是接口
```


### 对象的类型转换

> 接口可以作为类型来声明变量(不能用new实例化接口)，但该变量引用的对象必须是实现该接口的类的实例
> 该变量能过使用接口的方法

```java
List61B<String> lst= new SLList<String>();
//List61B是个接口，SLList实现了该接口
```

- 静态类型：声明变量时的类型;
- 动态类型：引用变量引用的对象的类型；

#### 向上转型：父类类型的变量引用子类类型的对象
```java
父类 object1=new 子类();
//object1只能访问子类继承父类的方法和属性
//当调用方法时，只有子类重写了父类的方法才调用子类的
```

#### 向下转型：父类类型的变量obj1引用子类类型的对象,再把obj1赋给子类类型的变量obj2         
```java
if(obj1 instanceof 子类){    
        子类 object2 = (子类)object1;  
        // obj1必须是指向子类对象的父类引用
        // 因为在编译器判定中object1是父类型，因此需要强制转换来通过编译
}
```


### 多态
1. 静态多态：方法重载
2. 动态多态
- 程序中定义的引用变量所指向的具体类型和通过该引用变量调用的方法在程序运行期间才确定
- 条件：继承、子类重写父类的一些方法、向上转型
- 继承同一个父类的子类对某些方法的重写了，多个子类对象调用重写的方法表现出不同的行为
> java运行一个被重写的方法时，它会再其（调用该方法的变量）动态类型中搜索适当的方法签名并运行它







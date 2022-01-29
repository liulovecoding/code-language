

## 终极父类——object类：位于包java.lang中

1. 用于转型等

- 如果一个类声明时没有指定父类，那么它的父类就是object类
- object类的主要方法
```java
public String toString();  

public boolean equals(Object obj); 

public final Class getClass();  //返回对象的类型类
> 官方建议：不要重写该方法

protected Object clone() throws CloneNotSupportedException;   
//创建并返回此对象的副本给调用者。

public int hashCode();  //返回对象的哈希码
```


#### toString()方法

- Object类的toString()方法打印对象在内存中的位置。这是一个十六进制字符串
- System.out.println(dog) ==  String s = dog.toString() + System.out.println(s)  //dog是个对象

> 官方建议：始终考虑在你的类中重写该方法

1. 重写

- 一次糟糕的重写
```
public String toString() {
    String returnString = "{";
    for (int i = 0; i < size; i += 1) {
        returnString += keys[i]; //这条语句不仅将key[i]加到returnString上，并创建一个新的字符串
        returnString += ", ";
    }
    returnString += "}";
    return returnString;
}
```
- 改进
> 使用StringBuilder. 它创建了一个可变的字符串对象，因此您可以继续附加到同一个字符串对象，而不是每次都创建一个新对象。
```
StringBuilder returnSB = new StringBuilder("{");
        for (int i = 0; i < size - 1; i += 1) {
            returnSB.append(items[i].toString());
            returnSB.append(", ");
        }
        returnSB.append(items[size - 1]);
        returnSB.append("}");
        return returnSB.toString();
```

####  equal()方法
- 比较两个引用变量是否指向同一个对象 ，否则在类中重写equals()方法
- ==检查两个对象是否实际上是内存中的同一个对象

1. 重写equals()遵守的规则
- 反身：x.equals(x)是真的
- 对称：x.equals(y)为真当且仅当y.equals(x)为真
- 传递：如果x.equals(y)和y.equals(z)为真，则x.equals(z)为真
-  x.equals(null)必须是假的


> 会更改两个对象的等价方式，并且Object的实现hashCode()不再有效。因此也必须重写hashCode()


#### clone()方法(浅拷贝)

对象的类或其超类必须实现了java.lang.Cloneable接口
```java
//实现类
public class Animal implements Cloneable {

    ...
    public Object clone() throws CloneNotSupportedException {
       ...
        //也可以为私有
    }
    ...
}
```
> 浅拷贝：当复制引用类型的对象时仅复制其引用，而不是复制对象

> 深拷贝：当复制引用类型的对象时复制其对象


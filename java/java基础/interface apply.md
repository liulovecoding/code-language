### HOF

- 利用接口实现(也算接口继承 //参考cs61b 4.2)

> 好处1： 每个类都不需要最大化代码
> 好处2：我们有可以优雅地（大部分）在多种类型上运行的代码

1. 编写一个接口
```java
public interface IntUnaryFunction {
    int apply(int x);
}
```

2. 编写类实现该接口
```java
public class TenX implements IntUnaryFunction {
    /* Returns ten times the argument. */
    public int apply(int x) {
        return 10 * x;
    }
}
```

3. 利用接口做类型编写高阶函数
> 在这里参数f的类型用IntUnaryFunction比用Object更优，因为用Object需要强转为TenX类型，才能使用Tenx实现接口的方法
```java
public static int do_twice(IntUnaryFunction f, int x) {
    return f.apply(f.apply(x));
}
```

4. 调用
```java
System.out.println(do_twice(new TenX(), 2));
```

### 编写更通用的方法
- 接口+泛型 ==更通用的接口

> 这是java内置的
```java
public interfance Compare<T>{
    public int compareTo(T obj);
```

### 实现支持foreach //本质是获得可迭代的对象（以某种方式迭代）

- foreach的本质
```java
for (T o :s){
    ...
}
==
while(s.hasNext(){
     o=s.next;
}
```

0. 接口java.lang.Iterable 介绍

```java
////用来支持foreach
public interface Iterable<T> {
    Iterator<T> iterator(); //该方法返回一个迭代对象

}
```

1. 实现接口java.lang.Iterable 

```java
import java.util.Iterator;

public class LinkedListDeque<T> implements  Iterable<T> {
    private  class  IntNode{
        public   T item;
        public   IntNode next;//指向下一个
        public   IntNode front;//指向上一个

        public  IntNode(T i,IntNode first,IntNode next){
            item=i;
            this.next=next;
            this.front=first;
        }
    }

    private  int size; //deque的item的个数

    public LinkedListDeque(){
        //构造前和尾哨兵
        firstNode=new IntNode(null,null,null);
        endNode=new IntNode(null,null,null);
        recursion=new IntNode(null,null,null);
        //初始化
        firstNode.next=endNode;
        endNode.front=firstNode;
        recursion=firstNode;
        size=0;
    }

    //写这个方法
    public Iterator<T> iterator() {
        return  new LLIterable(); //返回第二步写的类的对象
    }

    ...
}

0. java.util.Iterator介绍

```java
// 用于迭代
public interface Iterator<E>{
        boolean hasNext();
        E next();
}
```

2. 编写个子类实现接口java.util.Iterator
```java
public class LinkedListDeque<T> implements  Iterable<T> {
     ...
     private class LLIterable  implements  Iterator {
        private  IntNode node;
        private  int index;

        LLIterable(){
            node=firstNode;
            index=0;
        }

        public boolean hasNext(){
            return index<size;
        }

        public T next(){
            node=node.next;
            index+=1;
            return  node.item;
        }

   }
    
}
```

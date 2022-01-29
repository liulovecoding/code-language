
- 异常继承树
```ascii
                     ┌───────────┐
                     │  Object   │
                     └───────────┘
                           ▲
                           │
                     ┌───────────┐
                     │ Throwable │
                     └───────────┘
                           ▲
                 ┌─────────┴─────────┐
                 │                   │
           ┌───────────┐       ┌───────────┐
           │   Error   │       │ Exception │
           └───────────┘       └───────────┘
               ▲                     ▲
         ┌─────┘              ┌──-──-┴──────────┐
         │                    │                 │
┌─────────────────┐    ┌─────────────────┐┌───────────┐
│OutOfMemoryError │... │RuntimeException ││IOException│...
└─────────────────┘    └─────────────────┘└───────────┘
```


![异常](https://user-images.githubusercontent.com/90401274/144363305-64dcbcf3-18e2-4475-ad88-b89498c68c10.png)



### 异常处理

- 方法声明可能会抛出必检异常(说明当使用该方法需要异常处理)
```java
public void methodname throws Exception1,Exception2,..,ExceptionN  {  }  
//该方法可能抛出必检异常Exception1,Exception2,…,ExceptionN 
public void methodname throws Exception  {  }  
//该方法可能抛出所有的异常
```

- 异常抛出
1. 当方法内出现必检异常且该方法不想或不能处理时用throw语句抛出
2. 免检异常由JVM抛出，可以不用throw语句抛出
3. 且程序会在throw语句或JVM抛出异常后立即终止

```java
 public class TestException throws Type{  
    public static void main(String[] args) {  
    int a =30;
    if(a<0){
          throw new  Type; //抛出类型为Type的对象
    }	  
``` 
 
- 异常捕获处理(不需要异常声明)
```python
public static void main(String[] args) {  
       try { //用于捕获异常 
	       // 可能会发生异常的程序代码  
       } catch (Type1 id1){  
	      // 捕获并处置try抛出的异常类型Type1  
       } catch (Type2 id2){  //用于处理try捕获到的异常
       }finally {  //通常执行对资源的关闭
	           // 无论有无异常情况，都将执行的语句块  
      } 
}
```
 - 如果抛出的异常对象没有try-catch 语句处理的话，则由JVM处理
 - 如果抛出的异常对象是catch子句的异常类或者其子类的实例，则执行该catch块中的代码
 - 将捕获底层异常类的catch子句放在前面，同时将捕获相对高层的异常类的catch子句放在后面,否则，捕获底层异常类的catch子句将可能会被屏蔽
 - try 块后面接零个或多个catch块，如果没有catch块，则必须跟一个finally块

 ### File类

- file对象是把(**索引磁盘中的文件和目录的**)路径转换成抽象路径来创建的
- 用于程序中对文件对象表示的路径进行操作，如：创建一个新文件 etc

### 构造方法

- File对象不一定说明他代表的文件或目录存在，除非它真的存在或者再程序中创建了

- File file =new File(String pathName) 

  ```java
  path="C:\\Users\\50657\\Desktop\\test.txt"    
  File file = new File(path);
  if (file.exists()) #判断file代表的文件(目录)存不存在
      System.out.print("aleary exits");
  ```

  

- File file =new File(File parentfile,String child) 

  ```java
  //parentfile：抽象父路径，child:parentpath所代表的目录的子目录的路径 
  File parentfile = new File("C:\\Users\\50657\\Desktop\\text");
  File file = new File(parentfile, "test.txt");
  if (file.exists() && file1.exists())
      System.out.print("aleary exits");
  ```

  

- File file =new File(String parentpath,String child) 

  ```java
  //parentpath：父路径，child:parentpath的子路径 
  parentpath= "C:\\Users\\50657\\Desktop\\text";
  File file = new File(parentpath, "test.txt");
  ```

  

- File file=new File(URI uri) 

  #URI: 是一个用于标识某一互联网资源名称的字符串

、

### 方法

-  public boolean delete()    //删除file对象代表的目录或文件

  ```java
  file.delete();
  //若file是个目录的话，只有该目录为空才能删除
  ```

  

-  public boolean exits()  //判断file对象代表的目录或文件存不存在

-  public boolean isDirectory()   //判断file对象代表的文件(目录)是不是一个目录

-  public boolean isFile()   // 判断file对象代表的文件(目录)是不是一个标准文件

  ```java
  file.exits(); 
  file.isDirectory();
  file.isFile();
  ```

  

-  public boolean mkdirs()   //根据文件对象所代表的路径下创建目录(包括不存在的父目录)

- public boolean mkdir() //创建目录

  ```java
  File file=new File("C:\\Users\\50657\\Desktop\\text\\test") 
  file.mkdirs();
  //该路径上的目录可以不存在，不存在的都会创建
  
  File file=new File("C:\\Users\\50657\\Desktop\\text\\test") 
  file.mkdirs();
  //创建test目录(前提:该路径除了test目录可以不存在，其余目录都要存在)
  ```

  

-  public boolean createNewFile() throws IOException //创建文件

  ```java
  File file=new File("C:\\Users\\50657\\Desktop\\text\\test") 
  file.createNewFile();
  //当file代表的文件不存在时，创建
  ```

  

-  public boolean equals(Object obj)  //判断两个File对象是不是代表同一个文件或目录

  ```
  File file=new File("C:\\Users\\50657\\Desktop\\text\\test");
  File file1=new File("C:\\Users\\50657\\Desktop\\text\\test");
  file.equals(file1);
  //结果：true
  ```

  

-  public String toString()  //返回file表示的文件或目录的路径符串

-  public String getPath() //两者等价 

  ```java
  File file=new File("C:\\Users\\50657\\Desktop\\text\\test");
  String path=file.toString();
  System.out.println(path);
  //C:\Users\50657\Desktop\text\test
  ```

  

- public boolean renameTo(File dest)    //对实际文件重命名

  ```java
  File oldName = new File("E:\\hello\\test\\1.txt");
  File newName = new File("E:\\hello\\test\\2.txt");
  System.out.println(oldName.renameTo(newName));//true
  //1.txt文件被重命名为2.txtm
  //但是 odlName.toString()的值不变
  ```

  

- public long  lastModified()  //返回文件(目录)最后一次被修改的时间

- public long  lenght()   //文件内容的长度

  ```java
  file.lastModified();
  //返回fileb表示的文件(目录)最后一次被修改的时间
  file.lenght();
  //返回fileb表示的文件内容的长度
  ```

  

- public File[] listFiles()    //file所表示的目录中的文件和目录的File数组对象

- pubilc String[] list()      //file所表示的目录中的文件和目录的路径组成的字符串数组

  ```java
  File file=new File("C:\\Users\\50657\\Desktop\\text");
  //test目录下有目录test1，test2，test3.txt
  String[] list =file.list();
  //file所表示的目录中的文件和目录的名称组成的字符串数组
  for (String str : list) {
              System.out.println(str);
          }
  //结果：test1 test2 test3.txt (实际上会换行)
  File[] listfile=file.listfile(); 
  //
  File[] listfiles = newName.listFiles();
          for (File file1 : listfiles) {
              System.out.println(file1);
          }
  /*结果：
  C:\Users\50657\Desktop\text\test1
  C:\Users\50657\Desktop\text\test2
  C:\Users\50657\Desktop\text\test3.txt
  */
  ```

  

- public File[]  listFiles(new FilenameFilter）//文件过滤器

- public String[] list(new FilenameFilter)  //FilenameFilter写法一样

  ```java
  File[] listFiles2 = file.listFiles(new FilenameFilter() {
              public boolean accept(File dir, String name) {
                  return name.endsWith(".java") && new File(dir, name).isFile();
              }
          });
  ```
  
  
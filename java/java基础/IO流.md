## IO流

因为数据传输像水流一样



## 字节流

- 节(byte)为单位读取或写入数据，用于处理媒体数据
### 输入字节流InputStream
- InputStrem是抽象类，是所有输入字节流的父类

- fileIuputStream流：从文件中读取数据

- BtyeArrayIuputStream流：从Btye数组读取数据

- StringBufferIuputStram流：从StringBuffer中读取数据

- 上面提到的是三个基本流

  

### 输出字节流OutputStream
- OutputStram是抽象类，是所有输出字节流的父类

- FileOutputStream流：向文件中写入数据(

- BtyeArrayOutputStream流：向Btye数组写入数据

- StringBufferOutputStram流：向StringBuffer中写入数据

- 上面提到的是三个基本流

  

## 2.字符流
- 以字符为单位读取或写入数据(字符的长度与编码方式有关)，用于处理文本数据
- 本质是对字节流做了处理

### 输入字符流Reader
- Reader是抽象类，是所有输入字符流的父类
- StringReader流：从字符串缓冲区中读取字符
- FileReader流：从文件中读取字符

- InputStreamReader流：将字节输入流转化为字符输入流(上面提到的是三个常见流)

### 输出字符流Writer
- Writer是抽象类，是所有输出字符流的父类
- StringWriter流：向字符串缓冲区中写入字符
- FileWriter流：向文件中写入字符

- InputStreamWriter流：将字节输出流转化为字符输入流(上面提到的是三个常见流)


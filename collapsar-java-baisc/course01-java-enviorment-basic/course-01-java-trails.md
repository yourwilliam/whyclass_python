# \[course01\] 01 Java入门

## \[course01\] 01 Java入门

### JDK

[jdk 11 documentation](https://docs.oracle.com/en/java/javase/11/)

[Java 8 Conceptual Diagram](https://docs.oracle.com/javase/8/docs/)

![](https://ossp.pengjunjie.com/mweb/16279812356650.jpg)

JRE：Java Runtime Environment

JRE stands for “Java Runtime Environment” and may also be written as “Java RTE.” The Java Runtime Environment provides the minimum requirements for executing a Java application; it consists of the Java Virtual Machine \(JVM\), core classes, and supporting files.

JDK：Java Development Kit

The Java Development Kit \(JDK\) is a software development environment used for developing Java applications and applets. It includes the Java Runtime Environment \(JRE\), an interpreter/loader \(Java\), a compiler \(javac\), an archiver \(jar\), a documentation generator \(Javadoc\) and other tools needed in Java development.

JRE是java运行时环境，包含了java虚拟机，java基础类库。是使用java语言编写的程序运行所需要的软件环境，是提供给想运行java程序的用户使用的。

JDK顾名思义是java开发工具包，是程序员使用java语言编写java程序所需的开发工具包，是提供给程序员使用的。JDK包含了JRE，同时还包含了编译java源码的编译器javac，还包含了很多java程序调试和分析的工具：jconsole，jvisualvm等工具软件，还包含了java程序编写所需的文档和demo例子程序。

如果你需要运行java程序，只需安装JRE就可以了。如果你需要编写java程序，需要安装JDK。

#### Difference between JDK, JRE and JVM

![](https://ossp.pengjunjie.com/mweb/16279819859166.jpg)

**JDK – Java Development Kit** \(in short JDK\) is Kit which provides the environment to develop and execute\(run\) the Java program. JDK is a kit\(or package\) which includes two things

* Development Tools\(to provide an environment to develop your java programs\)
* JRE \(to execute your java program\).

Note : JDK is only used by Java Developers.

**JRE – Java Runtime Environment** \(to say JRE\) is an installation package which provides environment to only run\(not develop\) the java program\(or application\)onto your machine. JRE is only used by them who only wants to run the Java Programs i.e. end users of your system.

**JVM – Java Virtual machine**\(JVM\) is a very important part of both JDK and JRE because it is contained or inbuilt in both. Whatever Java program you run using JRE or JDK goes into JVM and JVM is responsible for executing the java program line by line hence it is also known as interpreter.

#### 安装jdk

本地可以安装oracle jdk 11的版本。

下载地址[https://www.oracle.com/java/technologies/javase-jdk11-downloads.html](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html)

直接使用安装包安装。安装完成之后，打开terminal，windows打开powershell。 运行命令行`java -version`。 此时可以发现无法打开，主要原因是安装之后没有把Java放入环境变量，系统全局路径是找不到相应的配置环境的。

#### 命令行

另一个文档已经整理过了相应的环境变量

**mac配置环境变量。**

在mac下面配置java的环境变量会比较麻烦，最好使用命令行操作。在命令行中运行

```bash
$ vi /etc/.bash_profile

加入两行

export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk-11.0.9.jdk/Contents/Home/
export PATH=${JAVA_HOME}/bin:$PATH
```

加入后会在terminal启动后自动加载环境变量。可以使用命令查看是否配置成功

```bash
$ export $PATH

在返回值中看到jdk的内容代表配置成功了。
```

配置成功之后再执行java即可

### 运行Java

* 在你的用户目录创建一个workspace目录，然后依次创建文件夹 java --&gt; clitest 目录
* 新建文本文件HelloWorld.java
* 在文本文件中添加基本代码

  ```text
  public class Helloworld{
    public static void main(String[] args) {
        System.out.println("hello world");
    }
  }
  ```

* 在terminal\(mac\), powershell\(windows\)中cd到对应目录
* 执行javac HelloWorld.java。 看看目录中会生成什么文件。这时候会多出来一个HelloWorld.class文件，就是字节码文件。
* 执行java HelloWorld 查看命令结果

### Java IDE

下载地址[https://www.jetbrains.com/idea/download](https://www.jetbrains.com/idea/download)

下载之后直接安装即可。

#### 创建工程

![-w1091](https://ossp.pengjunjie.com/mweb/16280062029243.jpg)


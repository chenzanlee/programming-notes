# 命令行工具篇 #

## javac——java编程语言编译器 ##
官方链接：https://docs.oracle.com/javase/8/docs/technotes/tools/windows/javac.html
##语法##
 javac [ options ] [ sourcefiles ] [ classes ] [ @argfiles ]

参数可以按任意顺序。
###options###
命令行选项。见Options一节。
###sourcefiles###
一个或多个待编译的源文件（例如MyClass.java)

###classes###
一个或多个待处理注解的类（例如MyPackage.MyClass)。

###@argfiles###
一个或多个列出了选项和源文件的文件。-J选项不允许在这些文件中使用。见命令行参数文件一节。

##说明##
javac命令读取用java编程语言写的类和接口的定义，将它们编译为字节码class文件。javac命令还可以处理java源文件或类中的注解。
有两种方式将源代码文件名称传递给javac.
- 对少量的源文件，直接在命令行汇总列出文件名
- 对大量的源文件，在一个文件中列出它们的名称，用空格或者换行符隔开。在javac中，通过在文件名前加一个@符号来使用这个文件。

##选项##
###标准选项###
-cp *path* or -classpath *path*
指定查找用户类文件、（可选的）注解处理器、源文件的位置。这个类路径覆盖了CLASSPATH环境变量中的用户类路径。如果CLASSPATH、-cp或-classpath都未指定，那么用户类路径为当前目录。见设置类路径
如果-sourcepath选项没有指定，那么用户类路径也用来查找源文件。
如果-processorpath选项没有指定，那么该类路径也用来查找注解处理器。

-Djava.ext.dirs=directories
覆盖已安装的扩展类的位置。

-d directory
设置生成的class文件的目标目录。因为javac命令不会创建它，该目录必须已经存在。如果一个类是一个包的一部分，那么javac将该class文件放到目标目录的一个子目录下，该子目录反映出包名，javac命令会根据需要创建相应的子目录。
如果你指定-d C:\myclasses,待编译的类为com.mypackage.MyClass,那么该class文件为C:\myclasses\com\mypackage\MyClass.class.
如果不指定-d选项的话，javac会将每个class文件放到生成它们的源文件所在的目录下。
注意：通过-d选项指定的目录不会自动添加到你的用户类路径。
## javap ##

## java ##
启动一个java应用程序。
官方链接：
注意事项：**注意下面option参数的位置，永远在第一位，以classname或-jar filename为界限，classname后面的字符串统统解析为args传递给主类的main()方法。**
java [options] classname [args]
java [options] -jar filename [args]
options
命令行选项参数，通过空格分开. See Options.

classname
待启动的类名，全限定类名  注意：这里不是class文件**

filename
将被调用的jar档案文件名，仅用于和-jar选项一起使用。

args
传递给main()方法的参数，通过空格分开


-cp/classpath
指定目录，jar档案文件，zip档案文件列表，用于查找类文件。以;分割，注意：**如果列表以；结束,则会被解释为包含当前路径，及等同于以；.结尾**。为方便起见，如果一个路径以'\*'结尾，则会被java启动器工具解释为该目录下的所有jar，比如目录mydir中包含a.jar,b.jar，则路径mydir/\*将被扩展为mydir/a.jar;mydir/b.jar.该扩展发生在jvm启动前。除了通过System.getEnv("CLASSPATH"),java程序是无法看到扩展前的*通配符的。


# jar #
jar cvf xx.jar  file1 file2
创建名为xx.jar的jar档案文件，包含file1,file2

jar uvf xx.jar file3  更新xx.jar,添加file3文件，如果xx.jar中已存在file3，则替换

jar tf xx.jar  列出xx.jar中的所有文件，包括文件夹的结构
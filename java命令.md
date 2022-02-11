### 只使用java工具编译项目

> 声明:该方法适用于在只有java环境的条件下使用，如有IDE或者MAVEN请不要使用。

示例目录结构

- example

  - lib(依赖jar文件)
  - classes(编译文件输出文件夹，需要提前创建)
  - src(源代码文件夹)

  

步骤一：在终端或者命令行中进入到example文件夹下。
步骤二：使用命令`find src -name \*.java > javaFilestxt.txt`查找需要编译的java文件并将结果写入 javaFiles.txt文件中。
步骤三：创建编译文件输出文件夹，使用javac命令进行编译，无报错表示编译成功。命令内容:`javacd classes -cp .:./1ib/* @./javaFiles.txt`，命令参数详解:d为指定输出路径，需要提前创建;-cp指定 classpath为当前目录和lib目录下所有的库文件;@后面指定需要编译的文件列表。
步骤四：(非必须)使用jar对编译文件进行打包。命令内容:`jar -cp a.jar folder1 folder2 filel file2`。
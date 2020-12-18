# JavaIO流

> 什么是java的IO流?
>
> i : input  输入
>
> o :output 输出
>
> 流式什么?
>
> 在计算机中我经常做的一件事情 ，复制粘贴，鼠标右键就可以操作完成。
>
> 在实际的开发中我们要将文件或者图片上传到服务器。
>
> 怎么把本地的东西上传到服务器，或者把服务器的东西下载到本地? 文件的复制
>
> 任何的文件，byte 字节表示大小。
>
> 底层都是字节的数据。unicode 编码或者其他的编码的东西。

## 1. File 文件

> 文件和目录路径名的抽象表示形式。 
>
> 用户界面和操作系统使用与系统相关的*路径名字符串*  来命名文件和目录。此类呈现分层路径名的一个抽象的、与系统无关的视图。*抽象路径名* 有两个组件： 
>
> 1. 一个可选的与系统有关的*前缀* 字符串，比如盘符，`"/"` 表示 UNIX  中的根目录，`"\\\\"` 表示 Microsoft Windows UNC 路径名。 
> 2. 零个或更多字符串*名称* 的序列。 
>
> 抽象路径名中的第一个名称是目录名，对于 Microsoft Windows UNC  路径名则是主机名。抽象路径名中第一个名称之后的每个名称表示一个目录；最后一个名称既可以表示目录，也可以表示文件。*空*  抽象路径名没有前缀和名称序列。 
>
> 路径名字符串与抽象路径名之间的转换与系统有关。将抽象路径名转换为路径名字符串时，每个名称与下一个名称之间用一个默认*分隔符*  隔开。默认名称分隔符由系统属性 `file.separator` 定义，可通过此类的公共静态字段 `separator` 和  `separatorChar`  使其可用。将路径名字符串转换为抽象路径名时，可以使用默认名称分隔符或者底层系统支持的任何其他名称分隔符来分隔其中的名称。

```java
package com.xdkj.javase.io;

import java.io.File;
import java.io.IOException;

/**File 文件或者目录的抽象表示形式:
 * 	File(String string )  文件或者文件夹的字符串路径表示
 * 	File(File,String)
 * 	File(String,String)
 * 
 * 判断:
 * 		exists() 判断文件或者文件夹是否存在
 * 		isFile() 判断是否是文件
 * 		isDirectory()判断是否是文件夹
 * 		equals() 判断路径是否相等
 * 		isAbsolute() 判断是否是绝对路径
 * 		idHidden() 是否是隐藏的文件
 * 		canRead() 是否是只读文件
 * 		canWrite() 是否是只写文件
 * 创建:
 * 		创建文件夹:
 * 			a. 创建单层文件夹  mkdir()
 * 			b. 创建多层文件夹 mkdirs()
 * 		创建文件:
 * 			createNewFile();
 * 删除: 
 * 		delete() 删除文件或者目录
 * 获取: 
 * 		getAbsoluteFile() 获取绝对的路径形式
 * 		getAbsolutePath() 获取绝对的字符串路径
 * 		getName() 获取文件文件夹名称
 * 		getParent()  获取父路径的字符串
 * 		getParentFile() 父文件的抽象名
 * 		length() 获取文件长度
 * 		list() 字符串数组
 * 		listFiles() 获取文件名数组
 * 	设置: 
 * 		setLastModiFiled()  最后一次修改的时间
 * 		setReadOnly() 设置只读
 * 		setWriteable() 设置只写 
 * 			
 * */
public class FileDemo {
	public static void main(String[] args) throws IOException {
		//fileMethod1();
		//fileMethod2();
		//fileMethod3();
		//fileMethod4("E:\\java\\javase\\io\\hello.txt" );
		 fileMethod5(new File("E:\\视频录制\\西点科技\\JAVA-51"));
	}
    
    //删除的是文件夹  文件夹必须是空的
	public  static void fileMethod6(File  file) {
		System.out.println(file.delete());
	}

	//遍历给定目录下的所有的问件
	//递归 自己调用自己
	//递归要有出口  
	public static void fileMethod5(File f ) {
		if(f.isDirectory()) {
			//获取文件夹中的问价和文件夹 的抽象路径数组
			File[] files = 	f.listFiles();
			for(int i = 0;i<files.length;i++) {
				//又得判断是问价夹还是问件
				fileMethod5( files[i] );
			}
		}else {
			//文件的名称
			System.out.println(f.getName());
		}
	}
	//获取和判断文件路径
	public static void fileMethod4(String  file1 ) {
		File file = new File(file1);
		//判断路径是否是文件路径
		System.out.println(file.isFile());
		//判断路径是否是文件夹路径  
		System.out.println(file.isDirectory());
		//是否是绝对路径
		System.out.println(file.isAbsolute());
		//文件的最后一次修改的时间
		System.out.println(file.lastModified());
		//文件大大小 (内容的大小)
		System.out.println(file.length());
		//绝对路径的字符串表示形式
		System.out.println(file.getAbsolutePath());
		//获取父路径的字符串
		System.out.println(file.getParent());
		//获取文件或者问价夹的名称
		System.out.println(file.getName());
		//父目录或者问件的抽象路径  File
		System.out.println(file.getParentFile());
		
	}
	//判断文件夹 、文件的属性
	public static void fileMethod3() {
		File file = new File("E:/1.txt");
		//文件是否是只读  只写  隐藏的
		System.out.println(file.canRead());//true
		System.out.println(file.canWrite());//true
		System.out.println(file.isHidden());//true
		//root 
		file.setReadable(true);//修改为 可读状态
		file.setWritable(true);//可写状态
		//io流写东西
	}
	
	
	//创建文件和文件夹
	private static void fileMethod2() throws IOException {
		File file2 = new File("E:/java/javase/io");
		File file3 = new File(file2,"hello.txt");
		//判断是否存在
		//创建文件夹  
		if(!file2.exists()) {
			file2.mkdirs();
		}
		//创建文件
		if(!file3.exists()) {
			file3.createNewFile();
		}
	}

	private static void fileMethod1() {
		//字符串是文件或者文件夹的路径名称
		//File  file = new File("E:\\1.txt");
		//File file = new File("E:\\","1.txt");
		File file = new File("E:\\");
		//父路径 + 子路径
		File file1 = new File(file,"1.txt");
			System.out.println(file);
			System.out.println(file1);
			//文件目录
			//单层文件目录
		//File file2 = new File("E:\\java");
	}
}

```


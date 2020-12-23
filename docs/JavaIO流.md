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
> 底层都是字节的数据。unicode 编码或者其他的编码的东西。\
>
> IO流按照数据的流向:
>
> InputStream/OutputStream (字节流)
>
> Reader/Writer(字符流)
>
> Io流基本上我们学习的都是上边四个抽象类的子类

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

## 2. InputStream

> 字节输入流:  此抽象类是表示字节输入流的所有类的超类。
>
> 因为是抽象类，抽象类不能实例化。

### 2.1 FileInputStream

+ read()
+ read(Byte[])
+ read(Byte[],offset,length)
+ close() 关闭流的资源

```java
package com.xdkj.javase.io;

import java.io.File;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;

public class FileInputStreamDemo {

	public static void main(String[] args) {
		//抽象路径
		File file = new File("E:/1.txt");
		//inputStreamMetod1(file);
		
		//inputStreamMetod2(file);
		inputStreamMetod3(file);
		
	}
	//一个字节一个字节的读取
	private static void inputStreamMetod1(File file) {
		InputStream  inputStream  = null;
		//从哪个路径的文件中读文件的内容
		try {
			inputStream = new FileInputStream(file);
			//读内容  
			//第一个字符的utf-8的编码
			System.out.println(inputStream.read());//49
			System.out.println(inputStream.read());//50
			System.out.println(inputStream.read());//51
			System.out.println('1'+0);
		} catch (FileNotFoundException e) {
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		}
	}
		//一个字节一个字节的读取
		private static void inputStreamMetod2(File file) {
			InputStream  inputStream  = null;
			OutputStream outStream = null;
			//从哪个路径的文件中读文件的内容
			try {
				inputStream = new FileInputStream(file);
				outStream = new FileOutputStream("E:\\2.txt");
				//读内容  
				//第一个字符的utf-8的编码
				int len = 0;	
				while((len = inputStream.read())!=-1) {
						System.out.println(len);
						outStream.write(len);
				}
				//  11100100 10111000 10000000
				//	0110 0010 0001 0001
				System.out.println('一'+0);
			} catch (FileNotFoundException e) {
				e.printStackTrace();
			} catch (IOException e) {
				e.printStackTrace();
			}finally {
				//资源关闭
				//先用后关
				try {
					outStream.close();
				} catch (IOException e) {
					e.printStackTrace();
				}
				try {
					inputStream.close();
				} catch (IOException e) {
					e.printStackTrace();
				}
			}
		}
		
		//使用数组来装读取到的字节内容  造成文件整体的长度错误!
				private static void inputStreamMetod3(File file) {
					InputStream  inputStream  = null;
					OutputStream outStream = null;
					//从哪个路径的文件中读文件的内容
					try {
						inputStream = new FileInputStream(file);
						outStream = new FileOutputStream("E:\\2.txt");
						//读内容  
						//第一个字符的utf-8的编码
						//默认给1024
						byte[] by = new byte[1024];
						//数组中读到的内容的实际的长度
						int len = 0;	
						while((len = inputStream.read(by))!=-1) {
							//System.out.println(inputStream.read(by,0,len));
								System.out.println(len);
								//写数组中的偏移量 数组中实际内容的长度
								outStream.write(by,0,len);
						}
						//阻塞的io流
						System.out.println('一'+0);
					} catch (FileNotFoundException e) {
						e.printStackTrace();
					} catch (IOException e) {
						e.printStackTrace();
					}finally {
						//资源关闭
						//先用后关
						try {
							outStream.close();
						} catch (IOException e) {
							e.printStackTrace();
						}
						try {
							inputStream.close();
						} catch (IOException e) {
							e.printStackTrace();
						}
					}
				}
}

```

### 2.2 高效缓冲流  BufferedInputStream

> 在创建 `BufferedInputStream` 时，会创建一个内部缓冲区数组.默认缓冲区的大小是8192.
>
> 缓冲区就像，勺子，用勺子(缓冲区数组)盛东西在装到袋子(数组)里面会比较的快。
>
> ```java
> public
>  class BufferedInputStream extends FilterInputStream {
> 
>     private static int DEFAULT_BUFFER_SIZE = 8192;
> 
> public BufferedInputStream(InputStream in) {
>         this(in, DEFAULT_BUFFER_SIZE);
>     }
> }
> ```
>
> 使用缓冲区数组结合 数组的方式去读取数据，速率明显提升很大。

```java
package com.xdkj.javase.io;

import java.io.BufferedInputStream;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;
import java.io.InputStream;

public class BufferedInputStreamDemo {

	public static void main(String[] args) {
		
		long start = System.currentTimeMillis();
		//method1();
			method3();
		long end = System.currentTimeMillis();
		System.out.println("method执行时间:"+ (end -start) );
		
		long start1 = System.currentTimeMillis();
		method2();
		long end1 = System.currentTimeMillis();
		System.out.println("method1执行时间:"+(end1- start1));
	}
	
	//带缓冲区的速度更快
	private static void method1() {
		InputStream in;
		BufferedInputStream bufferIn;
		try {
		 in = new FileInputStream("E:\\1.avi");
		 bufferIn = new BufferedInputStream(in);
		 int len = 0;
		 while((len = bufferIn.read())!=-1) {
			 //System.out.println(len);
		 }
		 
		} catch (FileNotFoundException e) {
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		}
	}
	//效率更高
	/*
	 * 缓冲区的数据相当于买米的勺子一样。原始的字节流是一粒一粒的向数组中装数据，
	 * 现在改用勺子向数组中装
	 * 数据了，效率肯定就高了。
	 * 
	 * */
	private static void method3() {
		InputStream in;
		BufferedInputStream bufferIn;
		try {
		 in = new FileInputStream("E:\\1.avi");
		 bufferIn = new BufferedInputStream(in,10240);
		 int len = 0;
		 byte [] by = new byte[1024];
		 while((len = bufferIn.read(by))!=-1) {
			 //System.out.println(new String(by,0,len));
		 }
		} catch (FileNotFoundException e) {
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		}
	}
	
	
	private static void method2() {
		InputStream in;
		try {
		 in = new FileInputStream("E:\\1.avi");
		 int len = 0;
		 
		 while((len= in.read())!=-1) {
			// System.out.println(len);
		 }
		} catch (FileNotFoundException e) {
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		}
	}
}

```

## 3. OutputStream

### 3.1 FileOutputStream

+ write()
+ write(by,0,len)
+ close()
+ flush();

```java
package com.xdkj.javase.io;

import java.io.File;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;

public class FileOutputStreamDemo {

	public static void main(String[] args) {
		//fileOutputStreamMethod2();
		//fileOutputStreamMethod3();
		//fileOutputStreamMethod4();
		fileOutputStreamMethod5();
	}
	//写入一个字节的内容
	public static void fileOutputStreamMethod1() {
		OutputStream outputStream  = null;
		try {
			//在写入内容的时候如果文件不存在会自动创建
			outputStream = new FileOutputStream("E:\\3.txt");
			outputStream.write(97);
		} catch (FileNotFoundException e) {
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		}finally {
			try {
				outputStream.close();
			} catch (IOException e) {
				e.printStackTrace();
			}
		}
	}
	//写入字符串文件
	public static void fileOutputStreamMethod2() {
		OutputStream outputStream  = null;
		try {
			//在写入内容的时候如果文件不存在会自动创建
			outputStream = new FileOutputStream("E:\\3.txt");
			outputStream.write(97);
			outputStream.write(97);
			outputStream.write(97);
			outputStream.write(97);
			//字符串写入的时候要转为字节数组
			outputStream.write("Hello World".getBytes());
		} catch (FileNotFoundException e) {
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		}finally {
			try {
				outputStream.close();
			} catch (IOException e) {
				e.printStackTrace();
			}
		}
	}
	//复制 文件
	public static void fileOutputStreamMethod3() {
		InputStream  inputStream = null;
		OutputStream outputStream  = null;
		try {
			//在写入内容的时候如果文件不存在会自动创建
			inputStream = new FileInputStream("E:\\1.txt");
			outputStream = new FileOutputStream("E:\\3.txt");
			byte []  by = new byte[1024];
			int len = 0;
			while((len = inputStream.read(by))!=-1) {
				// 会写入脏读的数据
				//outputStream.write(by);
				//数组中写入实际读取到的长度
				outputStream.write(by,0,len);
			}
		} catch (FileNotFoundException e) {
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		}finally {
			try {
				outputStream.close();
			} catch (IOException e) {
				e.printStackTrace();
			}
		}
	}
	//复制 图片
		public static void fileOutputStreamMethod4() {
			InputStream  inputStream = null;
			OutputStream outputStream  = null;
			try {
				//在写入内容的时候如果文件不存在会自动创建
				inputStream = new FileInputStream("E:\\MacBuntu-Wallpapers\\20180412031959734.jpg");
				outputStream = new FileOutputStream("E:\\4.jpg");
				byte []  by = new byte[1024];
				int len = 0;
				while((len = inputStream.read(by))!=-1) {
					// 会写入脏读的数据
					//outputStream.write(by);
					//数组中写入实际读取到的长度
					outputStream.write(by,0,len);
				}
			} catch (FileNotFoundException e) {
				e.printStackTrace();
			} catch (IOException e) {
				e.printStackTrace();
			}finally {
				try {
					outputStream.close();
				} catch (IOException e) {
					e.printStackTrace();
				}
			}
		}
		
		public static void fileOutputStreamMethod5() {
			InputStream  inputStream = null;
			OutputStream outputStream  = null;
			try {
				//在写入内容的时候如果文件不存在会自动创建
				inputStream = new FileInputStream("E:\\1.avi");
				outputStream = new FileOutputStream("E:\\5.avi");
				byte []  by = new byte[1024];
				int len = 0;
				while((len = inputStream.read(by))!=-1) {
					// 会写入脏读的数据
					//outputStream.write(by);
					//数组中写入实际读取到的长度
					outputStream.write(by,0,len);
				}
			} catch (FileNotFoundException e) {
				e.printStackTrace();
			} catch (IOException e) {
				e.printStackTrace();
			}finally {
				try {
					outputStream.close();
				} catch (IOException e) {
					e.printStackTrace();
				}
			}
		}
}

```

###  3.2BufferedOutputStream

```java
package com.xdkj.javase.io;

import java.io.BufferedInputStream;
import java.io.BufferedOutputStream;
import java.io.File;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;

public class BufferedOutputStreamDemo {
	public static void main(String[] args) {
		//method1();
		//method2();
		method3();
	}

	private static void method1() {
		try {
			OutputStream  out = new FileOutputStream(new File("E:\\6.txt"));
			BufferedOutputStream bufferOut = new BufferedOutputStream(out);
			bufferOut.write("HelloWorld".getBytes());
			//刷新缓存流 写入数据
			bufferOut.flush();
		} catch (FileNotFoundException e) {
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		}
	}
	//复制文件
	private static void method2() {
		//jdk1.7的io流自动关闭
		try(InputStream in = new FileInputStream("E:\\1.txt");
				BufferedInputStream  bufferIn = new BufferedInputStream(in);
				OutputStream  out = new FileOutputStream(new File("E:\\7.txt"));
				BufferedOutputStream bufferOut = new BufferedOutputStream(out);
			)
		{
			int len = 0;
			while((len = bufferIn.read())!=-1) {
				bufferOut.write(len);
			}
			//刷新缓存流 写入数据
			bufferOut.flush();
		} catch (FileNotFoundException e) {
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		}
	}
	//效率是最快的文件复制
	private static void method3() {
		//jdk1.7的io流自动关闭
		try(InputStream in = new FileInputStream("E:\\5.avi");
				BufferedInputStream  bufferIn = new BufferedInputStream(in);
				OutputStream  out = new FileOutputStream(new File("E:\\7.avi"));
				BufferedOutputStream bufferOut = new BufferedOutputStream(out);
			)
		{
			int len = 0;
			byte[] by = new byte[1024];
			while((len = bufferIn.read(by))!=-1) {
				bufferOut.write(by,0,len);
			}
			//刷新缓存流 写入数据
			bufferOut.flush();
		} catch (FileNotFoundException e) {
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		}
	}
}

```

## 4. 转换流(处理中文乱码)

> InputStreamReader(Inputsream in ,String charSetName)  在读取数据的时候指定编码
>
> OutputStreamWriter(OutputStream out,String chasrsetName); 写入内容的时候指定编码

```java
package com.xdkj.javase.io;

import java.io.BufferedInputStream;
import java.io.BufferedOutputStream;
import java.io.File;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.io.OutputStream;
import java.io.OutputStreamWriter;

public class CoverStreamDemo {
	public static void main(String[] args) {
		//method2();
		methid3();
	}
	//复制文件
		private static void method2() {
			//jdk1.7的io流自动关闭
			try(InputStream in = new FileInputStream("E:\\3.txt");
					BufferedInputStream  bufferIn = new BufferedInputStream(in);
					OutputStream  out = new FileOutputStream(new File("E:\\4.txt"));
					BufferedOutputStream bufferOut = new BufferedOutputStream(out);
				)
			{
				int len = 0;
				byte [] by = new byte[1024];
				while((len = bufferIn.read(by))!=-1) {
					bufferOut.write(by,0,len);
				}
				//刷新缓存流 写入数据
				bufferOut.flush();
			} catch (FileNotFoundException e) {
				e.printStackTrace();
			} catch (IOException e) {
				e.printStackTrace();
			}
		}
		//转换流  转换流式解决文件乱码的
		public static void methid3() {
			//jdk1.7的io流自动关闭
			try(InputStream in = new FileInputStream("E:\\7.txt");
					BufferedInputStream  bufferIn = new BufferedInputStream(in);
					OutputStream  out = new FileOutputStream(new File("E:\\8.txt"));
					BufferedOutputStream bufferOut = new BufferedOutputStream(out);
					//解码
					InputStreamReader  inReader = new InputStreamReader(bufferIn,"gb2312");
					//编码
					OutputStreamWriter   ouWriter = new OutputStreamWriter(bufferOut,"utf-8");
					/*我 ----> 25102   gb2312   utf-8 ----> 乱码的字
					 * 
					 * */
				)
			{
				int len = 0;
				char [] by = new char[1024];
				while((len = inReader.read(by))!=-1) {
					ouWriter.write(by,0,len);
				}
				//刷新缓存流 写入数据
				ouWriter.flush();
			} catch (FileNotFoundException e) {
				e.printStackTrace();
			} catch (IOException e) {
				e.printStackTrace();
			}
		}
}

```

##  5.Reader

> 适合于读取字符流。一般使用与读取文本文件(windows的记事本可以打开的文件)。

```java
package com.xdkj.javase.io;

import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.IOException;
import java.io.Reader;

public class ReaderDemo {

	public static void main(String[] args) {
		//method1();
		method2();
	}

	private static void method1() {
		try {
			Reader  reader = new FileReader("E:/1.txt");
			int  len = 0;
			while((len = reader.read())!=-1) {
				System.out.println(len);
			}
		} catch (FileNotFoundException e) {
			e.printStackTrace();
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}
	
	private static void method2() {
		try {
			Reader  reader = new FileReader("E:/1.txt");
			int  len = 0;
			char [] ch = new char[1024];
			while((len = reader.read(ch))!=-1) {
				System.out.println(ch);
			}
		} catch (FileNotFoundException e) {
			e.printStackTrace();
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}

}

```

## 6.Writer

```java
package com.xdkj.javase.io;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;
import java.io.Reader;
import java.io.Writer;

public class BufferedReaderWriterDemo {

	public static void main(String[] args) {
		//method1();
		method2();
	}

	private static void method1() {
		try (Reader  reader = new FileReader("E:/1.txt");
				BufferedReader  bufferReader = new BufferedReader(reader);
				
				Writer writer = new FileWriter("e:/10.txt");
				BufferedWriter bufferWriter = new BufferedWriter(writer);)
		{
			char [] ch = new char[1024];
			int len = 0;
			while((len = bufferReader.read(ch))!=-1) {
				bufferWriter.write(ch, 0, len);
			}
			bufferWriter.flush();
		} catch (FileNotFoundException e) {
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		}
	}
	
	private static void method2() {
		//流资源的自动关闭
		try (Reader  reader = new FileReader("E:/1.txt");
				BufferedReader  bufferReader = new BufferedReader(reader);
				
				Writer writer = new FileWriter("e:/11.txt");
				BufferedWriter bufferWriter = new BufferedWriter(writer);)
		{
			String  str = null;
			int len = 0;
			//按行读取  根据\r\n判断行结束符号
			while((str = bufferReader.readLine())!=null) {
				bufferWriter.write(str);
				//bufferWriter.write("\r\n");
				//换行
				bufferWriter.newLine();
			}
			//刷新缓冲区
			bufferWriter.flush();
		} catch (FileNotFoundException e) {
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		}
	}

}

```

> 对于图片。视频。音频。。。除文本意外的资源复制有四种方式
>
> 文本资源复制有9种方式:

## 7. 对象流

> 我们在程序开发中经常使用new关键字创建类的实例化对象，对象一般在方法找那个使用，方法执行完成对象就等待gc回收。
>
> 对象创建出来是在运行内存中保存的，我想把这个对象永久的保存下来怎么办?
>
> 把对象按照一定的规则写入文件中再使用的时候按照一定的规则读出来。
>
> 按照规则将对象写入文件称之为序列化   按照规则读出来成为反序列化。
>
> **把对象转换为字节序列的过程称为对象的序列化**。
> 　　**把字节序列恢复为对象的过程称为对象的反序列化**。
> 　　对象的序列化主要有两种用途：
> 　　1） 把对象的字节序列永久地保存到硬盘上，通常存放在一个文件中；
> 　　2） 在网络上传送对象的字节序列。
>
> 　　在很多应用中，需要对某些对象进行序列化，让它们离开内存空间，入住物理硬盘，以便长期保存。比如最常见的是Web服务器中的Session对象，当有 10万用户并发访问，就有可能出现10万个Session对象，内存可能吃不消，于是Web容器就会把一些seesion先序列化到硬盘中，等要用了，再把保存在硬盘中的对象还原到内存中。
>
> 　　当两个进程在进行远程通信时，彼此可以发送各种类型的数据。无论是何种类型的数据，都会以二进制序列的形式在网络上传送。发送方需要把这个Java对象转换为字节序列，才能在网络上传送；接收方则需要把字节序列再恢复为Java对象。



```java
package com.xdkj.javase.io;

import java.io.Serializable;

public class Student implements Serializable{
	/**
	 *  动态id
	 *  uuid
	 */
	private static final long serialVersionUID = 6174239004227470490L;
	
	
	private int age;
	private String name;
	private String email;
	//瞬时的
	transient String address;
	
	public Student() {
		super();
	}
	public Student(int age, String name, String email) {
		super();
		this.age = age;
		this.name = name;
		this.email = email;
	}
	public int getAge() {
		return age;
	}
	public void setAge(int age) {
		this.age = age;
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public String getEmail() {
		return email;
	}
	public void setEmail(String email) {
		this.email = email;
	}
	public String getAddress() {
		return address;
	}
	public void setAddress(String address) {
		this.address = address;
	}
	
	
	/*
	 * @Override public String toString() { return "Student [age=" + age + ", name="
	 * + name + ", email=" + email + "]"; }
	 */
	
}

```

```java
package com.xdkj.javase.io;

import java.io.Serializable;

public class Person  implements Serializable{
	/**
	 * 
	 */
	private static final long serialVersionUID = 2303898885138016551L;
	private int age;
	private String name;
	private String address;
	public Person() {
		super();
		// TODO Auto-generated constructor stub
	}
	public Person(int age, String name, String address) {
		super();
		this.age = age;
		this.name = name;
		this.address = address;
	}
	public int getAge() {
		return age;
	}
	public void setAge(int age) {
		this.age = age;
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public String getAddress() {
		return address;
	}
	public void setAddress(String address) {
		this.address = address;
	}
	@Override
	public String toString() {
		return "Person [age=" + age + ", name=" + name + ", address=" + address + "]";
	}
	
}

```

```java
package com.xdkj.javase.io;

import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.ObjectInputStream;
import java.io.ObjectOutputStream;

import com.xdkj.javase.io.Student;

public class ObjectStreamDemo {
	
	public static void main(String[] args) {
		method1();
		method2();
		//System.out.println(UUID.randomUUID());
	}

	private static void method1() {
		Student student = new Student(23,"joke","1888888@qq.com");
		Student student1 = new Student(25,"lucy","99999@qq.com");
		Person person = new Person(26,"admin","陕西省西安市");
		System.out.println(student);
		System.out.println(student1);
		//使用对象流
		try {
			//序列化写入
			ObjectOutputStream  objOut = new ObjectOutputStream(new FileOutputStream("E:/obj.txt"));
			//将对象写入文件中
			//java.io.NotSerializableException: com.xdkj.javase.io.Student
				objOut.writeObject(student);
				objOut.writeObject(student1);
				objOut.writeObject(person);
			//反序列化读取
				
		} catch (FileNotFoundException e) {
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		}
	}
	//反序列化
	//怎么保证从文件中读取对象的时候是完整的?
	//按照对象的序列化顺序去读取的，顺序不一致存在类转换异常
	//
	private static void method2() {
		try {
			ObjectInputStream  objIn=  new ObjectInputStream(new FileInputStream("E:/obj.txt"));
				Student student = (Student)	objIn.readObject();
				System.out.println(student);
				
				Student student1 = (Student)	objIn.readObject();
				System.out.println(student1);
				
				Person person = (Person)objIn.readObject();
				System.out.println(person);
				
				
		} catch (FileNotFoundException e) {
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		} catch (ClassNotFoundException e) {
			e.printStackTrace();
		}
	}

}

```



## 8. 内存流

## 9. 随机流

## 10.合并流

## 11. 打印流

 
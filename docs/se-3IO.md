### File
- java.io.File类：**文件和文件目录路径**的抽象表示形式，与平台无关
- File 能新建、删除、重命名文件和目录，但File不能访问文件内容本身。
- 如果需要访问文件内容本身，则需要使用输入/输出
- 想要在Java程序中表示一个真实存在的文件或目录，那么必须有一个File对 象，但是Java程序中的一个File对象，
可能没有一个真实存在的文件或目录。
- File对象可以作为参数传递给流的构造器
##### File-常用构造器
- public File(String pathname)
以pathname为路径创建File对象，可以是绝对路径或者相对路径
- public File(String parent,String child)
 以parent为父路径，child为子路径创建File对象。
- public File(File parent,String child)
根据一个父File对象和子文件路径创建File对象
##### File-路径分隔符
- 路径中的每级目录之间用一个路径分隔符隔开
- 路径分隔符和系统有关：
    1、windows和DOS系统默认使用“\”来表示
    2、UNIX和URL使用“/”来表示
- public static final String separator。根据操作系统，动态的提供分隔符
##### File-常用方法
###### 获取功能
- public String getAbsolutePath()：获取绝对路径
- public String getPath() ：获取路径
- public String getName() ：获取名称
- public StringgetParent()：获取上层文件目录路径。若无，返回null
- public long length() ：获取文件长度（即：字节数）。不能获取目录的长度
- public long lastModified()：获取最后一次的修改时间，毫秒值
- public String[]  list()：获取指定目录下的所有文件或者文件目录的名称数组
- public File[] listFiles()：获取指定目录下的所有文件或者文件目录的File数组
###### 重命名功能
- public boolean renameTo(File dest):把文件重命名为指定的文件路径
###### 判断功能
- ==public boolean isDirectory()==：判断是否是文件目录
- ==public boolean isFile()== ：判断是否是文件
- ==public boolean exists()== ：判断是否存在
- public boolean canRead() ：判断是否可读
- public boolean canWrite() ：判断是否可写
- public boolean isHidden() ：判断是否隐藏
###### 创建功能
- ==public boolean createNewFile()== ：创建文件。若文件存在，则不创建，返回false
- public boolean mkdir()：创建文件目录。如果此文件目录存在，就不创建了。
如果此文件目录的上层目录不存在，也不创建
- ==public boolean mkdirs()== ：创建文件目录。如果上层文件目录不存在，一并创建
 ==注意事项：如果你创建文件或者文件目录没有写盘符路径，那么，默认在项目路径下。==
###### 删除功能
- ==public boolean delete()==：删除文件或者文件夹
==删除注意事项：
Java中的删除不走回收站。 要删除一个文件目录，请注意该文件目录内不能包含文件或者文件目录==
```java
File file = new File("hello.txt");
file.createNewFile();
```

### IO
##### 原理
- I/O是Input/Output的缩写， I/O技术是非常实用的技术，用于==处理设备之间的数据传输==。如读/写文件，网络通讯等
-  Java程序中，对于数据的输入/输出操作以“==流(stream)==” 的
方式进行。
-  java.io包下提供了各种“流”类和接口，用以获取不同种类的
数据，并通过标准的方法输入或输出数据。
- ==**输入input**==：读取外部数据（磁
盘、光盘等存储设备的数据）到
程序（内存）中
- ==**输出output**==：将程序（内存）数据输出到磁盘、光盘等存储设备中。
##### 流的分类
- 按操作数据单位不同分为：字节流(8 bit)，字符流(16 bit)
- 按数据流的流向不同分为：输入流，输出流
- 按流的角色的不同分为：节点流，处理流
##### 节点流和处理流
- 节点流：直接从数据源或目的地读写数据
```
graph LR
数据源-->程序
```

- 处理流：不直接连接到数据源或目的地，而是“连接”在已存
在的流（节点流或处理流）之上，通过对数据的处理为程序提
供更为强大的读写功能。
##### InputStream & Readere
- InputStream 和 Reader 是所有输入流的基类。
- InputStream（典型实现：FileInputStream）
    int read()
    ==int read((byte[] b)==
    int read((byte[] b, int off, int len)
- Reader(典型实现：FileReader)
    int read()
    ==int read(char cbuf[])==
    int read(char cbuf[], int off, int len)
- FileInputStream从文件系统中的某个文件中获得输入字节。FileInputStream 用于读取非文本数据之类的原始字节流。要读取字符流，需要使用 FileReader
##### InputStream
- int read():
从输入流中读取数据的下一个字节。返回 0 到 255 范围内的 int 字节值。如果因为已经到达流末尾而没有可用的字节，则返回值-1。
- int read(byte[] b):从此输入流中将最多 b.length个字节的数据读入一个 byte 数组中。如果因为已
经到达流末尾而没有可用的字节，则返回值 -1。否则以整数形式返回实际读取的字节数
- int read(byte[] b, int off,int len):将输入流中最多 len 个数据字节读入 byte 数组。尝试读取 len 个字节，但读取
的字节也可能小于该值。以整数形式返回实际读取的字节数。如果因为流位于
文件末尾而没有可用的字节，则返回值 -1。
- public void close() throws IOException：关闭此输入流并释放与该流关联的所有系统资源。
##### Reader
- int read()：读取单个字符。作为整数读取的字符，范围在 0 到 65535 之间 (0x00-0xffff)（2个
字节的Unicode码），如果已到达流的末尾，则返回 -1
- int read(char[] cbuf)：将字符读入数组。如果已到达流的末尾，则返回 -1。否则返回本次读取的字符数。
- int read(char[] cbuf,int off,int len)：将字符读入数组的某一部分。存到数组cbuf中，从off处开始存储，最多读len个字
符。如果已到达流的末尾，则返回 -1。否则返回本次读取的字符数。
- public void close() throws IOException：关闭此输入流并释放与该流关联的所有系统资源。
```java
//1、FileReader流的实例化
FileReader fileReader = null;
try {
    fileReader = new FileReader(new File("hello.txt"));
    //2、读的操作
    char[] cbuf = new char[1024];
    int len;
    while((len = fileReader.read(cbuf)) != -1){
        System.out.println(new String(cbuf,0,len));
    }
} catch (IOException e) {
    e.printStackTrace();
}finally {
    //4、关流
    try {
        if(fileReader != null){
            fileReader.close();
        }
    } catch (IOException e) {
        e.printStackTrace();
    }
}
```
##### OutputStream & Writer
OutputStream 和 Writer 也非常相似：
- void write(int b/int c);
- void write(byte[] b/char[] cbuf);
- void write(byte[] b/char[] buff, int off, int len);
- void flush();
- void close(); 需要先刷新，再关闭此流

因为字符流直接以字符作为操作单位，所以 Writer 可以用字符串来替换字符数组，
即以 String 对象作为参数
- void write(String str);
- void write(String str, int off, int len);

FileOutputStream 从文件系统中的某个文件中获得输出字节。FileOutputStream
用于写出非文本数据之类的原始字节流。要写出字符流，需要使用 FileWriter
##### Writer
- void write(int c)
写入单个字符。要写入的字符包含在给定整数值的 16 个低位中，16 高位被忽略。 即
写入0 到 65535 之间的Unicode码。  void write(char[] cbuf)
写入字符数组。
- void write(char[] cbuf,int off,int len)
写入字符数组的某一部分。从off开始，写入len个字符
- void write(String str)
写入字符串。
- void write(String str,int off,int len)
写入字符串的某一部分。
- void flush()刷新该流的缓冲，则立即将它们写入预期目标。
- public void close() throws IOException
关闭此输出流并释放与该流关联的所有系统资源。


    /**
     * 拷贝字符:注意中文会乱码
     */
    @Test
    public void writeChar(){
        FileReader fr = null;
        FileWriter fw = null;
        try {
            //1、造流
            fr = new FileReader("hello.txt");
            fw = new FileWriter("hello2.txt");
            //2、复制
            char[] cbuf = new char[4];
            int len;
            while ((len = fr.read(cbuf)) != -1) {
                fw.write(cbuf, 0, len);
            }
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if (fr != null) {
                try {
                    fr.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if (fw != null) {
                try {
                    fw.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }

     /**
     * 拷贝字节
     */
    @Test
    public void writeBytes(){
      FileInputStream fis = null;
      FileOutputStream fos = null;
        try {
            //1、造流
            fis = new FileInputStream("image.png");
            fos = new FileOutputStream("image2.png");
            //2、复制
            byte[] buf = new byte[4];
            int len;
            while((len = fis.read(buf)) != -1){
                fos.write(buf,0,len);
            }
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }finally {
            if(fis != null){
                try {
                    fis.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if(fos != null){
                try {
                    fos.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }

    结论：
    1、对于文本文件(.txt,.java,.c,.cpp)，使用字符流处理
    2、对于非文本文件(.jpg,.mp3,.mp4,.avi,.doc,.ppt,...)，使用字节流处理

#### 处理流
##### 处理流-缓冲流
- 为了提高数据读写的速度，Java API提供了带缓冲功能的流类，在使用这些流类
时，会创建一个内部缓冲区数组，缺省使用==8192个字节==(8Kb)的缓冲区。
- 缓冲流要“套接”在相应的节点流之上，根据数据操作单位可以把缓冲流分为：
    BufferedInputStream 和 BufferedOutputStream
    BufferedReader 和 BufferedWriter
- 当读取数据时，数据按块读入缓冲区，其后的读操作则直接访问缓冲区
- 当使用BufferedInputStream读取字节文件时，BufferedInputStream会一次性从
文件中读取8192个(8Kb)，存在缓冲区中，直到缓冲区装满了，才重新从文件中
读取下一个8192个字节数组。
- 向流中写入字节时，不会直接写到文件，先写到缓冲区中直到缓冲区写满，
BufferedOutputStream才会把缓冲区中的数据一次性写到文件里。使用方法
flush()可以强制将缓冲区的内容全部写入输出流
- 关闭流的顺序和打开流的顺序相反。只要关闭最外层流即可，关闭最外层流也
会相应关闭内层节点流
- flush()方法的使用：手动将buffer中内容写入文件
- 如果是带缓冲区的流对象的close()方法，不但会关闭流，还会在关闭流之前刷
新缓冲区，关闭后不能再写出


    /**
     * 拷贝字符-缓冲流
     */
    @Test
    public void writeChar(){
        BufferedReader br = null;
        BufferedWriter bw = null;
        try {
            // 创建缓冲流对象：它是处理流，是对节点流的包装
            br = new BufferedReader(new FileReader("hello.txt"));
            bw = new BufferedWriter(new FileWriter("hello3.txt"));
            String str;
            //readLine 一次读取一行
            while((str = br.readLine()) != null){
                // 一次写入一行字符串
                bw.write(str);
                // 写入行分隔符
                bw.newLine();
            }
            // 刷新缓冲区
            bw.flush();
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if (br != null) {
                try {
                    // 关闭过滤流时,会自动关闭它所包装的底层节点流
                    br.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if (bw != null) {
                try {
                    bw.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }

##### 处理流-转换流
###### 特点
- 转换流提供了在字节流和字符流之间的转换
- Java API提供了两个转换流：
    ==InputStreamReader：将InputStream转换为Reader==
    ==OutputStreamWriter：将Writer转换为OutputStream==
- 字节流中的数据都是字符时，转成字符流操作更高效。
- 很多时候我们使用转换流来处理文件乱码问题。实现编码和
解码的功能。
###### InputStreamReader
- 实现将字节的输入流按指定字符集转换为字符的输入流。
- 需要和InputStream“套接”。
- 构造器：


    public InputStreamReader(InputStream in)
    public InputSreamReader(InputStream in,String charsetName)
    Reader isr = new InputStreamReader(System.in,”gbk”);

###### OutputStreamWriter
- 实现将字符的输出流按指定字符集转换为字节的输出流。
- 需要和OutputStream“套接”。
- 构造器：


    public OutputStreamWriter(OutputStream out)
    public OutputSreamWriter(OutputStream out,String charsetName)

转换流示例


    FileInputStream fis = new FileInputStream("hello.txt");
    FileOutputStream fos = new FileOutputStream("hello5.txt");

    InputStreamReader isr = new InputStreamReader(fis, "gbk");
    OutputStreamWriter osw = new OutputStreamWriter(fos,"gbk");

    BufferedReader bufferedReader = new BufferedReader(isr);
    BufferedWriter bufferedWriter = new BufferedWriter(osw);

    String str;
    while((str = bufferedReader.readLine()) != null){
        bufferedWriter.write(str);
        bufferedWriter.newLine();
        bufferedWriter.flush();
    }
    bufferedReader.close();
    bufferedWriter.close();
###### 字符编码
- 编码：字符串-字节数组
- 解码：字节数组-字符串
##### 处理流-标准输入、输出流（了解）
###### 特点
- System.in和System.out分别代表了系统标准的输入和输出设备
- 默认输入设备是：键盘，输出设备是：显示器
- System.in的类型是InputStream
- System.out的类型是PrintStream，其是OutputStream的子类
FilterOutputStream 的子类
- 重定向：通过System类的setIn，setOut方法对默认设备进行改变。
    public static void setIn(InputStream in)
    public static void setOut(PrintStream out)
##### 处理流-对象流
###### ObjectInputStream和OjbectOutputSteam
- 用于存储和读取基本数据类型数据或对象的处理流。它的强大之处就是可以把Java中的对象写入到数据源中，也能把对象从数据源中还原回来。
- ==序列化==：用ObjectOutputStream类保存基本类型数据或对象的机制
- ==反序列化==：用ObjectInputStream类读取基本类型数据或对象的机制
- ObjectOutputStream和ObjectInputStream不能序列化==static==和==transient==修饰的成员变量
###### 对象的序列化
- 若某个类实现了Serializable接口，该类的对象就是可序列化的：
    1、创建一个 ObjectOutputStream
    2、调用 ObjectOutputStream 对象的 writeObject(对象) 方法输出可序列化对象
    3、注意写出一次，操作flush()一次
- 反序列化：
    1、创建一个 ObjectInputStream
    2、调用 readObject() 方法读取流中的对象
强调：如果某个类的属性不是基本数据类型或String类型，而是另一个引用类型，那么这个引用类型必须是可序列化的，否则拥有该类型的Field的类也不能序列化
- 序列化：将对象写入到磁盘或者进行网络传输。


    //创建对象流
    ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream(“data.txt"));
    Person p = new Person("韩梅梅", 18, "中华大街", new Pet());
    oos.writeObject(p);
    oos.flush();
    oos.close();


- 反序列化：将磁盘中的对象数据源读出。


    ObjectInputStream ois = new ObjectInputStream(new FileInputStream(“data.txt"));
    Person p1 = (Person)ois.readObject();
    System.out.println(p1.toString());
    ois.close();

###### java.io.Serializable接口
- 实现了Serializable接口的对象，可将它们转换成一系列字节，并可在以后
完全恢复回原来的样子。这一过程亦可通过网络进行。这意味着序列化机
制能自动补偿操作系统间的差异。换句话说，可以先在Windows机器上创
建一个对象，对其序列化，然后通过网络发给一台Unix机器，然后在那里
准确无误地重新“装配”。不必关心数据在不同机器上如何表示，也不必
关心字节的顺序或者其他任何细节。
- 由于大部分作为参数的类如String、Integer等都实现了
java.io.Serializable的接口，也可以利用多态的性质，作为参数使接口更
灵活。
#####  随机存取文件流
###### 特点
- RandomAccessFile声明在java.io包下，但直接继承于java.lang.Object类。并且它实现了DataInput、DataOutput这两个接口，也就意味着这个类既可以读也可以写。
- RandomAccessFile 类支持 “随机访问”的方式，程序可以直接跳到文件的任意
地方来读、写文件：
    1、支持只访问文件的部分内容
    2、可以向已存在的文件后追加内容
- RandomAccessFile 对象包含一个记录指针，用以标示当前读写处的位置，RandomAccessFile 类对象可以自由移动记录指针：
    1、long getFilePointer()：获取文件记录指针的当前位置
    2、void seek(long pos)：将文件记录指针定位到 pos 位置
###### RandomAccessFile 类
- 构造器


    public RandomAccessFile(File file, String mode)
    public RandomAccessFile(String name, String mode)

- 创建 RandomAccessFile 类实例需要指定一个 mode 参数，该参数指
定RandomAccessFile 的访问模式：
    1、r: 以只读方式打开
    2、rw：打开以便读取和写入
    3、rwd:打开以便读取和写入；同步文件内容的更新
    4、rws:打开以便读取和写入；同步文件内容和元数据的更新
- 如果模式为只读r。则不会创建文件，而是会去读取一个已经存在的文件，
如果读取的文件不存在则会出现异常。 如果模式为rw读写。如果文件不
存在则会去创建文件，如果存在则不会创建。


    RandomAccessFile raf = new RandomAccessFile("hello.txt", "rw");
    //设置指针偏移量
    raf.seek(2);
    //读的操作
    byte[] buf = new byte[1024];
    int len;
    while ((len = raf.read(buf)) != -1) {
        System.out.print(new String(buf, 0, len));
    }
        
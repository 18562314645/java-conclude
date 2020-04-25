---
typora-root-url: ./
---

​                                                                 **java总结**

java相关的博客：<https://blog.kuangstudy.com/>

 **1. java的跨平台原理**

​	应为java有自己的虚拟机在不同平台上运行java虚拟机使得接口统一，部通平台上jvm不同，java通过不同版本及不同位数的jvm来屏蔽不同的系统间的指令集的差异，对外提供统一的javaapi接口，

**2.java基础知识**

​      java中有8中数据类型 int 8位4个字节  boolean 1 位   char  2字节  byte 1字节  short 2字节  long  8字节  float 4字节  double 8字节

**3.面向对象的特征有哪些方面**

​     封装（高度自治的封闭个体，对外提供获取自己或改变自己的方法），继承（可以继承一个类的的同时改变其中的一些内容），多态（引用变量指向具体类型 父类已用指向子类对象），抽象（把现实生活中的共同特征对象抽象为类）

**4.基本类型与包装类型**

​     为什么要有包装类型 ？java是一个面向对象的语言而基本的数据类型部具备面向对象的特性 如

null->integer 0->int 在数据库中容易歧义

**5.“==”和equals方法有什么区别**

"=="用来判断两个变量之间的值是否相等，变量分为基本数据类型和引用数据类型，基本数据类型直接比较值，而引用数据类型比较的是地址值

“equals” 用来比较两个对象长得是否一样，判断两个对象的某些特征是否一样，实际上就是调用对象的equals方法，基本数据类型没有equals方法

**6.string 和stringbuilder，stringbuffer和stringbuilder的区别**

string 是内容不可变的字符串，底层是一个不可变的字符数组（final char[]），而stringbuilder和stringbuffer是内容可变的字符串，底层使用的可变的字符数组可用append方法改变，拼接字符串不能使用string进行拼接，要使用stringbuffer和stringbuilder     stringbuffer和stringbuilder的区别stringbuffer线程安全，效率低和stringbuilder线程不安全，效率高

**7.java中的集合**

​	java中的集合分为value和key-value(collection map)两种

​     存储值分为list和set 存储key-value为map

​	list是有序的可重复的

​	set是无序的不可重复的，根据equals和hashcode来判断，也就是如果一个对象要存储到set中必须要重写equals和hashcode方法

**8.list**

​	list常用的arraylist和linklist，区别和使用场景

​	arraylist底层使用的数组（具有索引查询特定的元素很快而插入和删除修改比较慢，因为数组在内存中是一块连续的内存，如果插入删除时需要移动内存），linklist底层使用链表（不要求内存是连续的，在当前元素中存放上一个和下一个元素的地址查询时需要从头部开始一个一个的找索引，查询效率低而插入时不需要移动内存，只需改变引用指向即可，所以插入或者删除的效率高）

arraylist使用在查询比较多，但是插入和删除比较少的情况，linklist相反

**9.hashMap和hashTable，currenthashmap的**区别

​	hashmap和hashtable都可以使用存储key-value的数据，hashmap是可以把null作为key或value的，而hashtable是不可以的，hashmap是线程不安全的，效率高，而hashtable是线程安全的，效率低

​	既想线程安全又想效率高？currenthashmap （把大的分成多个小的）通过把整个map分为N个segment（类似hashtable），可以提供相同的线程安全，但是效率提升N倍，默认提升16倍

hashMap和treeMap的区别？1.首先hashMap和treeMap都是线程不安全的；2.hashMap是基于哈希表实现的， 使用HashMap要求添加的键类明确定义了hashCode()和equals() treeMap是基于红黑树实现的， TreeMap没有调优选项，因为该树总处于平衡状态；3.hashMap是无序的，treeMap是有序的。

**10.实现一个拷贝文件的工具使用自字节流是字符流**

​	纯文本用字符流，其他用（有声音图片的）字节流

**11.线程的几种实现方式，怎么启动？怎么区分？线程池？线程病发率**

​	方式1，通过继承Thread类实现一个线程    继承的扩展性不强，java只有单继承，如果一个类继承Thread就不能继承其他类了

​	方式2，通过实现Rannable接口实现一个线程

​	怎么启动？Thread thread =new Thread(继承了Thread的对象/实现了Runnable接口) Thread.start(启动线程的方法)  启动后执行的是run方法

​	怎么区分线程？在一个系统中有很多线程，每个线程都会打印日志，我想区分是哪个线程怎样标识？可以设置一个线程名称 thread.set("name") 是一种规范

**12.有没有使用过线程并发库？**

​	线程池的作用？限定线程的个数，不会导致由于线程过多导致系统运行缓慢或崩溃；线程池在开始不需要。后期会增加

**13.设计模式，常用的有哪些**？

​	设计模式就是经过前人无数次实践过程中可以反复使用解决特定问题的设计方法。

​	**常用的是**：单例模式  分为饱汉式（需要的时候才创建实例）饿汉式（一出来就创建单实例） 1.构造方法私有化，让除了自己类中能创建外，其他地方都不能创建     2.在自己的类中创建一个单实例  3.提供一个方法获取该实例对象

```java
饿汉式

public class Singleton {  

    private static final Singleton instance = new Singleton();  

    private Singleton (){}  

    public static Singleton getInstance() {  

     return instance;  

    }  

}


懒汉式

public class Singleton {  

    private static Singleton instance;  

    private Singleton (){}   

    public static Singleton getInstance() {  

     if (instance == null) {  

         instance = new Singleton();  

    }  

    return instance;  

    }  

}  
```

​	工厂模式：springIOC就是使用了工厂模式，对象的创建交给一个工厂去创建

​	代理模式：SpringAOP就是使用的动态代理

​	包装模式

**14.http get和post的区别？**

​	get 请求的参数会符在url之后（就是把数据放置在http协议头中），以？分割，多个参数用&连接；post提交：把提交的数据放置在http的包体中，因此get在地址栏能看到，post看不到；

​	传输数据大小get（数据有限），post（没有）；

​	安全性get（地址栏会显示） post（不显示）

**15.说下对servlet的理解？**

​	servlet是服务器端的程序，运行在服务器端主要用于交互式浏览和修改数据，生成动态web内容，httpServlet重写doGet和doPost方法，也可以重写service方法完成get post的请求

**16，servlet的生命周期**

​	它的生命周期由java.servlet接口的init，service和destroy方法来表达

​	servlet启动时，开始加载servlet生命周期开始。servlet被服务器实例化后，容器运行其init方法，请求到达时运行service方法，service方法自动请求对应的doxx方法，当服务器销毁实例时调用destroy方法

**17.jsp和servlet有哪些相同点和不同点，它们之间的联系是什么？**

​	所有的jsp文件都会被翻译为一个继承HttpServlet的类，也就是jsp最终也是一个servlet，这个servlet对外提供服务

​	不同点：jsp侧重于视图，而servlet主要用于控制逻辑l

​	jsp中9个内置对象：

request，response,pagecontext,session,application,out,config,page,exception

​	jsp中4大作用域：

pageContext，request，session，application

​	jsp传值：request，session，application，cookie

**18.session和cookie的区别**

​	cookie在客户端记录用户信息，session是在服务端，但是session的实现依赖于cookie，sessionId存放在cookie中，单个cookie保存数据不能超过4k，一个站点最多20 个cookie，当客户端禁用cookie时，就采用cookie+数据库方式

**19.数据库**

​	非关系型数据库：redis，memcache,mongodb,hadoop等

关系型数据库的三泛式：

​	第一范式，是根据数据库表中的每一列都不可以分割的基本数据项，同一列中不能有多个值，即实体类中的某个属性不能有多个值或者不能有重复的属性，（列数据不可分割）

​	第二范式，数据库表中的每行必须可以被唯一区分，为实现区分通常为表加上一列，存储各个实例的唯一标识。（即主键）

​	第三范式，要求一个数据库表中不包含已在其他表中已包含的非主键字信息（外键）

反三范式：有的时候为了效率，可以设置重复字段 

**20.事务（ACID）**

​	原子性 ：表示事务操作不可分割，要么成功，要么失败

​        一致性：要么都成功，要么都失败，后面失败了要对前面的操作进行回滚 

​	 隔离性：一个事务开始后不能受其他事务干扰

 	持久性：表示事务开始了就不能终止可持久到硬盘

**21.mysql数据库的默认的最大连接数**

​	为什么需要最大连接数？特定服务器上的数据库只能支持一定数目的连接，数据库安装时都会有一个最大连接数100，我们一般都会设置最大连接时

**22.mysql分页和oracl分页**

​	mysql用limit进行，limit offset，size

​	oracl的分页有点记不住，使用了三层嵌套查询

**23.触发器**

​	触发器要有触发条件，触发器效率高

**24.存储过程**

**25.简单说下你对jdbc的理解**

​	java database connection java只定义接口，让数据厂商自己实现接口，对于我们而言，只需要导入对应厂商开发的实现即可，然后以接口方式进行调用（mysql+mysql驱动即mysql接口实现+jdbc）。

**26.jdbc中preparedStatement相比statement的好处**

​	1.preparedstatement是预编译的，比statement速度快，还能有效防止sql注入

​	2.代码的可读性和可维护性好

**27.写一个简单的jdbc的程序？**

​	“贾连欲执事”    加载驱动  获取连接（DriverManager.getconnection(url,user,pw )）  设置参数  执行  释放连接（释放连接要从小到大，放在finaly里）

**28.数据库连接池的作用？**

​	限定个数，节约系统资源，加快响应时间

**29.介绍 一下ajax？**

​	什么是ajax？（异步的javascript和xml）作用是什么？（数据异步交换，局部刷新数据）怎么实现？（ajaxXmlhttprequest对象，使用这个对象异步发送数据，获取响应，完成局部更新）应用场景？（登录场景，失败时跳转，注册时提示用户名是否存在，二级联动等）

**30.js和jquery？**

​	jQuery是一个js框架，封装了js的属性和方法，并且增强了js的功能，让用户使用起来更加便利，原来使用js时要处理兼容性问题，现在有jQuery封装了底层好多了，原生的js的dom和事件绑定非常麻烦。

**31.jquery的常用选择器？**

​	ID选择器，class选择器，标签选择器，通用选择器

**32.jquery中的ajax和原生js实现ajax有什么关系？**

​	jquery中的ajax也是通过原生的js封装的，如果采用原生的js实现ajax是麻烦的，即使我们不使用jquery也要封装对象的方法和属性。

**33.spring的核心**

​	spring是IOC和AOP的容器  IOC控制反转，我的service需要调用dao，service就需要创建dao，在使用spring之后，spring发现你的service依赖与dao就给你注入。核心原理：就是工厂模式（容器map）+反射+配置文件。

​	AOP：面向切面编程，核心原理：使用动态代理的方式在执行前后或出现异常做相关的逻辑，我们主要使用aop做 （1.事务处理，2.权限判断 3.日志）

**34.spring的事物的传播特性**

**35.spring解析**（<https://blog.csdn.net/java_lyvee/article/details/101793774>）

​	1.spring中的循环依赖怎解决的？spring中是默认单例支持循环的

​	2.怎么证明他默认他默认支持的？怎么关闭循环依赖？spring解决循环依赖的细节

依赖注入的功能---在初始化时完成，初始化时干的工作？

​	1.初始化bean--bean有一个初始化的过程-------spring bean的生命周期

​	2.spring的生命周期到底在哪个步骤完成的依赖注入？

​	3.spring bean的产生过程------------------bean是由什么产生来的

​		class-----beanDefinition----------object（bean）

  	4.spring的实例化流程 ：（1）先scan扫描类，把要创建的类扫描出来，进行一个for循环拿到扫描出来的类，但是他不知道要不要创建，所以它要进行解析，（2）创建了一个beandefinition类，然后把类的属性set进去（比如是不是懒加载，或者类的scope），解析完后，（3）把他放put到一个map中；（4）然后看看你是否对spring进行了扩展，如果要扩展要实现一个beanfactorypoatprocessor；（5）遍历map，将解析出来的类遍历出来在决定要不要new

**36.spring bean的作用域**

​	bean的作用域范围可以再scope属性中设置，默认情况下，spring只为每个在IOC容器中声明的bean创建一个都实例，整个容器范围内都能共享该实例，所有后续的getbean（）都返回唯一的bean实例，该作用域成为singleton，还有prototype域（每次调用getbean时会返回一个新实例调用）   

request域（每次HTTP请求回创建一个新的bean）  session域（在一个会话中共享一个bean）

**springmvc流程：** 

![icon](/assert/14.png)

**37.如何解决中文乱码问题？**

​	post请求中在charetfilter中设置encoding值，我们可以在web.xml中设置初始化参数

```html
 <init-param>  

​	<param-name>encoding</param-name>

​        <param-value>utf-8</param-value>

<init-param> 

   <init-param>  

​	<param-name>foreencoding</param-name>

​        <param-value>true</param-value>

<init-param> 
```

针对get请求乱码问题最简单的就是修改tomcat的server.xml来修改urlencoding=utf-8

**38.Mybatis中当实体类中的属性名和表中的字段名不一样，怎么办？**

​	解决方案：

​	1.写sql语句时起别名

​	2.在mybatis的全局配置文件开启驼峰命名规则，在mybatis-config。xml中

​	3.在mapper的映射文件中使用resultMap来自定义映射规则

A.单表查询

```xml
<select id="selll" resultMap="userMap">       
 select id u_id,name u_name,age u_age from users
</select>
 <resultMap type="com.zhiyou100.xf.bean.Users" id="userMap">
  <id column="u_id" property="id"/><!--作为唯一标识的映射-->
  <result column="u_name" property="name"/><!--其他普通字段的映射-->
  <result column="u_age" property="age"/><!--property实体类中的属性名，cloumn：表中的字段名-->
</resultMap>
```

B.关联查询 一对一、多对一  实体类中将另一个类作为属性association

一对一：

```xml
<!-方式一：嵌套结果：使用嵌套结果映射来处理重复的联合结果的子集 封装联表查询的数据(去除重复的数据) select * from class c, teacher t where c.teacher_id=t.t_id and c.c_id=1 -->

 <select id="getClass" parameterType="int" resultMap="ClassResultMap">
 select * from class c, teacher t where c.teacher_id=t.t_id and c.c_id=#{id} 
</select> 
<resultMap type="_Classes" id="ClassResultMap">
 <id property="id" column="c_id"/> 
<result property="name" column="c_name"/>
 <association property="teacher" column="teacher_id" javaType="_Teacher">
 <id property="id" column="t_id"/> <result property="name" column="t_name"/> </association> 
</resultMap>
<!-
方式二：嵌套查询：通过执行另外一个 SQL 映射语句来返回预期的复杂类型 SELECT * FROM class WHERE c_id=1; SELECT*FROMteacherWHEREt_id=1 //1 是上一个查询得到的 teacher_id 的值
-->
<select id="getClass2" parameterType="int" resultMap="ClassResultMap2"> 
select * from class where c_id=#{id} 
</select> 
<resultMap type="_Classes" id="ClassResultMap2"> 
<id property="id" column="c_id"/> 
<result property="name" column="c_name"/>
 <association property="teacher" column="teacher_id" javaType="_Teacher" select="getTeacher">
 </association> 
</resultMap>
<select id="getTeacher" parameterType="int" resultType="_Teacher"> 
SELECT t_id id, t_name name FROM teacher WHERE t_id=#{id} 
</select>
```

一对多： 实体类中将另一个类的list作为属性collection 

```xml
<select id="selAll" resultMap="AllMap">
        select * from teacher,student,class where c_id=class_id and teacher_id=t_id and c_id=#{id}
    </select>
    <resultMap type="com.zhiyou100.xf.bean.Classes" id="AllMap">
        <id column="c_id" property="cid"/>
        <result column="c_name" property="cname"/>
        <association property="teacher" javaType="com.zhiyou100.xf.bean.Teacher">
            <id column="t_id" property="tid"/>
            <result column="t_name" property="tname"/>
        </association>
        <collection property="students" ofType="com.zhiyou100.xf.bean.Student">
            <id column="s_id" property="sid"/>
            <result column="s_name" property="sname"/>
        </collection>
    </resultMap>
```

**39.linux系统常用服务类相关命令？**

​	1.service network status 查看网络状态

​	2.chkconfig --list列取服务 用来设置自启动 

​	3.查看进程  ps -ef | grep mysql

**40.Redis持久化**
	rdb 节省空间，恢复快，fork一个子进程数据量大也很慢，满足条件才存储，

​	aof以日志方式，细粒度，增量备份，丢失数据概率低，数据是日志格式，站空间，恢复速度慢有读写存在一定性能压力，存在个别bug

**41.git常用操作**

​	第一次创建用户 git config --global user.name="用户名"     git config --global user.email=“邮箱”  只创建一次就够了

1.git status  查看当前状态 	  2.git add 文件名1 文件名2（可以添加一个或者多个）  添加到缓存区	     3.git .  添加当前目录到缓存区中

提交至版本库：git commit -m “注释内容”

查看版本：git log --pretty=online

回退操作：git reset --hard 提交编号

回到过去后要想在回到当前最新版本时，则需要指令区查看历史操作，已得到最新的commit id 使用指令 git reflog 查看版本号在通过 git reset --hard 版本号回到现在

**42.GitHub上两种常规使用方式**

​	1.基于http协议

​	a.创建空目录，名称就叫shop

​	b.使用clone指令克隆线上仓库到本地 语法：git clone +线上仓库地址 

​	c.在仓库上做对应的操作（提交暂存区，提交本地仓库，提交线上仓库，拉取线上仓库）

​		提交到线上仓库的指令：git push 在首次往线上仓库提交时出现403致命错误，原因是不是谁都能提交的必须鉴权，需要修改“./git/config”文件内容

​	d.拉取线上最新版本 git pull  上班时要经常拉取

​	2.基于ssh协议的

​		该方式与前面的HTTPS方式相比，只是影响GitHub对于用户的身份鉴权的方式，对其他没影响。

生成公私钥对指令（需要自行安装openssh） ssh-keygen-t rsa -C "注册的邮箱"

​	步骤：a.生成客户端公私钥文件  b.将文件上传到GitHub

  	 **分支指令**

​	1.查看分支：git branch

​	2.创建分支：git branch 分支名

​	3.切换分支：git checkout 分支名

​	4.删除分支：git branch -d 分支名

​	5.合并分支：git merge 被合并的分支名

**43.冲突的产生与解决**

​	同事早我下班后修改了线上代码，此时我本地仓库内容与线上不一致，第二天上班后没拉取代码，直接修改了本地仓库的内容，然后下班提交代码产生冲突。

​	解决冲突：当执行git pull时显示已经合并。打开冲突文件，解决冲突。

​	解决方法：需要和同事（谁提交的，看代码如何保留，将改好的再次提交即可）

​	如果都保留包标记删除后提交即可，如果不想保留谁的删除提交即可 

解决乱码问题可在bash窗口下依次执行：

git config  core.quotepath off

git config  --unset i18n.logoutputencoding

git config  --unset i18n.commitencoding

忽略目录：在当前目录下创建一个./gitignore文件夹，在里面写上要忽略提交的文件名称

**44.并发编程与高并发**

​	多个线程操作同一个资源

​	线程的生命周期：1.新建    2.就绪    3.运行     4.阻塞      5.死亡	

**45.常用的设计模式？**

​	1.单例模式   <https://www.cnblogs.com/songyoulian/p/10029785.html>

​	2.工厂模式  <https://www.cnblogs.com/songyoulian/p/10053074.html>

​	3.装饰模式：又叫包装模式，通过对客户端透明的方式来扩展对象的功能，是继承关系的一种替换，符合开闭模式；在不改变原有对象的基础之上，将功能附加到对象上。提供了比继承更有弹性的替代方案（扩展原有对象功能）

使用场景：

1. 扩展一个类的功能或者给一个类添加附加职责
2. 给一个对象动态的添加功能，或动态撤销功能。

**46.有关JVM相关**？

​	![icon](/assert/1582772736336.png)

​	实例变量放在堆内存中；静态变量+常量（private，static，final，string）+类信息+运行时常量存在方法区    **栈管运行  ，堆管存储**  **垃圾回收只发生在堆中**   **jvm优化主要是优化堆**

​	基本类型的变量和对象的引用变量都是在函数的栈内存中分配，栈中不存在垃圾回收问题

 ![icon](/assert/1582772943186.png)

当对象被new时发生在新生区的伊甸园区；

养老区：一般是数据库连接池这种池类对象在这；

永久区：没有垃圾回收用于存放运行环境所必需的的类信息，关闭jvm才释放内存 java7叫做永久代，java8叫做元空间

![icon](/assert/1582774755868.png)

​		![icon](/assert/1582775750485.png)

![icon](/assert/1582776625729.png)

![icon](/assert/1582776717992.png)

永久代就是方法区

![icon](/assert/1582778144272.png)

GC是什么？

​	频繁收集young区（普通GC,用到的算法是复制算法（coping）不会产生内存碎片，就是有点浪费空间）； 较少收集Old区(全局GC，一般是由标记清除或者是标记清除与标记整理的混合实现)； 基本不动perm区

**47.索引的数据结构？**

   数据结构分为：**二叉树**：（key（查找的值）-value（磁盘地址）结构），当数据出现单边增长的时候在用二叉树查找不太合适，	

​     **红黑树** ：如果出现单边增长的话他会自平衡，但是如果存储大数据量的话它的树的高度会很大，导致磁盘IO会很频繁

![icon](/assert/1582882404182.png)   

​      **hash表**  只要走了hash不管你的表的数据有多大，通过hash运算只需要一次磁盘io就能找到数据地址，但是如果是范围查找，hash算法就不行了

​     **b-tree**（mysql底层用的其实是b+tree，应为b-tree不能解决范围查找，虽然解决了红黑树树高的问题）  叶节点具有相同的深度，叶节点的指针为空，节点中的数据索引从左到右递增排列

​     **b+tree**：非叶子节点不存储data，只存储索引，可以放更多的索引，叶子节点不存储指针，顺序访问指针，提高区间访问的性能（树的高度为3时就可存储2千万条数据）

索引的优缺点：

优点：可以快速检索，减少I/O次数，加快检索速度；根据索引分组和排序，可以加快分组和排序；

缺点：索引本身也是表，因此会占用存储空间，一般来说，索引表占用的空间的数据表的1.5倍；索引表的维护和创建需要时间成本，这个成本随着数据量增大而增大；构建索引会降低数据表的修改操作（删除，添加，修改）的效率，因为在修改数据表的同时还需要修改索引表；

**48.存储引擎**

​	存储引擎到表级别常用的Innodb，MYSIAM

​	如果是myisam存储引擎的话在mysql的安装文件目录下的data文件夹下一个实例下边有三个文件分别为：

​        .frm		存储表结构相关的信息

​	.MYD	存储的是表结构中的所有的数据行信息

​	.MYI	存储的是表的索引

如果存储引擎是innodb的话有两个文件：

​	.frm:

​	.ibd:

​	什么是聚集索引？ 叶节点包含了完整的数据记录（把索引元素和数据元素聚集到一起）

​		innodb的主键索引其实就是聚集索引 myisam就是非聚集所引

​	为什么innodb表必须要有主键，并且推荐使用整型的自增所引（应为效率高，节省磁盘空间）？

​	     InnoDB引擎表是基于B+树的索引组织表(IOT)；每个表都需要有一个聚集索引(clustered index) 数据都是由b+tree来维护的，所以要有主键索引

 **InnoDB和MyIsam的区别？**

1.MyIsam默认表类型不是事务安全的，InnoDB是支持事物的

2.MyIsam不支持外键，InnoDB支持外键

3.MyIsam支持表级锁（不支持高并发，以读为主）， innodb支持行锁（共享锁，排它锁，意向锁），粒度更小，但是在执行不能确定扫描范围的sql语句时，innodb同样会锁全表。

4.执行大量select时MyIsam是最佳选择，执行insert，updata最好用innodb

5.myisam在磁盘上存储上有三个文件.frm(存储表定义) .myd（存储表数据） .myi（存储表索引）；innodb磁盘上存储的是表空间数据文件和日志文件，innodb表大小只受限于操作系统大小。

6.myisam使用非聚集索引，索引和数据分开，只缓存索引；innodb使用聚集索引，索引和数据存在一个文件。

7.myisam保存表具体行数；innodb不保存。

 8.delete from table时，innodb不会重新建立表，而会一行一行的删除。  

**49.联合索引的底层存储结构长什么样？**

​	工作中常用，

**50.mysql常用的命令？**

看你的mysql现在已提供什么存储引擎:  show engines;

看你的mysql当前默认的存储引擎:show variables like '%storage_engine%';

   7种表的join：

建表：	

```sql
CREATE TABLE `tbl_dept` (
 `id` INT(11) NOT NULL AUTO_INCREMENT,
 `deptName` VARCHAR(30) DEFAULT NULL,
 `locAdd` VARCHAR(40) DEFAULT NULL,
 PRIMARY KEY (`id`)
) ENGINE=INNODB AUTO_INCREMENT=1 DEFAULT CHARSET=utf8;
 
CREATE TABLE `tbl_emp` (
 `id` INT(11) NOT NULL AUTO_INCREMENT,
 `name` VARCHAR(20) DEFAULT NULL,
 `deptId` INT(11) DEFAULT NULL,
 PRIMARY KEY (`id`),
 KEY `fk_dept_id` (`deptId`)
 #CONSTRAINT `fk_dept_id` FOREIGN KEY (`deptId`) REFERENCES `tbl_dept` (`id`)
) ENGINE=INNODB AUTO_INCREMENT=1 DEFAULT CHARSET=utf8;
 
 
 
INSERT INTO tbl_dept(deptName,locAdd) VALUES('RD',11);
INSERT INTO tbl_dept(deptName,locAdd) VALUES('HR',12);
INSERT INTO tbl_dept(deptName,locAdd) VALUES('MK',13);
INSERT INTO tbl_dept(deptName,locAdd) VALUES('MIS',14);
INSERT INTO tbl_dept(deptName,locAdd) VALUES('FD',15);
 
 
INSERT INTO tbl_emp(NAME,deptId) VALUES('z3',1);
INSERT INTO tbl_emp(NAME,deptId) VALUES('z4',1);
INSERT INTO tbl_emp(NAME,deptId) VALUES('z5',1);
 
INSERT INTO tbl_emp(NAME,deptId) VALUES('w5',2);
INSERT INTO tbl_emp(NAME,deptId) VALUES('w6',2);
 
INSERT INTO tbl_emp(NAME,deptId) VALUES('s7',3);
 
INSERT INTO tbl_emp(NAME,deptId) VALUES('s8',4);
 
INSERT INTO tbl_emp(NAME,deptId) VALUES('s9',51);

```

7种查询：

```sql
1 A、B两表共有
 select * from tbl_emp a inner join tbl_dept b on a.deptId = b.id;
 
2 A、B两表共有+A的独有
 select * from tbl_emp a left join tbl_dept b on a.deptId = b.id;
 
3 A、B两表共有+B的独有
 select * from tbl_emp a right join tbl_dept b on a.deptId = b.id;
 
4 A的独有 
select * from tbl_emp a left join tbl_dept b on a.deptId = b.id where b.id is null; 
 
5 B的独有
 select * from tbl_emp a right join tbl_dept b on a.deptId = b.id where a.deptId is null; #B的独有
 
6 AB全有
#MySQL Full Join的实现 因为MySQL不支持FULL JOIN,下面是替代方法
 #left join + union(可去除重复数据)+ right join
SELECT * FROM tbl_emp A LEFT JOIN tbl_dept B ON A.deptId = B.id
UNION
SELECT * FROM tbl_emp A RIGHT JOIN tbl_dept B ON A.deptId = B.id
 
7 A的独有+B的独有
SELECT * FROM tbl_emp A LEFT JOIN tbl_dept B ON A.deptId = B.id WHERE B.`id` IS NULL
UNION
SELECT * FROM tbl_emp A RIGHT JOIN tbl_dept B ON A.deptId = B.id WHERE A.`deptId` IS NULL;

```

索引的创建删除语句

```sql
有四种方式来添加数据表的索引：
ALTER TABLE tbl_name ADD PRIMARY KEY (column_list): 该语句添加一个主键，这意味着索引值必须是唯一的，且不能为NULL。
 
ALTER TABLE tbl_name ADD UNIQUE index_name (column_list): 这条语句创建索引的值必须是唯一的（除了NULL外，NULL可能会出现多次）。
 
ALTER TABLE tbl_name ADD INDEX index_name (column_list): 添加普通索引，索引值可出现多次。
查看索引：
SHOW INDEX FROM TABLENAME \G
删除索引：
DROP INDEX[INDEXNAME] ON MYTABLE

查看sql详情
Explain + SQL语句
```

sql查询使用的类型：system > const > eq_ref > ref > range > index > all > all 一般能达到range级别最好能到ref级别

**51.权限认证shiro框架**

​	shiro提供了认证 授权  加密和会话管理等功能。

​	shiro是以过滤器的方式对访问规则进行控制，并且内置一系列过滤器 。大致分为认证过滤器和授权过滤器。

​	认证相关的有：anon(不认证也可以访问)  authbasic ，authc（必须认证才可以访问），user。

​	授权相关：perms（指定资源需要哪些权限才可以访问），roles，ssl，rest，port

spring整合shiro

​	spring提供一个简单的过滤器的处理方案，他将集体的操作交给内部filter对象delegate去处理，而这个delegate通过spring的IOC容器获取，这里采用spring的factorybean获取，虽然支配了一个filter，但是他并没有做实际的工作，而是交给spring容器中的为bean的名字的shirofilter类，即shirofactorybean，shiro过滤器工厂bean相当于间接地加载了9个内置过滤器

![icon](/assert/1583033112867.png)

登录认证流程：1.创建令牌（对用户名和密码进行封装）  2.获取subject（主题应用程序与shiro交互的入口部分）    3.执行认证

自定义relam ：真正实现登录校验的人，shiro只是去调用它 。

shiro的三个核心组件：**subject（主题）**    **SecurityManger（安全管理器）**    **Relam(数据源)**。

**52.springsecurity？**

​	spring security 的核心功能主要包括：认证 （你是谁） 授权 （你能干什么） 	攻击防护 （防止伪造身份）

​	其核心就是一组过滤器链，项目启动后将会自动配置。最核心的就是 Basic Authentication Filter 用来认证用户的身份，一个在spring security中一种过滤器处理一种认证方式。

SecurityContextHolder，SecurityContext，Authentication是Spring Security的基础对象。

​	1. SecurityContextHolder：存储当前的SecurityContext，即认证用户的上下文信息，内部使用ThreadLocal。

​	2. SecurityContext：持有Authentication对象和其他可能需要的信息

​	3. UserDetails：从Authentication中获取的对象，代表当前用户的具体信息

UserDetailsService：获取UserDetails的逻辑，一般封装了查询用户的逻辑，内部只有一个方法：

 UserDetails loadUserByUsername(String username) throws UsernameNotFoundException;

​	4.GrantedAuthority：当前用户获取到的授权信息。

案例：配置SpringSecurity的安全信息

```java
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    // @formatter:off
    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
                .authorizeRequests()
                    .antMatchers("/css/**", "/index").permitAll()
                    
                    // 只有USER权限的角色才能访问/user/接口
                    .antMatchers("/user/**").hasRole("USER")
                    .and()
                .formLogin().loginPage("/login").failureUrl("/login-error");
    }

//  @Autowired
//  public void configureGlobal(AuthenticationManagerBuilder auth) throws Exception {
//      auth
//          .inMemoryAuthentication()
//              .withUser(User.withDefaultPasswordEncoder().username("user").password("password").roles("USER"));
//  }
    // @formatter:on

    // 密码明文
    @Bean
    public PasswordEncoder passwordEncoder() {
        PasswordEncoder encoder = NoOpPasswordEncoder.getInstance();
        return encoder;
    }


  // 获取用户的来源
    @Bean
    public UserDetailsService userDetailsService(){
        UserDetailsService userDetailsService = new UserDetailsService(){

            @Override
            public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {
                if (StringUtils.isEmpty(username) || !"admin".equalsIgnoreCase(username)){
                    return null;
                }

                HashSet<GrantedAuthority> hashSet = new HashSet<>();
                // 内部检验权限，要以ROLE为前缀
                hashSet.add(new  SimpleGrantedAuthority("ROLE_USER") );
                User user = new User("admin","test",hashSet);

                return user;
            }
        };
        return userDetailsService;
    }
}
```

 **53.存储过程与存储函数区别？**

​	（1）存储函数的限制比较多,例如不能用临时表,只能用表变量,而存储过程的限制较少，存储过程的实现功能要复杂些,而函数的实现功能针对性比较强。

　　（2）返回值不同。存储函数必须有返回值,且仅返回一个结果值；存储过程可以没有返回值,但是能返回结果集(out,inout)。

　　（3）调用时的不同。存储函数嵌入在SQL中使用,可以在select 存储函数名(变量值)；存储过程通过call语句调用 call 存储过程名。

　　（4）参数的不同。存储函数的参数类型类似于IN参数，没有类似于OUT和INOUT的参数。存储过程的参数类型有三种，IN、out和INOUT：

　　　　a. in：数据只是从外部传入内部使用(值传递),可以是数值也可以是变量

　　　　b. out：只允许过程内部使用(不用外部数据),给外部使用的(引用传递:外部的数据会被先清空才会进入到内部),只能是变量

　　　　c. inout：外部可以在内部使用,内部修改的也可以给外部使用,典型的引用 传递,只能传递变量。

**a.存储过程：**

​	

```sql
CREATE [OR REPLACE] PROCEDURE procedure_name[(parameter_name in|out|in out parameter_type, [, ...])]
{IS | AS}
  [columnName1 tableName.columnName1%type;
   columnName2 tableName.columnName2%type;
   ...
  ]
BEGIN
  < procedure_body >
END;
 
-- 语法说明：
-- ① 用[]包含的内容为可有可无，根据实际情况而定；
-- ② procedure_name：存储过程名称；
-- ③ parameter_name：参数名称；
-- ④ 参数模式：
--   in: 是参数的默认模式，这种模式就是在程序运行的时候已经具有值，在程序体中值不会改变；即，可以传入参数；
--   out：该模式定义的参数只能在过程体内部赋值，标识该参数可以将某个值传递回调用它的过程；即，可以返回值；
--   in out：表示该参数可以向过程中传递值，也可以将某个值传出去；即，既可以传入参数，也可以返回值；
-- ⑤ parameter_type：参数数据类型；
-- ⑥ is、as：在存储过程中，两者没有任何区别；但是在视图中只能用as，在游标中只能用is；
-- ⑦ procedure_body：PL/SQL子程序体；即该存储过程要执行的操作内容；
-- ⑧ 创建存储过程时，可以在is或者as后面添加对类型或变量的说明；

```

实例：创建添加员工信息的存储过程：

```sql
create or replace procedure addEmployee(eNo in out number, uName in out varchar2, dNo in out number, sal in out number, com in out number)
as
  empNo emp.empNo%type;
  usernName emp.username%type;
  deptNo emp.deptno%type;
  salary emp.salary%type;
  comm emp.comm%type;
begin
  insert into emp(empNo, username, deptNo, salary, comm)values(eNo, uName, dNo, sal, com);
end;
```

  PL/SQL调用存储过程：

```sql
declare
  empNo emp.empno%type := 7777;
  username emp.username%type := 'Hellen';
  deptNo emp.deptno%type := 10;
  salary emp.salary%type := 3800;
  comm emp.comm%type := 700;
begin
  addEmployee(empNo, username, deptno, salary, comm);
end;
```

**b.存储函数：**

创建语法：

```sql
CREATE [OR REPLACE] FUNCTION function_name[(parameter_name in parameter_type, [, ...])]
    RETURN returnValType
{IS | AS}
  [variable1 type;
   variable2 type;
   ...
  ]
BEGIN
  < procedure_body >
END;
 
-- 语法说明：
-- ① 用[]包含的内容为可有可无，根据实际情况而定；
-- ② function_name：存储函数名称；
-- ③ parameter_name：参数名称；
-- ④ in: 参数模式，存储函数只有in模式；
-- ⑤ parameter_type：参数数据类型；
-- ⑥ returnValType：函数返回值数据类型；
-- ⑦ is、as：在存储过程中，两者没有任何区别；但是在视图中只能用as，在游标中只能用is；
-- ⑧ variable、type：分别用于声明函数在执行过程中所需要的变量名称和数据类型； 
-- ⑨ procedure_body：PL/SQL子程序体；即该存储函数要执行的操作内容；
-- ⑩ 创建存储过程时，可以在is或者as后面添加对类型或变量的说明；
```

 实例：创建为员工加薪的存储函数

```sql
create or replace FUNCTION addSalary(eNo in number, addVal in number)
  RETURN number
AS
  pNo number;         -- 定义变量保存员工编号
  pName varchar2(30); -- 定义变量保存员工用户名
  pDeptNo number;     -- 定义变量保存员工部门编号
  pSal number;        -- 定义变量保存员工的工资
  pComm number;       -- 定义变量保存员工的奖金
  pTotal number;      -- 定义变量保存员工的总收入
  newSalary number;   -- 定义变量保存加薪后的工资
  newComm number;     -- 定义变量保存加薪后的奖金
BEGIN
  SELECT empNo, username, deptNo, salary, comm INTO pNo, pName, pDeptNo, pSal, pComm FROM EMP WHERE empNo=eNo;
  pTotal := (pSal+pComm)*12;
  DBMS_OUTPUT.PUT_LINE('员工'||pName||'：初始工资为='||pSal||'；初始奖金为='||pComm||'；初始年薪为='||pTotal);
 
  newSalary := pSal+pSal*addVal;
  newComm := newSalary*0.12;
  UPDATE EMP SET username=pName, deptNo=pDeptNo, salary=newSalary, comm=newComm WHERE empNo=pNo;
  RETURN newSalary;
END;
```

 PL/SQL调用存储函数，为编号为"2222"的员工加薪30%：

```sql
declare
  a number;        -- 定义变量，接受存储函数返回值
begin
  a := addSalary(1111, 0.3);    -- 调用存储函数
  DBMS_OUTPUT.put_line(a);      -- 打印存储函数返回值
end;
```

**54.Docker相关**

**docker镜像**：Docker镜像是由文件系统叠加而成（是一种文件的存储形式）。最底端是一个文件引导系统，即bootfs，这很像典型的Linux/Unix的引导文件系统。

一些常用命令：

列出docker下的所有镜像：docker images

 搜索镜像： docker search 镜像名称

 拉取镜像：docker pull centos:7   

  删除镜像： docker rmi $IMAGE_ID：删除指定镜像

 docker rmi `docker images -q`：删除所有镜像

**docker容器操作：** 

看正在运行容器：docker ps

查看停止的容：docker ps -f status=exited

创建容器命令：docker run

  -i：表示运行容器

  -t：表示容器启动后会进入其命令行。加入这两个参数后，容器创建就能登录进去。即分配一个伪终端。

 --name :为创建的容器命名。

-v：表示目录映射关系（前者是宿主机目录，后者是映射到宿主机上的目录），可以使用多个－v做多个目录或文件映射。注意：最好做目录映射，在宿主机上做修改，然后共享到容器上。

  -d：在run后面加上-d参数,则会创建一个守护式容器在后台运行（这样创建容器后不会自动登录容器，如果只加-i -t两个参数，创建后就会自动进去容器）。

  -p：表示端口映射，前者是宿主机端口，后者是容器内的映射端口。可以使用多个－p做多个端口映射

实例：创建一个交互式容器并取名为mycentos

docker run -it --name=mycentos centos:7 /bin/bash

创建一个守护式容器：如果对于一个需要长期运行的容器来说，我们可以创建一个守护式容器。

docker run -di  --name=mycentos2 centos:7

登录守护式容器方式：docker exec -it container_name (或者container_id)  /bin/bash（exit退出时，容器不会停止）

停止正在运行的容器：docker stop 容器名/id.

启动已运行过的容器：docker start $CONTAINER_NAME/ID

**a.**文件拷贝：如果我们需要将文件拷贝到容器内可以使用cp命令:   docker cp 需要拷贝的文件或目录 容器名称:容器目录

也可以将文件从容器内拷贝出来: docker cp 容器名称:容器目录 需要拷贝的文件或目录

**b.**目录挂载：

创建容器 添加-v参数 后边为   宿主机目录:容器目录

docker run -di -v  /usr/local/myhtml:/usr/local/myhtml --name=mycentos2 centos:7  挂载多级目录时我们需要添加参数  --privileged=true

查看容器地址：docker inspect mycentos

删除容器：l  docker rm $CONTAINER_ID/NAME

**c.**迁移与备份：

​	容器保存为镜像：docker commit pinyougou_nginx（容器名字） mynginx（新的镜像名字）

此镜像的内容就是你当前容器的内容，接下来你可以用此镜像再次运行新的容器。

​	镜像备份：docker  save -o mynginx.tar mynginx        -o 输出到的文件

​	镜像恢复与迁移：docker load -i mynginx.tar    -i 输入的文件

容器和镜像可以互相转换。

**55.vue.js相关**  https://cn.vue.js.org

​	vue.js的核心是一个允许采用简洁的模板语法来声明式地将数据渲染进dom的系统：

1.模板语法：

​	（1）插值

​		a.文本{{}}   b.如果想渲染纯HTML标签内容用指令v-html  防止一些攻击。

​	v-show=“属性” 控制节点是否显示   在dom中还存在

​	v-if=“属性”   如果为true 就创建节点，否则就删除节点（dom中就没了）

​	v-for=“（data,index或key） in或of datalist” 循环遍历即可拿到key值和索引值

​	![icon](/assert/1.png)

过滤方法(filter)：     indexof方法：“abc”.indexof("a") 判断a是否在“abc”中，在的话返回0，否则返回-1

```html
var arr=[1,2,3,4,5]
var newlist=arr.filter(item=>{
	return item>3
})
```

事件修饰符  阻止事件冒泡：@click.stop   @click.prevent="具体方法"  阻止默认事件

双向绑定事件：v-model.lazy 指令当失去焦点时触发，节省资源  v-model.number只绑定数字

 v-model.trim 去除空格

**vue组件**：

1.axios与fetch实现数据请求

fetch:	fetch("url").then(res=>res.json()).then(res=>consle.log(res));

axios:    axios.get().then(res=>{console.log(res.data(自动包装data属性))}).catch(err=>{console.log(err)})

2.计算属性

计算属性其实是在一个computed下定义的方法函数，使用时像一个属性一样去使用,计算属性性能高，它能缓存

![icon](/assert/2.png)

3.虚拟dom与diff算法key的作用

​	虚拟dom能提高性能，因为它能够最大程度得保证组件，节点的可复用性，减少对dom的频繁操作

4.组件化开发：

定义全局组件：vue.component("组件名"，{template:}),可以在任何地方使用。

定义局部组件：components:{组件名:{tempalte:}}   在谁的内部定义谁能使用。

5.组件编写方式与vue实例的区别？

​	自定义组件需要有一个root element ；父组件的data是无法共享的；组件可以有data，methods，computed...但是data必须是一个函数

![icon](/assert/3.png)

6.父组件传子组件（属性向下传）

​	props:["父组件中传递过来的属性名"]   接收父组件传来的属性

![icon](/assert/4.png)

动态的绑定属性  在属性前面加":"来实现动态绑定，否则会把属性当成普通字符串来对待

属性验证![icon](/assert/5.png) 如果值是动态的加冒号来动态绑定

7.子传父组件间的通讯

​	在子组件中使用$emit()来触发父组件中的回调函数，即触发父组件中的方法执行

![icon](/assert/6.png)

$event用来接收参数

8.ref的使用

​	ref放在标签上拿到的是原生节点；  ref放到组件上拿到的是组件对象



![icon](/assert/7.png)

9.组件通信

![icon](/assert/8.png)

10.动态组件

<component> 元素，vue内置的组件动态的绑定多个组件到它的is属性 <keep-alive> 保留状态，避免重新渲染

![icon](/assert/10.png)

11.slot插槽（内容分发）具名插槽：具有名字的插槽，更精细的控制插入内容

![icon](/assert/11.png)

![icon](/assert/12.png)

使用插槽将父组件的内容混到了子组件中

![icon](/assert/13.png)

12.vue-router

​	a.创建`components目录下存放我们自己编写的组件

​	b.定义一个Content.vue 的组件

```html
<template>
  <div>
 <h1>内容页</h1>
  </div>
</template>

<script>
 export default {
     name: "Content"
 }
</script>
```

​	c. 安装路由,在src目录下,新建一个文件夹 : router,专门存放路由

```html
import Vue from 'vue'
// 导入路由插件
import Router from 'vue-router'
// 导入上面定义的组件
import Content from '../components/Content'
import main from '../components/main'
// 安装路由
Vue.use(Router);
// 配置路由
export default new Router({
  routes: [
    {
      // 路由路径
      path: '/content',
      // 路由名称
      name: 'Content',
      // 跳转到组件
      component: Content
    }, {
      // 路由路径
      path: '/main',
      // 路由名称
      name: 'main',
      // 跳转到组件
      component: main
    }
  ]
});
```

d.在`main.js` 中配置路由

```html
import Vue from 'vue'
import App from './App'

// 导入上面创建的路由配置目录
import router from './router'

//来关闭生产模式下给出的提示
Vue.config.productionTip = false;

new Vue({
  el: '#app',
  // 配置路由
  router,
  components: { App },
  template: '<App/>'
});
```

e.在`App.vue`中使用路由

```html
<template>
  <div id="app">
    <!--
      router-link： 默认会被渲染成一个 <a> 标签，to 属性为指定链接
      router-view： 用于渲染路由匹配到的组件
    -->
    <router-link to="/">首页</router-link>
    <router-link to="/content">内容</router-link>
    <router-view></router-view>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>
```

13.参数传递及接收

​	a.前端传参数

![icon](/assert/15.png)

​	b.路由中接收

![icon](/assert/16.png)

​	c.组件中展示(展示时要用标签包裹)

![icon](/assert/17.png)

方式2：通过pops解耦

​	a.前端传参数不用改变

​	b.路由中接收(允许使用pops接收)

![icon](/assert/18.png)

​	c.组件中展示

![icon](/assert/19.png)

重定向：![icon](/assert/20.png)

写完组件后要先把它配到路由中 import 组件名 from ' ' 在配置路由

14，钩子函数

![icon](/assert/21.png)

- to：路由将要跳转的路径信息
- from：路径跳转前的路径信息
- next：路由的控制参数 

15.js相关（可参考`<https://www.cnblogs.com/weigaojie/p/10491085.html>`）

`let ` ： let命令，用来声明变量。它的用法类似于var，但是所声明的变量，只在`let命令所在的代码块`内有效  适用于for循环;先声明，在使用;不允许在相同作用域内重复声明同一个变量;let可以识别块级作用域

`const`:声明一个只读的常量。一旦声明，常量的值就不能改变。

声明常量的同时进行赋值，不赋值就会报错

可以识别块级作用域

不能重复声明

不存在变量提升【先访问在声明】

`数据类型`：根据在内存中的存储位置划分。基本数据类型存放在栈中，引用数据类型存放在堆中（指针存放在栈中，内容存放在堆中 ）

`基本数据类型`：undefined；null 【空占位符】；string 【也是对象】

`string中对象的方法`：

​	let 对象=new String（“  ”）；

​	对象.charCodeAt(2)  返回第2个位置的字符编码

​	查找元素    对象.charAt(0) 字符串的第0个位置的元素【查找字符】

​	查找下标     对象.indexOf（“ ”）   查找对应字符的下标，如果有返回下标，如果没有，返  回-1【第一 个字符开始的下标】

​	对象.lastIndexOf（“”） 倒着看查找，倒序看如果有返回下标，如果没有，返回-1【第一个字符开始的下标】

​	对象.lastIndexOf（“”） 倒着看查找，倒序看如果有返回下标，如果没有，返回-1【第一个字符开始的下标】

​	对象.match（“”）  有的话，返回数组【返回值，下标，包含返回值的数组】没有  返回null

​	字符串的截取：【返回新值，不改变原内容】

​	对象.substr（开始下标，【截取的长度】）

​	对象.substring（开始下标，结束的下标），从开始下标开始到结束下标之前，不取到结束的下标

​	对象.slice（开始下标，结束的下标），从开始下标开始到结束下标之前，不取到结束的下标【数组的方法】

​	字符串大小写【转换】let str="AbCdEf";str.toLowerCase() 

​	转换为小写str.toUpperCase() 转换为大写

​	替换：str.replace（“山”，“闪”）；

​	转换【字符串转换数组】let str=“1,2,3,4,5,6”；arr2=str.split（“，”）；

`引用数据类型`

​	object（属性与方法的集合）数组，函数，对象

​	深拷贝：let arr=【1,2,3,4】

​			let  arr1；

​			arr1=arr； ：传址

​			arr1 和 arr具有相同地址

​	浅拷贝：let arr=【1,2,3,4】；

​			let arr1=【】；

​			arr.foreach(function（value）{    arr1.push（value）})

​	三元运算符：表达式 ? 为真的执行语句：为假的执行语句

ajax请求：

​	ajax({                              

​		  url:'/',    必须有    

​		type:'get',    可有可无    

​		dataType:'text',     可有可无   

​		 data:{name:"zhangsan"},     可有可无   

​		 success:function(data){         可有可无       

​	         upDate(data)            },})

![icon](/assert/22.png)



**56.vue的优缺点**

a.优点：

双向数据绑定  

 	通过MVVM思想实现数据的双向绑定，让开发者不用再操作dom对象，有更多的时间去思考业务逻辑。

组件化开发

​	我们可以像编程一样把模块封装 这就引入了组件化开发的思想。

虚拟dom

​	这个DOM操作属于预处理操作，并没有真实的操作DOM，所以叫做虚拟DOM。最后在计算完毕才真正将DOM操作提交，将DOM操作变化反映到DOM树上。

**57.spring面试相关**

**1.什么是spring？**

​	 Spring 框架指的都是 Spring Framework，它是很多模块的集合，这些模块是：核心容器、数据访问/集成,、Web、AOP（面向切面编程）、工具、消息和测试模块。比如：Core Container 中的 Core 组件是Spring 所有组件的核心，Beans 组件和 Context 组件是实现IOC和依赖注入的基础，AOP组件用来实现面向切面编程。

**2.列举一些重要的spring模块？**

![icon](/assert/23.png)

Spring Core： 基础,可以说 Spring 其他所有的功能都需要依赖于该类库。主要提供 IOC 依赖注入功能。
Spring Aspects： 该模块为与AspectJ的集成提供支持。
Spring AOP ：提供了面向方面的编程实现。
Spring JDBC : Java数据库连接。
Spring JMS ：Java消息服务。
Spring ORM : 用于支持Hibernate等ORM工具。
Spring Web : 为创建Web应用程序提供支持。
Spring Test : 提供了对 JUnit 和 TestNG 测试的支持。

**3.谈谈自己对于springIOC和AOP的理解？**

​	IoC（Inverse of Control:控制反转）是一种设计思想，就是 将原本在程序中手动创建对象的控制权，交由Spring框架来管理。 IoC 在其他语言中也有应用，并非 Spirng 特有。 IoC 容器是 Spring 用来实现 IoC 的载体， IoC 容器实际上就是个Map（key，value）,Map 中存放的是各种对象。

将对象之间的相互依赖关系交给 IOC 容器来管理，并由 IOC 容器完成对象的注入。这样可以很大程度上简化应用的开发，把应用从复杂的依赖关系中解放出来。 IOC 容器就像是一个工厂一样，当我们需要创建一个对象的时候，只需要配置好配置文件/注解即可，完全不用考虑对象是如何被创建出来的。 在实际项目中一个 Service 类可能有几百甚至上千个类作为它的底层，假如我们需要实例化这个 Service，你可能要每次都要搞清这个 Service 所有底层类的构造函数，这可能会把人逼疯。如果利用 IOC 的话，你只需要配置好，然后在需要的地方引用就行了，这大大增加了项目的可维护性且降低了开发难度。Spring的IOC有三种注入方式 ：构造器注入、setter方法注入、根据注解注入。

**4.springAOP理解？**

​	OOP面向对象，允许开发者定义纵向的关系，但并适用于定义横向的关系，导致了大量代码的重复，而不利于各个模块的重用。

AOP，一般称为面向切面，作为面向对象的一种补充，用于将那些与业务无关，但却对多个对象产生影响的公共行为和逻辑，抽取并封装为一个可重用的模块，这个模块被命名为“切面”（Aspect），减少系统中的重复代码，降低了模块间的耦合度，同时提高了系统的可维护性。可用于权限认证、日志、事务处理。

​	AOP实现的关键在于 代理模式，AOP代理主要分为静态代理和动态代理。静态代理的代表为AspectJ；动态代理则以Spring AOP为代表。

（1）AspectJ是静态代理的增强，所谓静态代理，就是AOP框架会在编译阶段生成AOP代理类，因此也称为编译时增强，他会在编译阶段将AspectJ(切面)织入到Java字节码中，运行的时候就是增强之后的AOP对象。

（2）Spring AOP使用的动态代理，所谓的动态代理就是说AOP框架不会去修改字节码，而是每次运行时在内存中临时为方法生成一个AOP对象，这个AOP对象包含了目标对象的全部方法，并且在特定的切点做了增强处理，并回调原对象的方法。

**Spring AOP中的动态代理主要有两种方式，JDK动态代理和CGLIB动态代理：**

​        ①JDK动态代理只提供接口的代理，不支持类的代理。核心InvocationHandler接口和Proxy类，InvocationHandler 通过invoke()方法反射来调用目标类中的代码，动态地将横切逻辑和业务编织在一起；接着，Proxy利用 InvocationHandler动态创建一个符合某一接口的的实例,  生成目标类的代理对象。

        ②如果**代理类没有实现 InvocationHandler 接口**，那么Spring AOP会选择使用CGLIB来动态代理目标类。CGLIB（Code Generation Library），是一个代码生成的类库，可以在运行时动态的生成指定类的一个子类对象，并覆盖其中特定方法并添加增强代码，从而实现AOP。CGLIB是通过继承的方式做的动态代理，因此如果某个类被标记为final，那么它是无法使用CGLIB做动态代理的。

（3）静态代理与动态代理区别在于生成AOP代理对象的时机不同，相对来说AspectJ的静态代理方式具有更好的性能，但是AspectJ需要特定的编译器进行处理，而Spring AOP则无需特定的编译器处理。
**JDK动态代理实例（被代理类要有接口）：**

```java
//首先被代理的类需要实现一个接口
public interface ProxyInterface {
    public void say(String str);
}

//然后写一个实现类   也就是需要被代理的类
public class ProxyImpl implements ProxyInterface {
    @Override
    public void say(String str) {
        System.out.println("ProxyImpl.say is " +str);
    }
}

//然后写代理类
public class ProxyClass implements InvocationHandler {
    Object o;
    public void setTarget(Object o){
        this.o = o;
    }
    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        System.out.println("在调用方法之前执行的方法");   
        method.invoke(o,args);
        System.out.println("在调用方法之后执行的操作");
        return null;
    }
}

//调用
//    jdk动态代理
    public static void main(String[] args) {
        ProxyInterface proxyInterface = new ProxyImpl();
        ProxyClass proxyClass = new ProxyClass();
        proxyClass.setTarget(proxyInterface);
	//传递被代理类的类加载器 接口  代理类  返回被代理类
        ProxyInterface proxy = (ProxyInterface)Proxy.newProxyInstance(proxyInterface.getClass().getClassLoader(),proxyInterface.getClass().getInterfaces(),proxyClass);
        System.out.println("------------------------------------------");
        proxy.say("hello");

        System.out.println(proxy.getClass().getName());
        System.out.println(proxyInterface.getClass().getName());
    }

```

**CGLIB动态代理实例（被代理类不需要要有接口）：**

```java
cglib动态代理的实现，原理
 
//被代理类 注意相对于jdk动态代理 cglib不需要一个公共接口-
package com.xyd.cglib;

public class CglibService {

    public  void  say(){
        System.out.println("我是被代理的方法 也叫做委托类");
    }
}

//实现cglib的接口MethodInterceptor

package com.xyd.cglib;

import net.sf.cglib.proxy.Enhancer;
import net.sf.cglib.proxy.MethodInterceptor;
import net.sf.cglib.proxy.MethodProxy;

import java.lang.reflect.Method;

public class CglibProxy implements MethodInterceptor {

    Object o;

    public Object getInstance(Object targer){
        this.o = targer;
        //cglib的核心原理 不需要接口，而是继承委托类
        Enhancer enhancer = new Enhancer();
        //产生目标类的子类
        enhancer.setSuperclass(this.o.getClass());
        //设置回调方法是MethodInterceptor的实现类
        enhancer.setCallback(this);
        //实例化我们构建的子类
        return enhancer.create();
    }
    public Object intercept(Object obj, 
    		Method method, 
    		Object[] args, MethodProxy proxy) throws Throwable {
        System.out.println("访问控制系统 启动···");
        proxy.invokeSuper(obj,args);
        System.out.println("你可真能闹儿");
        return null;
    }
}


//调用代码
package com.xyd.cglib;

public class MainCglib {
    public static void main(String[] args) {
        CglibService cglibService = new CglibService();
        CglibProxy cglibProxy = new CglibProxy();
        CglibService cglibSay = 
        (CglibService)cglibProxy.getInstance(cglibService);
        cglibSay.say();
    }
}
```

**5.BeanFactory和ApplicationContext有什么区别？**

​	BeanFactory和ApplicationContext是Spring的两大核心接口，都可以当做Spring的容器。其中ApplicationContext是BeanFactory的子接口。

（1）BeanFactory：是Spring里面最底层的接口，包含了各种Bean的定义，读取bean配置文档，管理bean的加载、实例化，控制bean的生命周期，维护bean之间的依赖关系。ApplicationContext接口作为BeanFactory的派生，除了提供BeanFactory所具有的功能外，还提供了更完整的框架功能：

①继承MessageSource，因此支持国际化。

②统一的资源文件访问方式。

③提供在监听器中注册bean的事件。

④同时加载多个配置文件。

⑤载入多个（有继承关系）上下文 ，使得每一个上下文都专注于一个特定的层次，比如应用的web层。

（2）①BeanFactroy采用的是延迟加载形式来注入Bean的，即只有在使用到某个Bean时(调用getBean())，才对该Bean进行加载实例化。这样，我们就不能发现一些存在的Spring的配置问题。如果Bean的某一个属性没有注入，BeanFacotry加载后，直至第一次使用调用getBean方法才会抛出异常。

        ②ApplicationContext，它是在容器启动时，一次性创建了所有的Bean。这样，在容器启动时，我们就可以发现Spring中存在的配置错误，这样有利于检查所依赖属性是否注入。 ApplicationContext启动后预载入所有的单实例Bean，通过预载入单实例bean ,确保当你需要的时候，你就不用等待，因为它们已经创建好了。

        ③相对于基本的BeanFactory，ApplicationContext 唯一的不足是占用内存空间。当应用程序配置Bean较多时，程序启动较慢。

（3）BeanFactory通常以编程的方式被创建，ApplicationContext还能以声明的方式创建，如使用ContextLoader。

（4）BeanFactory和ApplicationContext都支持BeanPostProcessor、BeanFactoryPostProcessor的使用，但两者之间的区别是：BeanFactory需要手动注册，而ApplicationContext则是自动注册

**6、请解释Spring Bean的生命周期？**

Servlet的生命周期：实例化，初始init，接收请求service，销毁destroy；

Spring上下文中的Bean生命周期也类似，如下：

（1）实例化Bean：

对于BeanFactory容器，当客户向容器请求一个尚未初始化的bean时，或初始化bean的时候需要注入另一个尚未初始化的依赖时，容器就会调用createBean进行实例化。对于ApplicationContext容器，当容器启动结束后，通过获取BeanDefinition对象中的信息，实例化所有的bean。

（2）设置对象属性（依赖注入）：

实例化后的对象被封装在BeanWrapper对象中，紧接着，Spring根据BeanDefinition中的信息 以及 通过BeanWrapper提供的设置属性的接口完成依赖注入。

（3）处理Aware接口：

接着，Spring会检测该对象是否实现了xxxAware接口，并将相关的xxxAware实例注入给Bean：

①如果这个Bean已经实现了BeanNameAware接口，会调用它实现的setBeanName(String beanId)方法，此处传递的就是Spring配置文件中Bean的id值；

②如果这个Bean已经实现了BeanFactoryAware接口，会调用它实现的setBeanFactory()方法，传递的是Spring工厂自身。

③如果这个Bean已经实现了ApplicationContextAware接口，会调用setApplicationContext(ApplicationContext)方法，传入Spring上下文；

（4）BeanPostProcessor：

如果想对Bean进行一些自定义的处理，那么可以让Bean实现了BeanPostProcessor接口，那将会调用postProcessBeforeInitialization(Object obj, String s)方法。

（5）InitializingBean 与 init-method：

如果Bean在Spring配置文件中配置了 init-method 属性，则会自动调用其配置的初始化方法。

（6）如果这个Bean实现了BeanPostProcessor接口，将会调用postProcessAfterInitialization(Object obj, String s)方法；由于这个方法是在Bean初始化结束时调用的，所以可以被应用于内存或缓存技术；

以上几个步骤完成后，Bean就已经被正确创建了，之后就可以使用这个Bean了。

（7）DisposableBean：

当Bean不再需要时，会经过清理阶段，如果Bean实现了DisposableBean这个接口，会调用其实现的destroy()方法；

（8）destroy-method：

最后，如果这个Bean的Spring配置中配置了destroy-method属性，会自动调用其配置的销毁方法。

**7、 解释Spring支持的几种bean的作用域？**

Spring容器中的bean可以分为5个范围：

（1）singleton：默认，每个容器中只有一个bean的实例，单例的模式由BeanFactory自身来维护。

（2）prototype：为每一个bean请求提供一个实例。

（3）request：为每一个网络请求创建一个实例，在请求完成以后，bean会失效并被垃圾回收器回收。

（4）session：与request范围类似，确保每个session中有一个bean的实例，在session过期后，bean会随之失效。

（5）global-session：全局作用域，global-session和Portlet应用相关。当你的应用部署在Portlet容器中工作时，它包含很多portlet。如果你想要声明让所有的portlet共用全局的存储变量的话，那么这全局变量需要存储在global-session中。全局作用域与Servlet中的session作用域效果相同。

**8、Spring框架中的单例Beans是线程安全的么？**

​	Spring框架并没有对单例bean进行任何多线程的封装处理。关于单例bean的线程安全和并发问题需要开发者自行去搞定。但实际上，大部分的Spring bean并没有可变的状态(比如Serview类和DAO类)，所以在某种程度上说Spring的单例bean是线程安全的。如果你的bean有多种状态的话（比如 View Model 对象），就需要自行保证线程安全。最浅显的解决办法就是将多态bean的作用域由“singleton”变更为“prototype”。

**9、Spring如何处理线程并发问题？**

​	在一般情况下，只有无状态的Bean才可以在多线程环境下共享，在Spring中，绝大部分Bean都可以声明为singleton作用域，因为Spring对一些Bean中非线程安全状态采用ThreadLocal进行处理，解决线程安全问题。

​	ThreadLocal和线程同步机制都是为了解决多线程中相同变量的访问冲突问题。同步机制采用了“时间换空间”的方式，仅提供一份变量，不同的线程在访问前需要获取锁，没获得锁的线程则需要排队。而ThreadLocal采用了“空间换时间”的方式。

​	ThreadLocal会为每一个线程提供一个独立的变量副本，从而隔离了多个线程对数据的访问冲突。因为每一个线程都拥有自己的变量副本，从而也就没有必要对该变量进行同步了。ThreadLocal提供了线程安全的共享对象，在编写多线程代码时，可以把不安全的变量封装进ThreadLocal。

**10-1、Spring基于xml注入bean的几种方式：**

（1）Set方法注入；

（2）构造器注入：①通过index设置参数的位置；②通过type设置参数类型；

（3）静态工厂注入；

（4）实例工厂；

**10-2、Spring的自动装配：**

在spring中，对象无需自己查找或创建与其关联的其他对象，由容器负责把需要相互协作的对象引用赋予各个对象，使用autowire来配置自动装载模式。

在Spring框架xml配置中共有5种自动装配：

（1）no：默认的方式是不进行自动装配的，通过手工设置ref属性来进行装配bean。

（2）byName：通过bean的名称进行自动装配，如果一个bean的 property 与另一bean 的name 相同，就进行自动装配。 

（3）byType：通过参数的数据类型进行自动装配。

（4）constructor：利用构造函数进行装配，并且构造函数的参数通过byType进行装配。

（5）autodetect：自动探测，如果有构造方法，通过 construct的方式自动装配，否则使用 byType的方式自动装配。

@Autowired可用于：构造函数、成员变量、Setter方法

注：@Autowired和@Resource之间的区别

(1) @Autowired默认是按照类型装配注入的，默认情况下它要求依赖对象必须存在（可以设置它required属性为false）。

(2) @Resource默认是按照名称来装配注入的，只有当找不到与名称匹配的bean才会按照类型来装配注入。

**11、Spring 框架中都用到了哪些设计模式？**

（1）工厂模式：BeanFactory就是简单工厂模式的体现，用来创建对象的实例；

（2）单例模式：Bean默认为单例模式。

（3）代理模式：Spring的AOP功能用到了JDK的动态代理和CGLIB字节码生成技术；

（4）模板方法：用来解决代码重复的问题。比如. RestTemplate, JmsTemplate, JpaTemplate。

（5）观察者模式：定义对象键一种一对多的依赖关系，当一个对象的状态发生改变时，所有依赖于它的对象都会得到通知被制动更新，如Spring中listener的实现--ApplicationListener。

**12、Spring事务的实现方式和实现原理：**

Spring事务的本质其实就是数据库对事务的支持，没有数据库的事务支持，spring是无法提供事务功能的。真正的数据库层的事务提交和回滚是通过binlog或者redo log实现的。

（1）Spring事务的种类：

spring支持编程式事务管理和声明式事务管理两种方式：

①编程式事务管理使用TransactionTemplate。

②声明式事务管理建立在AOP之上的。其本质是通过AOP功能，对方法前后进行拦截，将事务处理的功能编织到拦截的方法中，也就是在目标方法开始之前加入一个事务，在执行完目标方法之后根据执行情况提交或者回滚事务。

声明式事务最大的优点就是不需要在业务逻辑代码中掺杂事务管理的代码，只需在配置文件中做相关的事务规则声明或通过@Transactional注解的方式，便可以将事务规则应用到业务逻辑中。

声明式事务管理要优于编程式事务管理，这正是spring倡导的非侵入式的开发方式，使业务代码不受污染，只要加上注解就可以获得完全的事务支持。唯一不足地方是，最细粒度只能作用到方法级别，无法做到像编程式事务那样可以作用到代码块级别。

（2）spring的事务传播行为：

spring事务的传播行为说的是，当多个事务同时存在的时候，spring如何处理这些事务的行为。

① PROPAGATION_REQUIRED：如果当前没有事务，就创建一个新事务，如果当前存在事务，就加入该事务，该设置是最常用的设置。

② PROPAGATION_SUPPORTS：支持当前事务，如果当前存在事务，就加入该事务，如果当前不存在事务，就以非事务执行。‘

③ PROPAGATION_MANDATORY：支持当前事务，如果当前存在事务，就加入该事务，如果当前不存在事务，就抛出异常。

④ PROPAGATION_REQUIRES_NEW：创建新事务，无论当前存不存在事务，都创建新事务。

⑤ PROPAGATION_NOT_SUPPORTED：以非事务方式执行操作，如果当前存在事务，就把当前事务挂起。

⑥ PROPAGATION_NEVER：以非事务方式执行，如果当前存在事务，则抛出异常。

⑦ PROPAGATION_NESTED：如果当前存在事务，则在嵌套事务内执行。如果当前没有事务，则按REQUIRED属性执行。

（3）Spring中的隔离级别：

① ISOLATION_DEFAULT：这是个 PlatfromTransactionManager 默认的隔离级别，使用数据库默认的事务隔离级别。

② ISOLATION_READ_UNCOMMITTED：读未提交，允许另外一个事务可以看到这个事务未提交的数据。

③ ISOLATION_READ_COMMITTED：读已提交，保证一个事务修改的数据提交后才能被另一事务读取，而且能看到该事务对已有记录的更新。

④ ISOLATION_REPEATABLE_READ：可重复读，保证一个事务修改的数据提交后才能被另一事务读取，但是不能看到该事务对已有记录的更新。

⑤ ISOLATION_SERIALIZABLE：一个事务在执行的过程中完全看不到其他事务对数据库所做的更新。

**13、Spring框架中有哪些不同类型的事件？**

Spring 提供了以下5种标准的事件：

（1）上下文更新事件（ContextRefreshedEvent）：在调用ConfigurableApplicationContext 接口中的refresh()方法时被触发。

（2）上下文开始事件（ContextStartedEvent）：当容器调用ConfigurableApplicationContext的Start()方法开始/重新开始容器时触发该事件。

（3）上下文停止事件（ContextStoppedEvent）：当容器调用ConfigurableApplicationContext的Stop()方法停止容器时触发该事件。

（4）上下文关闭事件（ContextClosedEvent）：当ApplicationContext被关闭时触发该事件。容器被关闭时，其管理的所有单例Bean都被销毁。

（5）请求处理事件（RequestHandledEvent）：在Web应用中，当一个http请求（request）结束触发该事件。

如果一个bean实现了ApplicationListener接口，当一个ApplicationEvent 被发布以后，bean会自动被通知。

**14、解释一下Spring AOP里面的几个名词：**

（1）切面（Aspect）：被抽取的公共模块，可能会横切多个对象。 在Spring AOP中，切面可以使用通用类（基于模式的风格） 或者在普通类中以 @AspectJ 注解来实现。

（2）连接点（Join point）：指方法，在Spring AOP中，一个连接点 总是 代表一个方法的执行。 

（3）通知（Advice）：在切面的某个特定的连接点（Join point）上执行的动作。通知有各种类型，其中包括“around”、“before”和“after”等通知。许多AOP框架，包括Spring，都是以拦截器做通知模型， 并维护一个以连接点为中心的拦截器链。

（4）切入点（Pointcut）：切入点是指 我们要对哪些Join point进行拦截的定义。通过切入点表达式，指定拦截的方法，比如指定拦截add*、search*。

（5）引入（Introduction）：（也被称为内部类型声明（inter-type declaration））。声明额外的方法或者某个类型的字段。Spring允许引入新的接口（以及一个对应的实现）到任何被代理的对象。例如，你可以使用一个引入来使bean实现 IsModified 接口，以便简化缓存机制。

（6）目标对象（Target Object）： 被一个或者多个切面（aspect）所通知（advise）的对象。也有人把它叫做 被通知（adviced） 对象。 既然Spring AOP是通过运行时代理实现的，这个对象永远是一个 被代理（proxied） 对象。

（7）织入（Weaving）：指把增强应用到目标对象来创建新的代理对象的过程。Spring是在运行时完成织入。

切入点（pointcut）和连接点（join point）匹配的概念是AOP的关键，这使得AOP不同于其它仅仅提供拦截功能的旧技术。 切入点使得定位通知（advice）可独立于OO层次。 例如，一个提供声明式事务管理的around通知可以被应用到一组横跨多个对象中的方法上（例如服务层的所有业务操作）。

![icon](/assert/24.png)

**15、Spring通知有哪些类型？**

（1）前置通知（Before advice）：在某连接点（join point）之前执行的通知，但这个通知不能阻止连接点前的执行（除非它抛出一个异常）。

（2）返回后通知（After returning advice）：在某连接点（join point）正常完成后执行的通知：例如，一个方法没有抛出任何异常，正常返回。 

（3）抛出异常后通知（After throwing advice）：在方法抛出异常退出时执行的通知。 

（4）后通知（After (finally) advice）：当某连接点退出的时候执行的通知（不论是正常返回还是异常退出）。 

（5）环绕通知（Around Advice）：包围一个连接点（join point）的通知，如方法调用。这是最强大的一种通知类型。 环绕通知可以在方法调用前后完成自定义的行为。它也会选择是否继续执行连接点或直接返回它们自己的返回值或抛出异常来结束执行。 环绕通知是最常用的一种通知类型。大部分基于拦截的AOP框架，例如Nanning和JBoss4，都只提供环绕通知。 同一个aspect，不同advice的执行顺序：

```java
同一个aspect，不同advice的执行顺序：

①没有异常情况下的执行顺序：

around before advice
before advice
target method 执行
around after advice
after advice
afterReturning

②有异常情况下的执行顺序：

around before advice
before advice
target method 执行
around after advice
after advice
afterThrowing:异常发生
java.lang.RuntimeException: 异常发生
```

**58.两个相同的微服务间怎么保证数据的一致性？**

分布式锁实现方案有三种

 1.基于ZooKeeper的分布式锁.

2.数据库锁；

 3.基于Redis的分布式锁；

1.通过zookeeper的节点唯一性（推荐使用）

​		多个Jvm同时在Zookeeper上创建同一个相同的节点( /Lock)zk节点唯一的！ 不能重复！节点类型为临时节点， jvm1创建成功时候，jvm2和jvm3创建节点时候会报错，该节点已经存在。这时候 jvm2和jvm3进行等待。   jvm1的程序现在执行完毕，执行释放锁。关闭当前会话。临时节点不复存在了并且事件通知Watcher，jvm2和jvm3继续创建     

​		 ps：zk强制关闭时候，通知会有延迟。但是close（）方法关闭时候，延迟小2.通过redis的setnx来实现，该命令只能set不存在的值，如果set存在的值就会set失败（有死锁问题
3.也可以乐观锁，使用sql来解决库存超卖问题，在sql中判断 updat tb_stock set stock=stock-1 and stock>=1

**59.CAS单点登陆时的数据保存在哪？**

​		Cas Server端提供注册功能并维护用户通用信息，Cas Client端维护用户详细信息。腾讯等大型网站就是这样做的。

​		Cas Server端建一个集中注册和维护的用户信息库，仅存放通用信息，例如身份证号、员工编号、姓名和口令等等，CAS在此用户库上进行集中认证。可以用一个LDAP服务器，如ActiveDirectory来集中管理这个用户信息库。

当用户通过CAS验证访问客户端应用时，CAS传递用户凭证（身份证号、员工编号、姓名），客户端须判断该用户凭证是否在本系统中存在，如果已存在则自动进入系统，并遵循客户端权限管理； 

如果用户凭证在客户端应用中没有保存过，则根据业务需要判断CAS提供的用户通用信息是否足够用，若够用直接后台写入本系统用户表，然后进入系统；如果还需补充其它信息则弹出注册页面，显示通用信息，用户补充填入其它信息后提交，这样用户下次再访问本系统时就可以自动进入。

像QQ的应用，你登录时，就是手机、邮箱、密码这类通用的信息，这些信息就保存在CASServer端。进入各应用后，再完善扩展信息，如工作经验、性别、地区等，这个就好比QQ里微博信息的完善，像QQ校友里的学校的设置等等。

如果用户在业务系统中原本就有账户信息（在单点登录系统实施前的旧系统），则在上诉注册页面让用户选择绑定原有账户，输入原客户端应用的登录名和登录口令，验证通过后将用户的CAS凭证和旧账户绑定保存在客户端用户表中，这样用户再次访问客户端应用时就可以使用原账户的相关信息。

**60.springboot创建bean怎么创建？**

1.直接类上加注解@Component@Controller@Service 。。。

2.使用@Bean注解配合@Configuration注解

**61.java反射**

反射的作用：

1)，在运行时判断任意一个对象所属的类

2)，在运行时构造任意一个类的对象

3)，在运行时判断任意一个类所具有的成员变量和方法

4)，在运行时调用任意一个对象的方法

优点：灵活性高，动态的创建对象和编译对象

缺点：对性能有影响，比直接运行Java代码效率低

**62.redis相关问题**

1.什么是缓存雪崩，怎么解决？

<img src="/assert/25.png" alt="icon" style="zoom:75%;" />

如何解决？

<img src="/assert/26.png" alt="icon" style="zoom:75%;" />

- 对缓存做高可用，防止缓存宕机
- 使用断路器，如果缓存宕机，为了防止系统全部宕机，限制部分流量进入 DB，保证部分可用，其余的请求返回断路器的默认值。

2.什么是缓存穿透？怎解决？  **使用缓存的主要作用就是减少与数据库的交互**

**解释 1：**缓存查询一个没有的 key，同时数据库也没有，如果有人大量的使用这种方式，那么就会导致 DB 宕机。

**解决方案：**我们可以使用一个默认值来防止，例如，当访问一个不存在的 key，然后再去访问数据库，还是没有，那么就在缓存里放一个占位符，下次来的时候，检查这个占位符，如果发生时占位符，就不去数据库查询了，防止 DB 宕机。

**解释 2：**大量请求查询一个刚刚失效的 key，导致 DB 压力倍增，可能导致宕机，但实际上，查询的都是相同的数据。

**解决方案：**可以在这些请求代码加上双重检查锁。但是那个阶段的请求会变慢。不过总比 DB 宕机好。

3.什么是缓存并发竞争，怎么解决？

**解释：**多个客户端写一个 key，如果顺序错了，数据就不对了。但是顺序我们无法控制。

**解决方案：**使用分布式锁，例如 zk，同时加入数据的时间戳。同一时刻，只有抢到锁的客户端才能写入，同时，写入时，比较当前数据的时间戳和缓存中数据的时间戳

4.什么是缓存和数据库双写不一致？怎么解决？

解释：连续写数据库和缓存，但是操作期间，出现并发了，数据不一致了。

通常，更新缓存和数据库有以下几种顺序：

- 先更新数据库，再更新缓存。
- 先删缓存，再更新数据库。
- 先更新数据库，再删除缓存。

先更新数据库，再删除缓存。这个实际是常用的方案，但是有很多人不知道，这里介绍一下，这个叫 Cache Aside Pattern，老外发明的。如果先更新数据库，再删除缓存，那么就会出现更新数据库之前有瞬间数据不是很及时。

同时，如果在更新之前，缓存刚好失效了，读客户端有可能读到旧值，然后在写客户端删除结束后再次设置了旧值，非常巧合的情况。

有 2 个前提条件：**缓存在写之前的时候失效，同时，在写客户度删除操作结束后，放置旧数据 —— 也就是读比写慢。**** 设置有的写操作还会锁表。**

所以，这个很难出现，但是如果出现了怎么办？使用双删！！！记录更新期间有没有客户端读数据库，如果有，在更新完数据库之后，执行延迟删除。

还有一种可能，如果执行更新数据库，准备执行删除缓存时，服务挂了，执行删除失败怎么办？？？

这就坑了！！！不过可以通过订阅数据库的 binlog 来删除。

5.Redis 的过期策略

​	 Redis 是怎么删除过期的 key，而且 Redis 是单线程的，删除 key 会不会造成阻塞。要搞清楚这些，就要了解 Redis 的过期策略和内存淘汰机制。 

 **Redis采用的是定期删除 + 懒惰删除策略。** 

**定期删除策略**

Redis 会将每个设置了过期时间的 key 放入到一个独立的字典中，默认每 100ms 进行一次过期扫描：

1. 随机抽取 20 个 key
2. 删除这 20 个key中过期的key
3. 如果过期的 key 比例超过 1/4，就重复步骤 1，继续删除。

 **为什不扫描所有的 key？** 

Redis 是单线程，全部扫描岂不是卡死了。而且为了防止每次扫描过期的 key 比例都超过 1/4，导致不停循环卡死线程，Redis 为每次扫描添加了上限时间，默认是 25ms。

如果客户端将超时时间设置的比较短，比如 10ms，那么就会出现大量的链接因为超时而关闭，业务端就会出现很多异常。而且这时你还无法从 Redis 的 slowlog 中看到慢查询记录，因为慢查询指的是逻辑处理过程慢，不包含等待时间。

如果在同一时间出现大面积 key 过期，Redis 循环多次扫描过期词典，直到过期的 key 比例小于 1/4。这会导致卡顿，而且在高并发的情况下，可能会导致缓存雪崩。

**从库的过期策略**

从库不会进行过期扫描，从库对过期的处理是被动的。主库在 key 到期时，会在 AOF 文件里增加一条 del 指令，同步到所有的从库，从库通过执行这条 del 指令来删除过期的 key。

因为指令同步是异步进行的，所以主库过期的 key 的 del 指令没有及时同步到从库的话，会出现主从数据的不一致，主库没有的数据在从库里还存在

**懒惰删除策略**

 **Redis 为什么要懒惰删除(lazy free)？** 

 删除指令 del 会直接释放对象的内存，大部分情况下，这个指令非常快，没有明显延迟。不过如果删除的 key 是一个非常大的对象，比如一个包含了千万元素的 hash，又或者在使用 FLUSHDB 和 FLUSHALL 删除包含大量键的数据库时，那么删除操作就会导致单线程卡顿。  redis 4.0 引入了 lazyfree 的机制，它可以将删除键或数据库的操作放在后台线程里执行， 从而尽可能地避免服务器阻塞。 

 **unlink  key指令**，它能对删除操作进行懒处理，丢给后台线程来异步回收内存。 

 **flushdb 和 flushall 指令**，用来清空数据库，这也是极其缓慢的操作。Redis 4.0 同样给这两个指令也带来了异步化，在指令后面增加 async 参数就可以将整棵大树连根拔起，扔给后台线程慢慢焚烧。 

**redis中的内存淘汰机制**

Redis 的内存占用会越来越高。Redis 为了限制最大使用内存，提供了 redis.conf 中的
配置参数 maxmemory。当内存超出 maxmemory，**Redis 提供了几种内存淘汰机制让用户选择，配置 maxmemory-policy：**

- **noeviction：**当内存超出 maxmemory，写入请求会报错，但是删除和读请求可以继续。（使用这个策略，疯了吧）
- **allkeys-lru：**当内存超出 maxmemory，在所有的 key 中，移除最少使用的key。只把 Redis 既当缓存是使用这种策略。（推荐）。
- **allkeys-random：**当内存超出 maxmemory，在所有的 key 中，随机移除某个 key。（应该没人用吧）
- **volatile-lru：**当内存超出 maxmemory，在设置了过期时间 key 的字典中，移除最少使用的 key。把 Redis 既当缓存，又做持久化的时候使用这种策略。
- **volatile-random：**当内存超出 maxmemory，在设置了过期时间 key 的字典中，随机移除某个key。
- **volatile-ttl：**当内存超出 maxmemory，在设置了过期时间 key 的字典中，优先移除 ttl 小的。

**63.消息队列中如何保证消息的顺序性**

rabbitMQ场景：一个 queue，多个 consumer。比如，生产者向 RabbitMQ 里发送了三条数据，顺序依次是 data1/data2/data3，压入的是 RabbitMQ 的一个内存队列。有三个消费者分别从 MQ 中消费这三条数据中的一条，结果消费者2先执行完操作，把 data2 存入数据库，然后是 data1/data3。这不明显乱了。

<img src="/assert/28.png" alt="icon" style="zoom:75%;" />

 

解决方案： 拆分多个 queue，每个 queue 一个 consumer，就是多一些 queue 而已，确实是麻烦点；或者就一个 queue 但是对应一个 consumer，然后这个 consumer 内部用内存队列做排队，然后分发给底层不同的 worker 来处理。 

<img src="/assert/27.png" alt="icon" style="zoom:75%;" />

**64.同步方法和同步代码块的区别是什么？**

**区别：**

- 同步方法默认用this或者当前类class对象作为锁；
- 同步代码块可以选择以什么来加锁，比同步方法要更细颗粒度，我们可以选择只同步会发生同步问题的部分代码而不是整个方法；

**65.删除数据库中重复的数据？**

1.按照分组的方式获取最小id

```sql
select  min(id) id,workID from employee GROUP BY workID
```

2.从以上的内容中选取id列作为单独的一行

```sql
select id from(
SELECT
    min(id) id
FROM
    employee
GROUP BY
    workID ) tempt

```

3.删除不包含在内的内容

```sql
DELETE
FROM
	employee
WHERE
	id NOT IN (
		select id from(
SELECT
    min(id) id
FROM
    employee
GROUP BY
    workID ) tempt
	)
```

**66.Mabits中${}和#{}区别？**

#{} 和 ${} 在使用中的技巧和建议

（1）不论是单个参数，还是多个参数，一律都建议使用注解@Param("")

（2）能用 #{} 的地方就用 #{}，不用或少用 ${}  

（3）表名作参数时，必须用 ${}。如：select * from ${tableName}  

（4）order by 时，必须用 ${}。如：select * from t_user order by ${columnName}  

（5）使用 ${} 时，要注意何时加或不加单引号，即 ${} 和 '${}'

**67.并发编程相关**

并发编程的源头：1， 缓存导致的可见性 ；2， 线程切换带来的原子性问题 ；3， 编译优化的有序性问题 

java内存模型：解决可见性和有序性：

 可见性的原因是缓存,有序性的原因是编译优化,那解决的最直接的办法就是禁用缓存和编译优化,但是有缓存和编译优化的目的是提高程序性能,禁用了程序的性能如何保证? 合理的方案是按需禁用缓存和编译优化,Java内存模型规范了JVM如何提供按需禁用缓存和编译优化的方法,具体的,这些方法包括**volatile,synchronized和final三个关键字,以及六项Happens-Before规则** 

**Volatile**关键字：

 volatile关键字用来声明变量,告诉编译器这个变量的读写不能使用CPU缓存,必须从内存中读写. 

**68.springcloude相关**

@EnableDiscoveryClient和@EnableEurekaClient共同点就是：都是能够让注册中心能够发现，扫描到改服务。

不同点：@EnableEurekaClient只适用于Eureka作为注册中心，@EnableDiscoveryClient 可以是其他注册中心。
@SpringBootApplication：由@SpringBootConfiguration,@EnableAutoConfiguration,@ComponentScan组成

@EnableZuulProxy： @EnableZuulProxy简单理解为@EnableZuulServer的增强版，当Zuul与Eureka、Ribbon等组件配合使用时，我们使用@EnableZuulProxy。  




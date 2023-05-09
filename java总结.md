# java基础

 ## 开发环境

  > jdk > jre > jvm
  >
  > linux 环境变量配置在/etc/profile $ export PATH=.....

 ## 数据类型

 ### 基本数据类型共八种

  > 1. byte(1)
  >
  > 2. short(2)    前三种在运算时自动转换为int
  >
  > 3. char(2) 注意编码问题 代码单元,码点,基本语言平面
  >
  > 4. int(4)
  >
  > 5. float(4) 数字有效位6 ～ 7位  +- 3.40282347E+38F
  >
  > 6. long(8)
  >
  > 7. double(8)  数字有效位数15位 +- 1.79769313486231570E+308
  >
  > 8. boolean(4 or 1)布尔类型会在jvm里转换成int类型或byte数组，常量只有true 或 false
  >
  >    #### 浮点数的特殊数值：
  >
  >    > 1. 正无穷大(正整数➗0为正无穷大) Double.POSITIVE_INFINITY
  >    > 2. 负无穷大(负整数➗0为负无穷大)Double.NEGATIVE_INFINITY
  >    > 3. NaN(不是数字; 0/0 or 负数的平方根)Double.isNAN(x)检测x是不是数字

 ###  引用数据类型 *** (类的实例化对象)***

  > 1. 字符串
  > 2. 数组
  > 3. 集合
  > 4. 其他类的对象

  ## 控制结构

  > if  else
  >
  > if 	else if 	else
  >
  > switch	case
  >
  > for循环
  >
  > while循环	do	while循环
  >
  > for	each
  >
  > continue break

  ## 类与对象

  > 1. 封装:构造器,访问器,更改器--->数据私有方法公开
  >
  >    ```java
  >    public class Student {
  >             
  >        {
  >            System.out.println("creat a student"+ nextID);
  >        }
  >        private String name = "";
  >        private String age = "";
  >        private static int nextID = 1;
  >        static
  >        {
  >            System.out.println("class is ready");
  >            System.out.println(nextID);
  >        }
  >        private int stuID = 0;
  >        private Date time = new Date();
  >             
  >        public int study(int num) {
  >            System.out.println("学习");
  >             
  >            return 0;
  >        }
  >        public double study() {
  >            System.out.println("学习");
  >            return 99.0;
  >             
  >        }
  >             
  >        @Override
  >        public boolean equals(Object otherObject) {
  >            if (otherObject == null) return false;
  >            if (super.equals(otherObject)) return true;
  >            if (!(getClass() == otherObject.getClass())) return false;
  >            Student other = (Student) otherObject;
  >            return stuID == other.stuID;
  >        }
  >             
  >        @Override
  >        public int hashCode() {
  >            return Objects.hashCode(stuID);
  >        }
  >             
  >        @Override
  >        public String toString() {
  >            return getClass().getName() +
  >                    "[" + "name:" + name + age + "@" + stuID + "greattime:" + time + "]";
  >        }
  >             
  >        public Student() {
  >             
  >        }
  >             
  >        public Student(String name) {
  >            this.name = name;
  >        }
  >             
  >        public Student(String name, String age) {
  >            this.name = name;
  >            this.age = age;
  >            this.stuID = setStuID(nextID);
  >        }
  >            public String getName() {
  >              return name;
  >       }
  >    
  >       public void setName(String name) {
  >                      this.name = name;
  >       }
  >    
  >       public void setAge(String age) {
  >                      this.age = age;
  >       }
  >    
  >       public int getStuID() {
  >                      return stuID;
  >       }
  >    
  >       private int setStuID(int stuID) {
  >               
  >           return nextID++;
  >               
  >       }
  >               
  >       public String getAge() {
  >                      return age;
  >       }
  > 
  > 2. 继承:抽象出多种数据类型的共同属性和方法,子类可以直接使用或重写[覆盖]方法(权限符合)
  > 
  >   ```java
  >    
  >   public class Instrument {
  >        public void play(){
  >           System.out.println("play the Instrument");
  >        }
  >    }
  >    public class Brass extends Instrument{
  >        @Override
  >        public void play() {
  >            System.out.println("play the brass");
  >        }
  >        public void play2(){
  >            System.out.println("调用brass的play2");
  >        };
  >    }
  >    public class Wind extends Instrument{
  >        @Override
  >        public void play(){
  >            System.out.println("play the wind");
  >        }
  >        public void play2(){
  >            System.out.println("调用wind的play2");
  >        }
  >    }
  >   ```
  > 
  > 
  > 
  > 3. 多态:一个类型变量可以引用多个不同类型的实例,父类的方法在不同子类有不同的行为,会根据编译类型和实际类型实现
  >
  >       ```java
  >     public class Music {
  >        public static void main(String[] args) {
  >           Instrument[] instruments = new Instrument[3];
  >            instruments[0] = new Instrument();
  >            instruments[1] = new Wind();
  >            instruments[2] = new Brass();
  >          
  >            for (Instrument a :
  >                    instruments) {
  >                a.play();
  >                         if (a.getClass() == Wind.class) ((Wind) a).play2();
  >                if (a.getClass() == Brass.class) ((Brass) a).play2();
  >          
  >            }
  >          
  >        }
  >             }
  >    ```

  > ---
  >
  > 
  >
### **!重载与重写**
  >
  > 1.重载(Overload):相同的功能,相同的方法名,不一致的形参列表,即为重载
  >
  > 2.重写(Override):个性化的功能,相同的方法签名,返回值类型可以相同也可以不同(指的是可以自动转换为父类方法的返回类型的类型)经常重写的方法有
  >
  > > toString
  > >
  > > equals 和 hashcode 
  > >
  > > 1. equals方法的五条原则:自反性,对称性,传递性,一致性,非空对象比null返回false
  > > 2. 如果两个对象用equals方法对比相等,那么他们的hashcode也要相等

---

  

### **!动态绑定与静态绑定**
  >动态绑定:***虚拟机***调用的方法依赖于隐试参数时,调用实际类型的实例方法,如果没有,就会寻找父类的方法,依次向上
  >
  >静态绑定:如果是***private***方法,***static***方法,***final***方法或者***构造器***,那么***编译器***将知道准确调用哪个方法,为静态绑定

### 访问修饰符

| 修饰符\范围 | 同类 | 同包 | 子类 | 其他类 |
| ----------- | ---- | ---- | ---- | ------ |
| private     | true |      |      |        |
| 默认        | true | true |      |        |
| protected   | true | true | true |        |
| public      | true | true | true | true   |

### 接口***(interface)***

> 接口不是类，是对希望符合这个接口类的一组需求，可以抽象对象的行为,接口可以多实现***(implements)*** 
>
> 1. 接口可以包含常量***(static final)***
>
> 2. 接口中的方法自动为***public***
>
> 3. 可以用default关键字定义方法体(方法冲突，超类优先，否则必须重写方法)
>
> 4. 可以存在静态方法
>
> 5. 可以用[^lambda]表达式简化函数式接口的语法
>
>    ```java
>    public class ThreadDemo02 {
>        public static void main(String[] args) {
>               Thread thread = new Thread(() -> {for (int i = 1;i < 100 ;i ++)
>               		System.out.println("sssf"+i);});
>           	   Thread thread1 = new Thread(() -> {for (int i = 1;i < 100 ;i ++)
>               		System.out.println("ss"+i);});
>           	   thread1.start();
>               thread.start();
>               System.out.println("main");
>       }
>            
>
> 

## 异常处理

![Java中的异常层次结构](https://upload-images.jianshu.io/upload_images/10059245-bbe075c98468571a.png)

- RuntimException 和 Error为***非检查型异常***

- 其他异常为***检查型***

- 抛出异常throws

- 捕获异常

  ```java
  try{
      
  }catch(Exception e){
      
  }finally{
      
  }
  try(Resource res = ...){
      
  }cathc(Exception e){
      
  }
  ```

  

  ```java
  import java.io.FileInputStream;
  import java.io.FileNotFoundException;
  import java.io.FileOutputStream;
  import java.io.IOException;
  
  public class ExceptionDemo01 {
      @SuppressWarnings({"all"})
      public static void main(String[] args) {
  
          try (FileInputStream a = new FileInputStream("tdt.png")) {
              FileOutputStream c = new FileOutputStream("ttt_copy.png");
              int b;
              byte[] bytes = new byte[1024 * 4];
              while ((b = a.read(bytes)) != -1){
                  c.write(bytes);
              }
          } catch (IOException e) {
              if (e.getClass() == FileNotFoundException.class) {
                  System.out.println("not found file");
              }else {
                  e.printStackTrace();
              }
         }  finally {
              System.out.println("运行结束");
          }
  
      }
  
  }
  
  ```

## 多线程

![线程状态图](https://img-blog.csdn.net/20180512102914671?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NoaTJodWFuZw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

> - 创建线程的方式：
>
>   1. 继承Thread类重写run()方法
>   2. 实现Runable接口重写run()方法(lambda表达式或者内部类)，然后把对象放入Thread类的构造器
>
> - 将线程转换为可运行模式，调用start()方法
>
> - 可以用***synchronized***关键字来控制线程的执行
>
>   1. 将关键字写在方法头中
>
>      ```java
>      public class Bank {
>          private int account = 10000;
>      
>          public int getAccount() {
>              return account;
>          }
>      
>          public void setAccount(int account) {
>              this.account = account;
>          }
>          public synchronized boolean getMoney(int money){
>              if (money < 0) {
>                  System.out.println("失败");
>                  return false;
>              }
>              int account = getAccount();
>              if (account >= money) {
>                  account -= money;
>                  setAccount(account);
>                  System.out.println("出钞票成功！账户余额"+getAccount());
>                  return true;
>              }
>              System.out.println("失败");
>              return false;
>          }
>      }
>      ```
>
>      2. 利用线程锁同步代码块
>
>         ```java
>         public class Shop{
>             //此处不适合使用同步方法,因为效率太低,而且挑衣服的动作可以一起做
>             //public synchronized void buy(){
>             public void buy(){
>                 try {
>                     Thread t = Thread.currentThread();//获取运行buy方法的线程对象
>                     System.out.println(t.getName()+":正在挑衣服...");
>                     Thread.sleep(5000);
>                     /*
>                      * 同步块在使用的时候,需要在"()"中指定同步监视器对象,该对象可以是任何引用类型的实例,
>                      * 必须要保证多个需要同步执行该代码块的线程看到的这个同步监视器对象是"同一个"!
>                      * 需要结合开发中的实际业务决定
>                      * */
>                     synchronized (this){
>                         System.out.println(t.getName()+":正在试衣服...");
>                         Thread.sleep(5000);
>                         System.out.println(t.getName() + "离开试衣间");
>                     }
>                     System.out.println(t.getName()+":结账离开!");
>                 } catch (InterruptedException e) {
>                 }
>             }
>         }
>         public class SyncDemo02 {
>             public static void main(String[] args) {
>                 Shop shop = new Shop();
>                 Thread hulk = new Thread(new Thread() {
>                     @Override
>                     public void run() {
>         
>                             shop.buy();
>                        
>                     }
>                 });
>                 Thread ken = new Thread(() -> {
>                     shop.buy();
>                 });
>                 hulk.start();
>                 ken.start();
>             }
>         }
>         ```



## [JavaAPI](https://docs.oracle.com/javase/8/docs/api/)

见[^api]文档



[^lambda]: (parameter) -> {method}
[^api]: https://docs.oracle.com/javase/8/docs/api/
## 异常
	概念 : 在java等面向对象语言中 异常本身是一个类，产生异常就是		创建异常对象并抛出异常对象,交由jvm中断处理
	体系 : 根类 : java.lang.Throwable 可抛出
		   子类 : java.lang.Error 错误 不能处理的问题
				 java.lang.Excption 异常类(编译期异常) 写代码
				Exception子类  : 
					java.lang.RuntimeExcption (运行期异常)
					java程序运行过程中出现的异常(非运行期异常)
	*异常就相对于一个小问题，把异常处理掉,程序可以继续执行
	*错误 : 程序出现错误,必须修改源代码	
	
## 异常的产生过程与处理
	jvm检测到程序出现异常
	1. jvm会根据异常原因创建一个异常对象，该异常对象包含异常产生的(内容，原因，位置)
		 new ArrayIndexOutOfBoundsException("3")
	2.在出现异常方法中,没有异常的处理逻辑(try...catch),jvm将异常对象抛给方法的调用者,main()来处理异常,main方法也没有处理逻辑,则依次上抛给main方法的调用者JVM
	3.jvm接收到异常对象后
		1.把异常对象(内容，原因，位置)以红色字体打印在控制台
		2.JVM将终止正在执行的java程序

## 异常处理
	throw关键字 抛出指定异常(自己不处理 交给别人处理)
		使用格式 : throw new xxxException("异常产生的原因");
		注意 :
			1.throw关键字必须写在方法内部
			2.throw关键字后面new的对象必须时Exception或其子类
			3.thorw抛出的异常对象必须处理
				* RuntimeException 或 其子类 可以不处理交给；默认交给jvm处理
				*编译异常,必须处理,要么throw,要么try..catch
			4.抛出的异常有子父类关系,声明父类异常
			5.调用声明抛出异常的方法，就必须处理声明的异常
				要么继续抛出 要么try..catch
		## 以后工作中，首先必须对方法参数进行合法性校验
				 if (arr == null )
					throw new NullPointerException("传递的数组的值为空") //运行期异常
				if(index > arr.length || index < 0)
					throw new ArrayIndexOutOfBoundException("数组越界异常")
		缺陷 : 异常后面的代码不会执行
	try...catch
		格式:
			try{
				可能产生异常的代码
			}catch(定义一个异常对象，用来接受try中的抛出的异常对象){
				怎么处理异常，一般把异常信息记录到一个日志中
			}
			
## Objects类中静态方法
	public static <T> T requireNonNull(T obj) 查看指定引用对象是不是null
		if(Objects.requireNonNull(obj))   

## Throwable类异常处理的方法
	String getMessage(); Returns a short description of 	this throwable
	String toString(); .Returns the detail message string 	of this throwable.
	void printStackTrace(); Prints this throwable and its 	backtrace to the standard error stream.
		jvm打印异常对象,默认此方法，打印异常信息时最全面的
## 异常捕获
	1.一次try,多此catch
		catch里异常变量有子父类关系,子类异常必须写在上面.(子类写在下面不会被生效)
	2.多个异常，一次捕获，一次处理
		catch对象 catch(Exception e)

	*finally代码块
		有return语句，永远返回finally中结果
## 子父类异常
	父类异常是什么样，子类异常就是什么样
	父类声明抛出异常,子类重写父类方法时，抛出与父类相同的异常或者不抛出异常
	父类方法没有抛出异常，子类重写方法时也不可抛出异常。子类产生的异常，只能捕获处理

## 自定义异常
	java提供的异常类不够使用

	public class XxxException extends Exception | RuntimeException{
		添加一个空参构造方法
		添加一个带异常信息的构造方法
		调用父类带异常的构造方法
		public XxxException(){
			super();
		}
		
		public XxxException(String message){
			super(message);		
		}
	}	

	*RuntimeException 不需要处理，交给jvm中断处理

*自定义异常练习
	要求 : 模拟注册操作，如果注册名已存在，则抛出异常并提示
	02_day05Exception cn.hr.ExceptionDemo1 cn.hr.RegisterException
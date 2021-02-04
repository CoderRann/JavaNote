## 一、简述String类中的equals方法与Object类中的equals方法的不同点。
 * String类中的equals方法是用来判断两个对象的内容是否相同
 * Object 类中的equals方法是用来判断两个对象是否是同一个对象，所谓同一个对象指的是内存中的同一块存储空间(与==相同比较地址)
 
## 二、Object类的toString方法
  直接说出打印结果，并解释原因。
	
    public class ToStringTest{
   		 static int i = 1;
  	     public static void main(String args[]){
       	 System.out.println("love " + new ToStringTest());
    	 ToStringTest a = new ToStringTest();
    	 a.i++;
    	 System.out.println("me " + a.i);//me 2
    	}
   		public String toString(){
    	 	System.out.print("I ");//I
    	 	return "java ";
    	}
	}


**分析**

* 1.加载静态变量
* 2.执行main方法,由于main方法内部第一行代码为输出语句，里面**new了此类对象**，当执行此行代码时会**先创建了本类的对象**，由于此类重写了toString方法，会**先执行toString方法**的打印输出，然后返回“java ”，再执行main方法第一行打印输出
* 3.什么时候会**自动调用toString**方法?
	* 当我们打印对象时,使用println和print方法时 
	
			public void println(Object x){
             String s = String.valueOf(x);
             synchronized (this) { 
                      print(s); newLine();
      		}
   			public void print(Object obj) {
              write(String.valueOf(obj));
			}
	* 这两个方法是 System.out.print和println()方法传入一个 Object 类对象时打印 的内容,当然,传入其它类时，同样如此。	
	* 当要打印一个对象时，会自动调用 String.valueOf()这个方法，下面是这个方法的代码： 
	
			public static String valueOf(Object obj) { 
  		  	   return (obj == null) ? "null" : obj.toString(); 
			}
	* 而 String.valueOf()方法会调用toString方法
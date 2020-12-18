## 一、简述String类中的equals方法与Object类中的equals方法的不同点。
 * String类中的equals方法是用来判断两个对象的内容是否相同
 * Object 类中的equals方法是用来判断两个对象是否是同一个对象，所谓同一个对象指的是内存中的同一块存储空间(与==相同比较地址)
 
## 二、Object类的toString方法
  直接说出打印结果，并解释原因。
	
    public class ToStringTest{
   		 static int i = 1;
  	     public static void main(String args[]){
       	 System.out.println("love " + new ToStringTest	());//love java
    	 ToStringTest a = new ToStringTest();
    	 a.i++;
    	 System.out.println("me " + a.i);//me 2
    	}
   		public String toString(){
    	 	System.out.print("I ");//I
    	 	return "java ";
    	}
	}

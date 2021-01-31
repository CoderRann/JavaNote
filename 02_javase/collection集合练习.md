## 1.简述集合框架
	
* 单列集合java.util.Collection
	* List的特点是元素有序、元素可重复。
		* java.util.ArrayList
		* java.util.LinkedList 
	* Set的特点是元素无序，而且不可重复。
		* 实现类有java.util.HashSet
		* java.util.TreeSet。 
* 双列集合java.util.Map。
	
## 2.Collection集合统计元素出现次数
给定以下代码,请定义方法listTest()统计集合中指定元素出现的次数，如"a": 2,"b": 2,"c" :1, "xxx":0。
		
	Collection<String> list = new ArrayList<>();
		list.add("a");
		list.add("a");
		list.add("b");
		list.add("b");
		list.add("c");
		System.out.println("a:"+listTest(list, "a"));	
		System.out.println("b:"+listTest(list, "b"));	
		System.out.println("c:"+listTest(list, "c"));
		System.out.println("xxx:"+listTest(list, "xxx"));
**解答**
	
	private static int listTest(Collection<String> list, String s) {
        int count = 0;
        for (String a:list
             ) {
            if (a.equals(s)) {
                count++;
            }
        }
        return count;
    }		
## 3.Collection集合数组转集合
定义一个方法，要求此方法把int数组转成存有相同元素的集合(集合里面的元素是Integer)，并返回。
	 
	public static void main(String args[]) {
        Collection<Integer> list = new ArrayList<>();
        int []arr = {1,2,3,4};
        list =  listTest(list,arr);
        System.out.println(list);

    }

    private static Collection<Integer> listTest(Collection<Integer> list, int[] arr) {
        for (int a : arr
        ) {
            list.add(a);
        }
        return list;
    }

## 4.Collection集合contains()方法使用
定义一个方法listTest(ArrayList<String> al, String s),要求使用contains()方法判断al集合里面是否包含s。
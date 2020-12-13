
JDBC实现
public class jdbcDemo1 {
    public static void main(String[] args) throws Exception {
        //import  package jar
        //注册驱动
        Class.forName("com.mysql.jdbc.Driver");
        //获取数据库连接对象
        Connection conn = getConnection("jdbc:mysql://localhost:3306/db3", "root", "root");
        //定义sql语句
        String sql = "update abc set name = 'jn' where idstu = 1";
        //获取执行sql语句的对象 statement
        Statement stmt = conn.createStatement();
        // executer sql return result
        int i = stmt.executeUpdate(sql);
        //traiter des résults
        //
        System.out.println(i);
        //释放资源
        stmt.close();
        conn.close();
    }
}

jdbc各个对象详解
	1. DriverManager 驱动管理对象
		功能
			1. 注册驱动 registration driver
			class.forname(类)加载进内存 load into memory
			static void registerDrive(Driver driver)  //注册与给定的驱动程序
				class.forname("com.mysql.jdbc.Driver"); 存在静态代码块随着类的加载自动执行
				static {
					try {
						java.sql.DriverManager.registerDriver(new Driver());
						} catch (SQLException E) {
					throw new RuntimeException("Can't register driver!");
					}
				}
			2. 获取数据库连接
			static Connection getConnection(String url, String user, String password) 
				Attempts to establish a connection to the given database URL. 
			参数
				url : 指定连接的路径  jdbc:mysql://@ip: num port/name database
	2. connection 数据库链接对象
		功能
			1.获取执行sql语句的对象
				Statement createStatement()
				PreparedStatement prepareStatement(String sql)
			2.管理事务
				开启事务 void setAutoCommit(boolean autoCommit) 调用该方法设置参数为false 开启事务
				提交事务 void commit()
				回滚事务 void rommback()
	3.Statement : 执行sql的对象
		用于执行静态sql并返回结果
			boolean executer(String sql)
			int executeUpdate(String sql) 执行DML(insert,update delete)语句 DDL(create,alter,drop)
				返回值：数据库中影响的行数 >0 executer success               没有返回值
			ResultSet executeQuery(String sql) 执行DQL语句 select
	4.ResultSet : 结果集对象,封装结果
		boolean next(); 游标向下移动一行 //游标默认在顶行 判断当前游标所在行是否有数据 true表示有数据 false无
		getXxx(参数);获取数据
			Xxx : 代表数据类型 如 Int getInt();
			参数 :
				int 代表列的编号，从1开始 getString（1）
				String 代表列名称
		 
			rs= stmt.executeQuery(sql);
			while(rs.next()){
			int idstu = getInt(1);
			String name = getString（2）;
			
			sout(id +"--"+name);
			}
			
			
	表相当于类，表的每条相当于对象，将各个对象封装在集合里.
		
	5.PreparedStatement ：Statement子接口
		1.sql注入问题 : 在拼接sql时,有一些sql的特殊关键字参与字符串拼接.
			1.输入用户名随便,输入密码 : a' or 'a' = 'a
			2.sql="select * from user where username = 'sdqd' and password = 'a' or 'a' = 'a'"; 为恒等式
 				where条件输入失效
		2.用PreparedStatement：Statement子接口 解决sql注入
		3.预编译的sql:参数使用？作为占位符
				定义sql语句 : 如 select * from user where username= ？;
		4.步骤
			1.导入jar包
			2.注册驱动
			3.获取数据库连接对象
			4.定义sql语句
        		String sql = "update abc set name = ？ where idstu = 1";
        	5.获取执行sql语句的对象 PreparedStatement
        		PreparedStatement prestmt = conn.PrepqredStatement(sql);
			5.给？赋值 
				*方法:setXxx方法(参数1,参数2)
					*参数1:？的位置参数
					*参数2:？的值
			6.执行sql
				pstmt.executeQuery() //空参子类方法
			7.处理结果
			8.释放资源
       	5.后期都会使用preparedStatement对象
			效率更高


## 抽取jdbc工具类 : jdbcUtils
	*分析
		1.注册驱动抽取
		2.抽取一个方法获取连接对象
			* 需求:不想传递参数、还想保证工具类的通用性
			* 解决 配置文件
				jdbc.properties
					url=
					user=
					password=
					 
		3.抽取一个方法释放资源
## 练习
	1.通过键盘录入用户名与密码
	2.判断是否登陆成功
		select * from user where username = '' and password = '';
		如果返回值为true 即登录成功
	
	*步骤
		1.创建user表
			CREATE TABLE USER(
				id INT PRIMARY KEY  AUTO_INCREMENT,
				username VARCHAR(32),
				PASSWORD VARCHAR(32)
				);

			SELECT * FROM USER;
			
			INSERT INTO USER VALUE(NULL,'zhangsan','123');
			INSERT INTO USER VALUES(NULL,'lishi','234');

##JDBC控制事务
	1.事务。 一个包含多个步骤的业务操作.如果这个业务操作被事务管理,则这多个步骤要么同时成功,要么同时失败
	2.操作 :
		1.开启事务
		2.提交事务
		3.回滚事务
	3.使用connnection对象管理
		开启事务 void setAutoCommit(boolean autoCommit) 调用该方法设置参数为false 开启事务
			conn后开启
		提交事务 void commit()
			当所有sql执行完毕
		回滚事务 void rommback()
			catch 后回滚
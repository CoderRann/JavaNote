## 今日内容
	1.数据库连接池

	2.Spring JDBC : JDBC template


## 数据库连接池
	1.其实就是一个容器(集合),存放数据库连接的容器
		当系统初始化好后,容器被创建,容器中会申请一些连接对象,当用户来访问数据库时,从容器中获取连接对象,用户访问结束后,会将连接对象归还给容器.
	2.好处
		节约资源
	3.实现
		1. 标准接口 : DateSource javax.sql包下 sun官方提供
			1.方法
				* 获取连接 : getConnection()
				* 归还连接 : Connection.close()如果Connection对象由连接池获取的,则调用close方法,代表归还连接.
		2. 有数据库厂商来实现
			1. C3P0 : 数据库连接池技术
			2. Druid : 由阿里提供
			
		3. C3P0 
			*步骤
				1.导入jar包 c3p0-0.9.5.5.jar
				mchange-commons-java-0.2.19.jar
				mysql-connector-java-5.1.37-bin.jar
				2.定义配置文件 
					名称 : c3p0.properties c3p0-config.xml
					路径 : 放在类目录 src目录下
				3.创建核心对象 数据库连接池对象 	ComboPooledDateSource
				4.获取连接 : getConnection()
		4.Druid : 
			*步骤
				1.导入jar包 druid-1.0.9.jar
				mysql-connector-java-5.1.37-bin.jar
				2.定义配置文件 
					properties文件形式
					名称 : 可以为任何名称
					路径 : 任意目录
				3.加载配置文件 properties
				3.获取数据库连接池对象 : 通过工厂类获取
					DruidDataSourceFactory
				4.获取连接 : getConnection()
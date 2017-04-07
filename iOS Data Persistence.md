# iOS 持久化
+ 属性列表：XML文件
	+ NSArray
		+ arrayWithContentsOfFile(`Only OC`) 
		+ initWithContentsOfFile
		+ writeToFile: atomically:
	+ NSDictionary 
		+ dictionaryWithContentOfFile (`Only OC`)
		+ initWithContentsOfFile
		+ writeToFile: atomically:
+ 对象归档：先将归档对象序列化为一个文件，然后在通过反归档将数据恢复到对象中
	+ 归档对象必须实现NSCoding协议
	+ 每个成员变量应该是基础数据类型或都是实现NSCoding协议的某个类的实例 
	+ 归档过程使用NSKeyedArchiver对象归档数据
	+ 反归档过程使用NSKeyedUnarchiver对象反归档数据
+ SQLite数据库
	+ 支持的数据类型
		+ INTEGER：有符号整数类型
		+ REAL：浮点类型
		+ TEXT：字符串类型
		+ BLOB：二进制大对象
+ Core Data

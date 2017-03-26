# iOS File Manager

## 沙盒机制
+ iOS没有SDK概念，程序之间文件不能互相访问。只能对自身目录下文件进行读写操作
+ 文件目录
	+ Documents：程序创建或应用浏览产生的文件数据
	+ Library：程序的默认设置或状态信息保存在该目录
	+ tmp：提供一个即时创建临时文件的地方，但不需要持久化
+ 获取沙盒路径

```objective-c
NSString *homePath = NSHomeDirectory();
```  

+ 获取`Documents`路径

```objective-c
// 检索制定路径
NSArray *docPaths = NSSearchPathDirectoriesInDomains(NSDocumentsDirectory, NSUserDomainMask,YES);
NSString *documentsPath = [docPaths lastObject];
```

+ 获取`Library`路径

```objective-c
// 检索制定路径
NSArray *libPaths = NSSearchPathDirectoriesInDomains(NSLibraryDirectory, NSUserDomainMask,YES);
NSString *libraryPath = [libPaths lastObject];
```

+ 获取`Tmp`路径

```objective-c
NSString *tmpPath = NSTemporaryDirectory();
```

+ NSData：二进制数据，屏蔽了数据之间的差异。用于包装数据
	+ NSData -> NSString

	```objective-c
	NSString *str = [[NSString alloc] initWithData:data encoding:NSUTF8String];
	```

	+ NSString -> NSData 
	
	```objective-c
	NSData *data = [str dataUsingEncoding:NSUTF8StringEncoding];
	```
	
	+ NSData -> UIImage
	
	```objective-c
	UIImage *image = [UIImage imageWithData:data];
	```
	
	+ UIImage -> NSData
	
	```objective-c
	NSData *data = UIImagePNGRepresentation (image);
	```
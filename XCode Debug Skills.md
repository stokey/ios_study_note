# XCode调试
+ 断点
	+ 文件行断点：直接点击文件中的行号即可
	+ 符号断点：打开断点导航面板，点击`+`添加`Add Symbolic Breakpoint`[`特定方法名的断点设置`]
	+ 异常断点：打开断点导航面板，点击`+`添加`Add Exception Breakpoint`[`给未设置try/catch的代码添加捕获异常的能力`]
	+ OpenGL ES断点
	+ 单元测试失败断点 
+ 日志
	+ NSLog
	+ NSLogv：将输出重新定向到文件中

	
|              类型                 |   实例  |  NSLog中的格式化字符串 |
| :----------------------------: | :--------: | :----------------------------------: |
|              char                 |   'a'  |  %c |
|  short int       |   -10  |  %hi,%hx,%ho |
| unsigned short int   |   9  |  %hu,%hx,%ho |
|    int     |   9  |  %i,%x,%o |
|  unsigned int  |   17u  |  %u,%x,%o |
|      unsigned long/long int         |   17UL/17L,0xffffUL/0xffffL  |  %li,%lx,%lo |
|      float         |   12.3f  |  %f,%e,%g |
|      double       |   12.34  |  %f,%e,%g|
|      long double        |   12.34l  |  %Lf,%Le,%Lg |
|      对象指针        |   “<<Note:0x7697220>>” |  %p,%@ |

	
+ 断言
	+ NSAssert—Objective-C
	+ assert/assertionFailure—Swift
+ 通过设备管理器查看设备日志信息：Window --> Devices --> View Device Logs 


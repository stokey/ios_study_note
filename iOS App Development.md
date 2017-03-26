# iOS App Development

## AppDelegate

+ main 函数会执行一个AppDelegate类
+ AppDelegate相当于Android MainActivity
+ 主要实现功能
	+ setStatusBarStyle
	+ self.window/self.window.backgroundColor赋值  
	+ self.mainViewController赋值
	+ self.window.rootViewController = self.mainViewController
	+ [self.window.makeKeyAndVisible]
+ ViewController相当于Android Activity
	+ [self presentViewController]设置当前显示ViewController
	+ 页面之间参数传递，可以通过直接设置相关ViewController相关属性值实现
+ UIButton点击事件
	+ `[self.addLocationButton addTarget:self  action: @selector(addLocationButtonPressed)  forControlEvents: UIControlEventTouchUpInside];
`   
+ BackgroundColor
	+ view.backgroundColor = [UIColor colorWithPatternImage:[UIImage imageNamed:@"background.png"]]
	+ view.backgroundColor = [UIColor clearColor] 
+ NSUserDefaults：相当于Android SharePreference（key-value）
+ NSData
+ NSKeyedUnarchiver
+ 读取本地文件
	+ NSString *path = [[NSBundle mainBundle]pathForResource:@"API_KEY" ofType:@""]; //读取文件路径
	+ NSString *content = [NSString stringWithContentsOfFile:path encoding:NSUTF8StringEncoding error:nil]; //从路径中读取文件内容
+ Objective-C 实现单例模式：`dispatch_one`

```objective-c
+(SOLWundergroundDownloader *) sharedDownloaderInstance{
	static SOLWundergroundDownloader *shareDownloader = nil;
	static dispath_one_t onceToken;
	dispatch_one(&onceToken, ^{
		 NSString *path = [[NSBundle mainBundle]pathForResource:@"API_KEY" ofType:@""];
		 NSString *content = [NSString stringWithContentsOfFile:path encoding:NSUTF8StringEncoding error:nil];
		 NSString *apiKey = [content stringByTrimmingCharactersInSet:[NSCharacterSet newlineCharacterSet]];
		 sharedDownloader = [[SOLWundergroundDownloader alloc]initWithAPIKey:apiKey];
	});
	return shareDownloader;
}
```

+ JPG to PNG：UIImage ===>PNG(JPG) NSData ===>UIImage

```objective-c
UIImage *image = [UIImage imageNamed:@"j1.jpg"];
NSData *data = UIImagePNGRepresentation(image);
UIImage *imagePng = [UIImage imageWithData:data];
``` 

+ ImageView加载GIF文件
	+ 引入头文件：`ImageIO/MobileCoreSevices` 
	+ 获取GIF图片数据 

		```objective-c
		NSString *gifPathSource = [[NSBundle mainBundle] pathForResource: @"jiafei" ofType:@"gif"];
		NSData *data = [NSData dataWithContentOfFile: gifPathSource];
		```
	+ 将GIF数据分解

		```objective-c
		CGImageSourceRef source = CGImageSourceCreateWithData((__bridge CFDataRef) data, NULL);
		```
	+ 将单帧数据转换成UIImage

		```objective-c
		size_t count = CGImageSourceGetCount(source);
		NSMutableArray *tempArray = [[NSMutableArray alloc] init];
		for (size_t i=0; i < count; i++){
			CGImageRef imageRef = CGImageSourceCreateImageAtIndex(source, i, NULL);
			UIImage *image = [UIImage imageWithCGImage:imageRef scale:[UIScreen mainScreen].scale orientation:UIImageOrientationUp];
			[tmpArray addObject:image];
			CGImageRelease(imageRef); //释放CGImageRef对象
		}
		CFRelease(source); //释放CGImageSourceRef对象
		```
	+ 保存单帧图片 
		
		```objective-c
		NSArray *pathArray = NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES);
		NSString *path = pathArray[0];
		if (path) {
			for (int i=0; i < [tempArray count]; i++){
				NSData *data = [tempArray objectAtIndex: i];
				NSString *pathName = [path stringByAppendingString: [NSString stringWithFormat:@"/%d.png",i]];
				[data writeToFile: pathName atomically: NO];
			}
		}
		```
	+ 使用动画方式显示GIF图片
		
		```objective-c
		UIImageView *imageView = [[UIImageView alloc] initWithFrame: CGRectMake(0, 100, 270,140)];
		[imageView setAnimationImages: tempArray];
		[imageView setAnimationRepeatCount:10]; // 设置动画重复次数
		[imageView setAnimationDuration:2]; //设置动画持续时间
		[imageView startAnimating];
		```	
+ __bridge：用于Objective-C和Core Foundation指针之间的转换。这种转换不会更换对象的所有权
+ __bridge+transfer/CFBridgeRelease：将非Objective-C指针转换为Objective-C指针。对象所有权会交给ARC
+ __bridge+retained/CFBridgeRetain：用于从Objective-C到Core Foundation的指针转换，并且会将对象的所有权（ownership）转移，所以你需要在不再使用该对象的时候调用CFRelease方法来解除引用

+ iOS数据解析
	+ JSON
		+ TouchJson
		+ JSONKit
		+ SBJson
		+ iOS JSON库[iOS5+]
			+ NSJSONSerialization
			+ JSONObjectWithData: options: error:
					
		```objective-c
		NSString *jsonStr = @"{\"name\":\"James\",\"age\":\"30\"}";
		NSData *jsonData = [jsonStr dataUsingEncoding:NSUTF*StringEncoding];
		id jsonObj = [NSJSONSerialization JSONObjectWithData:jsonData options:NSJSONReadingAllowFragments error:nil];
		if ([jsonObj isKindOfClass:[NSDictionary class]]){
			// 字典类型	
		} else if ([jsonObj isKindOfClass:[NSArray class]]{
			// 数组类型
		}
		```  
		 
	+ XML
		+ SAX
		+ DOM
		+ PULL  
+ Objective-C `isa` 
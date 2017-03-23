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

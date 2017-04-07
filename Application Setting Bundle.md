# 应用程序设置
+ 设置：在使用中是不经常变化的，决定了应用的一些基本行为和特征
+ 配置：在使用中经常变化的。

+ 应用程序设置包
	+ Setting Bundle：包含设置界面中所需的设置项目描述、用到的图片、文字的本地化和子设置界面项目的描述等内容
	+ Setting Bundle类型
		+ PSGroupSpecifier（组）：其他设置项目放置在组中
		+ PSTextFieldSpecifier（文本字段）：指示项目是文本字段类型
		+ PSTitleValueSpecifier（标题）：指示该项目是标题类型
		+ PSSliderSpecifier（滑块）：指示该类型是滑块类型
		+ PSToggleSwitchSpecifer（开关）
		+ PSMultiValueSpecifier（值列表）
		+ PSChildPaneSpecifier（子界面） 
	+ 读取Setting Bundle值
		+ NSUserDefault *defaults = NSUserDefault.standardUserDefaults();
		+ 取值	
			+ boolForKey
			+ floatForKey
			+ integerForKey
			+ objectForKey
			+ stringForKey
			+ doubleForKey
	+ 设置NSUserDefault属性
		+ [NSUserDefault setXX]
		+ [NSUserDefault synchronize]
+ **SettingBundle .plist默认值读取失败？**   


## 国际化
+ 文本信息国际化
	+ 系统按钮和信息国际化：`BuilderInterface PROJECT选择Localizations下面+，选择添加相应需要的国际化文件`  
	+ 应用名称国际化：`借助InfoPlist.strings文件进行配置`
		+ 创建InfoPlist.strings文件
		+ 打开其文件检查器，点击`Localized`按钮，添加相应语言系统
		+ 在不同语言.plist文件添加`CFBundleDisplayName="SQLite Demo" `用于显示应用名称
	+ 程序代码输出的静态文本国际化：`NSLocalizedString` 
	+ 使用工具`genstring`：genstrings [-a] [-q] [-o <outputDir>] sourcefile
+ xib和storyboard国际化
	+ Base国际化技术： `打开storyboard文件检查器，点击Localized按钮，添加相应语言系统`
		+ 根据`ObjectID`设置相应值 
+ 资源文件国际化
	+ 选中需要国际化的资源文件，打开文件检查器，点击Localized按钮，添加相应语言系统的资源文件
	+ 通过NSBundle获取对应语言系统资源路径
		+ `NSBundle *thisBundle = NSBundle.mainBundle();`
		+ `NSString *url = [thisBundle pathForResource:@"backgroud" ofType:@"aiff"];
`  

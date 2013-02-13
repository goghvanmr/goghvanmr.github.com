---
layout: post
title: "[日拱一卒]iOS 开发笔记"
description: ""
category: developer
tags: [iOS]
---
{% include JB/setup %}

##	原来 Foundation 框架自带有 Json 解析库, 

而且效率远高于 SBJson. 解析 Json 的语句为:

	NSDictionary *object = [NSJSONSerialization JSONObjectWithData:response options:NSJSONReadingAllowFragments error:nil];

##	通过 URL 下载图片生成 UIImage

	NSData *imageData = [NSData dataWithContentsOfURL:item.thumbnailURL];
    cell.thumbnail.image = [UIImage imageWithData:imageData];

需要注意的是, ```dataWithContentsOfURL``` 这个函数要阻塞线程, 所以最好不要放到主线程中.

##	NSObject 的 description 函数

重载这个函数, 可以达到自定义一个类的打印信息的功能.

##	NSUserDefaults

	NSUserDefaults * defaults = [NSUserDefaults standardUserDefaults];
	[defaults setValue:[NSNumber numberWithBool:YES] forKey:@"isLoggedIn"];
	[defaults setValue:self.email.text forKey:@"email"];
	[defaults setValue:self.password.text forKey:@"password"];

注意上面的代码中, ```[NSNumber numberWithBool:YES]``` 是因为, BOOL 型不能隐性的转换为 id 型, 而 setValue 的参数是 id. 所以将其显性地转换为 NSNumber. 提取这个值的时候, 只需要再转回 BOOL 型即可.

	NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
    BOOL isLoggedIn = [[defaults valueForKey:@"isLoggedIn"] boolValue];

##	如何根据条件来选择应用的入口?

例如, 如果用户之前没有登录, 应用启动时, 显示登录界面. 而如果用户之前已经登录了, 则显示主界面. 这个需要在 AppDelegate 中的 ```application: didFinishLaunchingWithOptions:``` 函数中加入条件选择.

	NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
    BOOL isLoggedIn = [[defaults valueForKey:@"isLoggedIn"] boolValue];
    
    NSString *segueId = isLoggedIn ? @"MainViewController" : @"LoginViewController";
    UIStoryboard *storyboard = [UIStoryboard storyboardWithName:@"MainStoryboard" bundle:nil];
    UIViewController *initViewController = [storyboard instantiateViewControllerWithIdentifier:segueId];
    
    self.window = [[UIWindow alloc] initWithFrame:[[UIScreen mainScreen] bounds]];
    self.window.rootViewController = initViewController;
    [self.window makeKeyAndVisible];
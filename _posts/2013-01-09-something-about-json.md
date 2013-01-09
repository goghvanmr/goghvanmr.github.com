---
layout: post
title: "[日拱一卒]关于JSON的三小点"
description: ""
category: developer
tags: [json, iOS, django]
---
{% include JB/setup %}

##	服务器应返回JSON而不是字符串

RESTful的Web应用, 客户端将用户名和密码发送给服务器端做鉴权, 服务器端应该给客户端如何答复呢? 之前我只是简单地返回一个字符串, 来表明登录是否成功. 但是更好的做法如下:

	{
    		"success": true,
    		"auth_token": "dfc7ad3884e7",
    		"login": "emailexample",
    		"email": "email@example.com"
	}
---

	{
    		"success": false,
    		"message": "Error with your login or password"
	}


##	Django如何返回JSON类型给客户端

	response_data['result'] = 'failed'
	response_data['message'] = 'You messed up'
	return HttpResponse(json.dumps(response_data), mimetype="application/json")

##	iOS如何解析JSON

使用名为**SBJSON**的第三方框架, 可以很简单的实现:

	SBJsonParser *parser= [[SBJsonParser alloc] init];
	NSDictionary *object = [parser objectWithString:response];
    
	NSLog(@"%@", [object objectForKey:@"message"]);
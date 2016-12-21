---
layout: post
title: "cocoa简洁写法笔记"
date: 2014-09-05 13:14
comments: true
categories: 
---

对cocoa的一些语法糖做的笔记
<!--more-->

### NSNumber
```ruby
NSNumber *totalNumber = [NSNumber numberWithInt:1];
to
NSNumber *totalNumber = @1;

## 更多拓展
NSNumber *floatNumber = @2.5f;
NSNumber *boolNumber = @YES;
NSNumber *totalNumber = @(5 * 6.5f);
```

### NSArray
```ruby
NSArray *members = [NSArray arrayWithObjects:@"father",@"mother",@"Jim",nil];
to
NSArray *members = @[@"father",@"mother",@"Jim"];

# 取值
NSString *username = [members objectAtIndex:2];
to
NSString *username = members[2];
```

### NSDictionary
```ruby
NSDictionary *personData = [NSDictionary dictionaryWithObjectsAndKeys:@"Jim",@"name",@"man",@"gender",nil];
to
NSDictionary *personData = @{@"name":@"Jim",
							 @"gender":@"man"};

# 取值
NSString *username = [personData objectForKey:@"name"];
to
NSString *username = person[@"name"];

# 设值和替换
[personData replaceObjectAtIndex:1 withOjbect:@"woman"];
[personData setObject:@"address" forKey:@"Beijing"];
to
person[1] = @"woman";
person[@"address"] = @"Beijing";		
							
```


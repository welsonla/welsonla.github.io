title: "为什么使用Mantle"
date: 2015-10-08 16:06:07
tags: iOS
---

项目地址: [https://github.com/Mantle/Mantle](https://github.com/Mantle/Mantle)

今年上半年在两个项目中都将Model层替换为Mantle，大大减少了开发中实体转换的时间;选择mantle的初衷是因为看到了大神的blog,里面的应用场景也是在开发中我们经常遇到的情况:
[iWangKe.me - 为什么唱吧iOS 6.0选择了Mantle](http://www.iwangke.me/2014/10/13/Why-Changba-iOS-choose-Mantle/)


## 对比一下
```json
# http://bubbler.labs.douban.com/j/user/wheats

{
  "homepage": "http://www.douban.com/people/wheats",
  "icon": "http://img3.douban.com/icon/u46721592-5.jpg",
  "userid": "46721592",
  "r": 0,
  "stats": {
    "board": 0,
    "bub": 0,
    "collect": 0
  },
  "title": "welsonla",
  "uid": "wheats"
}

```

![](http://ww1.sinaimg.cn/large/6e8de9dbjw1ewtvrr4eyjj20gp0eqjvh.jpg)

![](http://ww1.sinaimg.cn/large/6e8de9dbjw1ewtvsjo0s6j20go0f7whk.jpg)


## You should know:

- 使用Mantle需要继承MTLModel
- 如果需要将实体中的某个字段映射成一个实体或者实体的数组，需要继承MTLJSONSerializing
- Mantle需要一个字典来讲字典中的字段与实体的字段进行匹配

## 将JSON转换为制定的Model

```ruby
MDoubanUser *allModel = [MTLJSONAdapter modelOfClass:[MDoubanUser class] fromJSONDictionary:rstlDict] error:nil]
```
  
## 将JSON中的数组转换为Model的数组

```ruby
NSArray *users = [MTLJSONAdapter modelsOfClass:[MDoubanUser class] fromJSONArray:userArray error:nil];
```

  
## 将某个字段对应到某个实体
```ruby
+(NSValueTransformer *)JSONTransformerForKey:(NSString *)key{

  if ([key isEqualToString:@"stats"]) {
      #假设上诉到json中的stats创建了一个单独的实体类为MStats,
      return [MTLJSONAdapter dictionaryTransformerWithModelClass:[MStats class]];
  }else if([key isEqualToString:@"books"]){
      #假设中json中有一个books数组，并有对应的实体MBook
      return return [MTLJSONAdapter arrayTransformerWithModelClass:[MBook class]];;
  }
  return nil;
}
```

## 自定义转换
自定义转换只要定义一个字段名+JSONTransformer结尾的方法，就会执行我们自定义的转换,比如时间格式化，对某些字符进行一些操作处理

```ruby
# 将uid前面加上"Author"
+ (NSValueTransformer *)uidJSONTransformer{
    return [MTLValueTransformer transformerUsingForwardBlock:^id(NSString *uid, BOOL *success, NSError *__autoreleasing *error) {
        return [@"Author: " stringByAppendingString:uid];
    }];
}
```

## 多个字段对应
在项目中，经常遇到，接口A返回的用户id字段说uid,接口B返回的用户字段是ID，这种情况我们只需要中Model中将两个字段存到一个数组绑定到同一个属性上就可以了

```ruby
+ (NSDictionary *)JSONKeyPathsByPropertyKey
{
    return @{
		@"uid":@[@"uid",@"ID"],
		@"userid":@"userid",
		@"stats":@"stats",
		@"title":@"title",
		@"r":@"r",
		@"homepage":@"homepage",
		@"icon":@"icon"
    };
}
```


## 将实体中的值封装成一个dictionary，方便接口传输

```ruby
#使用全部的字段
NSDictionary *params = [user dictionaryValue];

#使用部分的字段
NSDictionary *params = [address dictionaryWithValuesForKeys:@[@"uid",@"stats",@"homepage"]];
```

## 最后

在项目的开发过程中，我抽时间做了一个小工具，可以方便的将JSON转换为Mantle支持的Model类，希望对你们有帮助

Source: https://github.com/TimeBots/ModelBot
Download: [ModelBot Download](https://github.com/TimeBots/ModelBot/releases/download/0.3.0/ModelBot.0.3.0.zip)
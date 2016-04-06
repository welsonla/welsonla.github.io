title: 从Objective-c迁移到Swift的一些坑
comment: true
date: 2016-01-27 15:08:49
categories:
---

### NSString to String
```swift
#ObjC
NSString *notice

#Swift
var notice:String?
```

### NSArray,NSMutableArray to Array

```swift
#1. 声明
#ObjC
NSMutableArray *listArray = [NSMutableArray array];

#Swift
var listArray:[String] = Array() //必须带参数类型
var listArray:[AnyObject] = Array()

#2. 增加元素
#ObjC
[listArray addObject:@"foo"];

#Swift
listArray.append("foo")
```

### NSRange->Range
```swift
#ObjC
NSRange range = NSMakeRange(0,10)

#Swift
Range(start: 0, end: 10)

```

# NSDictionary,NSmutableDictionary  to Dictionary
```swift
#ObjC
NSMutableDictionary *score = [NSMutableDictionary dictionary];

#Swift
var score0:[String:String]?
var score1 = [String:String]()
var score2 = Dictionary<String,String>()
var score3 = [:]

#ObjC
NSDictionary *person = @{@"name":@"Single Dog",@"Skill":@"Swift"};
person[@“age”] = @“28”;

#Swift
var person = ["name":"Single Dog","Skill":"Swift"]
person["age"] = "28"
```

### Random

```swift
#ObjC
arc4random%255

#Swift
arc4random_uniform(255)
random() % 255
```

### Selector
感觉Selector的方式不如ObjC那样有方法提示，容易写错，效率反而不如之前
```swift
#ObjC
SEL callback = @selector(uploadCallback:)

#Swift
Selector("uploadCallback:")
```

### id to AnyObject
```swift
#ObjC
id sender

#Swift
var sender:Anyobject?
```  
### 三元运算缩写
```swift
#ObjC
a ? : b

#Swift
a ?? b
```

### 枚举
```swift
#ObjC
typedef NS_ENUM(NSInteger,LocationState){
    LocationStateStart,
    LocationStateFinish,
    LocationStateFail
};

#Swift
enum LocationState {
    case LocationStart, LocationFinish, LocationFail
}
```

# Todo List
1. Block to Closure
2. DateFormatter
3. nil value check
……

遇到继续添加,未完待续……

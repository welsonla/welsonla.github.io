title: 关于Xcode单元测试(XCTest)的一些总结
date: 2015-05-04 10:58:17
categories: something
---

单元测试可以让我们快速检测项目接口与一些功能的可用性，这次编写了大量的单元测试，让我对之前的一些疑惑有了一个透彻的理解

- 单元测试中，可以直接import我们项目中的类
- 想要执行的方法，必须使用test开头，testLogin会被执行，userLogin这样的方法名不会被执行
- 单元测试没有头文件，一些变量声明，写在interface里面
- 对于一些变量的初始化，放到setup里面进行

##一个简单的单元测试类
#####创建单元测试类
![](http://ww1.sinaimg.cn/large/6e8de9dbgw1ers0n47wtrj20ka0bygnf.jpg)

####一个简单的类
```ruby
#import <UIKit/UIKit.h>
#import <XCTest/XCTest.h>
#import "LoginService.h" //引入自定义的类

@interface HelloTest : XCTestCase
{
	//变量声明		
    NSInteger count;
    LoginService *loginService;
}

@end

@implementation HelloTest

- (void)setUp {
    [super setUp];
    
    //初始化
    count = 5;
    
    loginService = [[LoginService alloc] init];

}

- (void)tearDown {

    [super tearDown];
}

- (void)testCount
{
    XCTAssertEqual(count, 6,@"count不等于6,count的值为:%ld",(long)count);
}

- (void)testExample {

    XCTAssert(YES, @"Pass");
}

- (void)testPerformanceExample {

    [self measureBlock:^{

    }];
}

@end
```

**cmd+U** 进行执行后会提示我们如下错误,测试通过的方法，会有绿色对号，失败的方法会显示我们写的错误提示
![](http://ww1.sinaimg.cn/large/6e8de9dbgw1ers0vuinl5j20p405jq49.jpg)

##XCTest的测试方法大都类似

####XCTAssertGreaterThan
```ruby
#判断count是否大于8
XCTAssertGreaterThan(count, 8,@"count is not greater than 8");
```
####XCTAssertNotEqual
```ruby
#判断是否不相等
XCTAssertNotEqual(count, 5,@"they are equal");
```

####XCTAssertTrue
```ruby
#判断某个表达式是否成立
XCTAssertTrue(count>3,@"count greater than 3");
```
运行结果
![](http://ww4.sinaimg.cn/large/6e8de9dbgw1ers16kf52bj210v04jn03.jpg)


##对于异步方法的测试(Asynchronous Testing)
对于block等异步方式执行的方法，在测试的时候，我们要使用，一般的做法都是延迟，**等待block执行完毕再进行检查**

#####主要步骤
- 声明一个XCTestExpectation
- 在block中使用fulfill抛出错误
- waitForExpectationsWithTimeout进行一个延迟时间设定


```ruby
#import <XCTest/XCTestCase+AsynchronousTesting.h>
```

比如上面的loginService

```ruby   
- (void)testLogin
{
	##声明一个Exception
    XCTestExpectation *loginException = [self expectationWithDescription:@"loginError"];

    [loginService sendLoginWithMobile:TEST_MOBILE andCode:TEST_CODE onComplete:^(NSDictionary *jsonDict, NSString *jsonString) {
        MStatus *status = [loginService convertToMStatus:jsonDict];
        XCTAssertEqual(status.returncode, 0, @"login error");
        
        //抛出错误
        [loginException fulfill];
    } onFailure:^(NSString *msg) {
        XCTFail(@"login error:%@",msg);
        
        //抛出错误
        [loginException fulfill];
    }];
    
    //延迟两秒执行
    [self waitForExpectationsWithTimeout:2 handler:^(NSError *error) {
        XCTFail(@"time out:%@",error);
    }];
}
```

---
layout: post
title: "different of class and category"
date: 2013-05-10 01:05
comments: true
categories: 
---


当需要重写父类中的方法时，这时候定义子类


```ruby
@interface JADanSideController : JASidePanelController


@end


@implementation JADanSideController

- (UIBarButtonItem *)leftButtonForCenterPanel{
    
    UIButton *leftBarButton = [UIButton buttonWithType:UIButtonTypeCustom];
    [leftBarButton setFrame:CGRectMake(0, 0, 44, 30)];
    [leftBarButton setBackgroundImage:[UIImage imageNamed:@"List_NaviSide.png"] forState:UIControlStateNormal];
    [leftBarButton addTarget:self action:@selector(toggleLeftPanel:) forControlEvents:UIControlEventTouchUpInside];
    __autoreleasing UIBarButtonItem *leftBarButtonItem = [[UIBarButtonItem alloc] initWithCustomView:leftBarButton];

    return leftBarButtonItem;
}

@end

```

当需要为父类添加方法时，这时候定义类别


```ruby
@interface JADanSideController : JASidePanelController

- (void)setBackGroundColor;

@end

```
# TColorfulTabBar

彩色的TabBar，加平滑的切换动画

## 设计图

![](./README-IMAGES/ColorfulTabBarDesign.gif)

## 效果展示

![](./README-IMAGES/result.gif)

## 相关库

这个Demo中引入了`TKit`这个库，它的作用只是为了显示16进制的颜色。如果不需要，可以删除，然后将颜色换成自己的就行。

## 视图层级

这个效果的实现是通过重写TabBar，然后给TabBar添加了一个彩色view(`colorView`)实现的。

视图层级如下：

![](./README-IMAGES/ViewHierarchy.png)

在`UITabBarController`中，将系统的`UITabBar`替换成`TColorfulTabBar`即可。(<font color = red>注：tabBarController.tabbar属性是readonly修饰的，所以要通过KVC来修改</font>)

代码如下：

```objc
TColorfulTabBar *tabBar = [[TColorfulTabBar alloc] initWithFrame:tabBarController.tabBar.frame];
[tabBarController setValue:tabBar forKey:@"tabBar"];
```

## 自定义

Demo相关配置在`TColorfulTabBar+Configuration`这个类目当中，可以修改每个item的颜色与item的个数。

```objc
// item的颜色（个数要和item的个数相同）
- (NSArray *)itemColors;

// item的个数
- (NSInteger)itemCount;
```

## 技术支持

[http://www.brighttj.com/ios/ios-colorful-tabbar-implement.html](http://www.brighttj.com/ios/ios-colorful-tabbar-implement.html)

## 可能出现的问题

因为当`TColorfulTabBar`加载到父视图上时，我让`TColorfulTabBar`响应了自己的代理方法，所以如果在`UITabBarController `中再次修改`delegate `，可能会导致`TColorfulTabBar`无法拿到下标。

如果没有修改代理，那有可能会导致`UITabBarController`中的`UITabBarDelegate`无效。
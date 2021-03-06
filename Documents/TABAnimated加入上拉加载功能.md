## TABAnimated加入上拉加载功能

## 前言
本文说明TABAnimated 2.4.0的上拉加载功能

## 基本原理
在原理上没有什么新意，和普通的上拉加载原理一致，基于KVO监听UIScrollView的contentOffSet和contentInset。  
不过，在展示上不再是传统的loading，而是骨架图。  
并且这个骨架图是基于TABAnimated内部的骨架屏生产流程进行制作的，共享缓存、复用池、配置信息、调整回调。

## 效果图

![image.png](https://upload-images.jianshu.io/upload_images/5632003-3f0a066cfd86a4b4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 使用方式

block形式

```
[_tableView tab_addPullLoadingActionHandler:^{
	 // 开发者在此处进行数据请求
	 // 模拟数据请求
	 [self performSelector:@selector(loadMoreData) withObject:nil afterDelay:0.5];
}];
```
block形式绑定class、height

```
[_tableView tab_addPullLoadingClass:TestTableViewCell.class viewHeight:100 actionHandler:^{
	// 开发者在此处进行数据请求
	// 模拟数据请求
	[self performSelector:@selector(loadMoreData) withObject:nil afterDelay:0.5];
}];
```

消息传递形式

```
- (void)tab_addPullLoadinTarget:(id)target selector:(SEL)selector;
- (void)tab_addPullLoadingClass:(nonnull Class)pullLoadingClass viewHeight:(CGFloat)viewHeight target:(id)target selector:(SEL)selector;
```

停止刷新

```
- (void)tab_stopPullLoading;
```

永远停止刷新

```
- (void)tab_stopPullLoadingNoMoreData;
```




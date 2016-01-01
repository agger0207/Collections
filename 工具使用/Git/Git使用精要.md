# Git 使用精要

## 1 Pull Request

多人合作时，使用Pull Request进行Merge会更好跟踪，并且可以结合任务管理系统以及Code Review; 选择添加注释后拒绝或者Merge Pull Request.

分支上有新的提交后，可以直接在"branch"中看到新的pull request.

## 2 Git Sub Module的使用

可以参照

https://github.com/gaosboy/iOSSF

里面对GitSubModule的使用；

也可以参照https://github.com/Mantle/Mantle 或者https://github.com/octokit/octokit.objc的说明

或者其他开源工程里面的script/bootstrap
通常情况下，bootstrap是为了调用或者配置git submodules

常见的操作示例如下：
### 在项目中添加Submodule
git submodule add git@github.com:jjz/pod-library.git pod-library

例如，添加Mantle:

	git submodule add git@github.com:Mantle/Mantle Mantle

但是，如果ssh被封掉了，那么可以用下面的命令，也是一样的.
	
	git submodule add https://github.com/Mantle/Mantle Mantle
	
正常情况下，如果没有额外的需要，那么就不需要任何处理了；只需要将这个工程拖到自己的工程或者work space中去即可；如果有额外的需要，例如	

添加YTKNetwork:

	git submodule add https://github.com/yuantiku/YTKNetwork YTKNetwork

### 使用.gitmodules来初始化Submodule
参照“https://github.com/gaosboy/iOSSF”弄个.gitmodules文件管理所有的submodules;
然后用命令
	
	git submodule init

来初始化并且使用
	
	git submodule update
	
来更新submodule.

## Git Submodule基本使用流程总结

以YTKNetwork为例，
### 1 添加submodule到自己的仓库

	git submodule add https://github.com/yuantiku/YTKNetwork YTKNetwork
	
这个命令也就是其他开源库所说的，“Add the Mantle repository as a submodule of your application's repository.”	
	
### 2 拖动到自己的工程目录或者workspace中去
通常情况下就不需要再额外建立workspace了.

### 3 需要更新时调用下面命令进行更新
git submodule update

### 关于.gitmodules的使用

可以参考
https://github.com/gaosboy/iOSSF

submodules添加了以后，会生成一个.gitmodules文件；那么每次从git上clone工程下来的时候，都需要重新调用`git submodule init`方法以及`git submodule update`方法来重新获取到具体的内容

### 注意，部分Framework需要添加到'Embedded Binaries'

可以参考
http://www.cocoachina.com/ios/20141126/10322.html

另外，在Mantle的git中提到过，存在这样的bug [Can't add cross-project iOS Embedded Binaries in a Workspace environment](http://www.openradar.appspot.com/19676555), 不清楚Xcode 7中是否解决了这个问题.

总的来说，如果只是简单的用一个两个库，那么submodule还好，但是如果同时使用多个，而且直接进行工程依赖，那么明显Cocoapods更强大.

附注：[Git Submodule的坑](http://blog.devtang.com/blog/2013/05/08/git-submodule-issues/)


## Gitsubmodule与CocoaPods的结合使用

问题描述：库A以Pods的方式提供，但是里面依赖了B; 而B以submodule的方式提供.

解决方案：
在PodsSpec中无法解决这个依赖问题，但是可以在Pods文件中解决. 例如

	pod 'AggerLib', :git => 'https://github.com/git/agger/AggerLib.git', :branch => 'master', :submodules => true

也就是要加上 :submodule => true


原文：
	
	I’ve been banging my head against a brick wall for a few hours now on this, so I thought I’d post this for the benefit of anybody else searching:
	
	If you are using the wonderful Cocoapods in an iOS project you’re developing, and you make one of your Pods load directly from a Git repository (perhaps GitHub) then there’s a little gotcha to be aware of: if the Podspec includes :submodules => true in the source section then it is necessary to manually add that to your Podfile too.
	
	In my case, I’m hacking on my own version of the Bypass-ios Pod, so I had tried adding this line to my Podfile:
	pod 'Bypass', :git => "git@github.com:andygeers/bypass-ios.git"
	
	However, that was missing a few files from a submodule, causing compile errors like this:
	'element.h' file not found
	
	It feels a bit cumbersome, but instead it is necessary to write the Podfile like this:
	pod 'Bypass', :git => "git@github.com:andygeers/bypass-ios.git", :submodules => true
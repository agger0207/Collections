# Gitsubmodule与CocoaPods的结合使用

## 遇到的问题
A以Pods的方式提供，但是里面依赖了B; 而B以submodule的方式提供.


Git submodule与CocoaPods可能不好结合使用；因为实际的仓库中是没有submodule的文件的

周三尝试了一下，无法成功...

不过这里面有一篇文章解释这个问题：

[USING SUBMODULES IN COCOAPODS SOURCED FROM GIT](http://www.geero.net/2014/06/using-submodules-in-cocoapods-sourced-from-git/)
http://www.geero.net/2014/06/using-submodules-in-cocoapods-sourced-from-git/

值得记下来:

## 解决方案

	pod 'AggerLib', :git => 'https://github.com/git/agger/AggerLib.git', :branch => 'master', :submodules => true

也就是要加上 :submodule => true

不过要求对指定git的权限；否则也无法获取到.
(那么到时候和他们商量一下，看他们愿意以那种方式来做)

原文：
	
	I’ve been banging my head against a brick wall for a few hours now on this, so I thought I’d post this for the benefit of anybody else searching:
	
	If you are using the wonderful Cocoapods in an iOS project you’re developing, and you make one of your Pods load directly from a Git repository (perhaps GitHub) then there’s a little gotcha to be aware of: if the Podspec includes :submodules => true in the source section then it is necessary to manually add that to your Podfile too.
	
	In my case, I’m hacking on my own version of the Bypass-ios Pod, so I had tried adding this line to my Podfile:
	pod 'Bypass', :git => "git@github.com:andygeers/bypass-ios.git"
	
	However, that was missing a few files from a submodule, causing compile errors like this:
	'element.h' file not found
	
	It feels a bit cumbersome, but instead it is necessary to write the Podfile like this:
	pod 'Bypass', :git => "git@github.com:andygeers/bypass-ios.git", :submodules => true
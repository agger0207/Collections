# Cocoapo技巧


pod list | grep AFNetworking  查看本地库列表


podspec文件存放在 ~/.cocoapods下面
这是一个文件夹，下面依次是repos->master->Specs

Specs下就是各个库的

可以从中找出AFNetworking来

ls | grep AFNetworking

然后可以把这个文件夹拷贝出来看看；里面有不同的版本号，然后每个版本号对应的文件夹下面都有一个AFNetworking.podspec.json文件
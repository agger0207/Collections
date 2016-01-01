# Github不显示Contributions的问题

上次重做了系统后，自己的Commit上不能正确显示Contributions.\

需要设置email为username@users.noreply.github.com。

参见：

https://gist.github.com/suziewong/4378434

如果有多个不同的email, 那么可以在保持全局的基础上调用如下命令:

git config --local user.email "username@users.noreply.github.com"

其中，username替换成为自己的名字.

来设置当前Repo的email, 然后这样就可以看到Contributions了.
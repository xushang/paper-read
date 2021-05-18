
常用git指令
#1 push：该单词直译过来就是“推”的意思，如果我们本地的代码有了更新，为了保持本地与远程的代码同步，我们就需要把本地的代码推到远程的仓库，代码示例：
git push origin master

#2 pull：该单词直译过来就是“拉”的意思，如果我们远程仓库的代码有了更新，同样为了保持本地与远程的代码同步，我们就需要把远程的代码拉到本地，代码示例：
git pull origin master

参考文档
【超详细图文过程】如何使用Git和Github来管理自己的代码？ - 张屿儿的文章 - 知乎
https://zhuanlan.zhihu.com/p/23167699

还不会使用 GitHub ？ GitHub 教程来了！万字图文详解 - GitHubPorn的文章 - 知乎
https://zhuanlan.zhihu.com/p/369486197

#3 
用Git 下载主干上的代码时报错:
翻译成中文:因为没有合并文件，拖动是不可能的。因为一个未解决的冲突而退出。

分析
看输出的错误日志,很明显本地有代码与主干代码冲突,导致pull失败。
所以commit—push 但是点击commit弹出提示框“没有可提交的内容”证明我本地代码没有任何的更改，有一个最笨的方法，就是把本地代码稍作修改，然后commit—push，果然提交成功了，然后push，还是失败。

再分析
在git pull的过程中，如果有冲突，那么除了冲突的文件之外，其它的文件都会做为staged区的文件保存起来。
本地的push和merge会形成MERGE-HEAD(FETCH-HEAD), HEAD（PUSH-HEAD）这样的引用。HEAD代表本地最近成功push后形成的引用。MERGE-HEAD表示成功pull后形成的引用。可以通过MERGE-HEAD或者HEAD来实现类型与svn revet的效果。
将本地的冲突文件冲掉，不仅需要reset到MERGE-HEAD或者HEAD,还需要–hard。没有后面的hard，不会冲掉本地工作区。只会冲掉stage区。
git reset –hard FETCH_HEAD
————————————————
版权声明：本文为CSDN博主「柠檬草。」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/yyx3214/article/details/81261733

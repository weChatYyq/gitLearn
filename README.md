# gitLearn
git 学习记录

## Git忽略提交
场景
---
在使用Git的过程中，我们喜欢有的文件比如日志，临时文件，编译的中间文件等不要提交到代码仓库，这时就要设置相应的忽略规则，来忽略这些文件的提交。

方法
--
- 在Git项目中定义 .gitignore 文件
这种方式通过在项目的某个文件夹下定义 .gitignore 文件，在该文件中定义相应的忽略规则，来管理当前文件夹下的文件的Git提交行为。
.gitignore 文件是可以提交到共有仓库中，这就为该项目下的所有开发者都共享一套定义好的忽略规则。
在 .gitingore 文件中，遵循相应的语法，在每一行指定一个忽略规则。如： 
```cmd
  *.log
  *.temp
  /vendor
```
- 在Git项目的设置中指定排除文件
这种方式只是临时指定该项目的行为，需要编辑当前项目下的 .git/info/exclude 文件，然后将需要忽略提交的文件写入其中。
需要注意的是，这种方式指定的忽略文件的根目录是项目根目录。
- 定义Git全局的 .gitignore 文件
除了可以在项目中定义 .gitignore 文件外，还可以设置全局的 git .gitignore 文件来管理所有Git项目的行为。这种方式在不同的项目开发者之间是不共享的，是属于项目之上Git应用级别的行为。

这种方式也需要创建相应的 .gitignore 文件，可以放在任意位置。然后在使用以下命令配置Git：
```cmd
git config --global core.excludesfile ~/.gitignore
``` 

忽略规则
--
以斜杠“/”开头表示目录；
以星号“*”通配多个字符；
以问号“?”通配单个字符
以方括号“[]”包含单个字符的匹配列表；
以叹号“!”表示不忽略(跟踪)匹配到的文件或目录。
注意： git 对于 .gitignore配置文件是按行从上到下进行规则匹配的
/mtk 过滤整个文件夹
*.zip 过滤所有.zip文件
/mtk/do.c 过滤某个具体文件
!/mtk/one.txt 追踪（不过滤）某个具体文件

在 .gitignore 文件中，每一行的忽略规则的语法如下：

空格不匹配任意文件，可作为分隔符，可用反斜杠转义
# 开头的模式标识注释，可以使用反斜杠进行转义
! 开头的模式标识否定，该文件将会再次被包含，如果排除了该文件的父级目录，则使用 ! 也不会再次被包含。可以使用反斜杠进行转义
/ 结束的模式只匹配文件夹以及在该文件夹路径下的内容，但是不匹配该文件
/ 开始的模式匹配项目跟目录
如果一个模式不包含斜杠，则它匹配相对于当前 .gitignore 文件路径的内容，如果该模式不在 .gitignore 文件中，则相对于项目根目录
**匹配多级目录，可在开始，中间，结束
?通用匹配单个字符
[]通用匹配单个字符列表 
详细的忽略规则可以参考[官方英文文档](https://git-scm.com/docs/gitignore)

常用匹配示例
--
bin/: 忽略当前路径下的bin文件夹，该文件夹下的所有内容都会被忽略，不忽略 bin 文件
/bin: 忽略根目录下的bin文件
/*.c: 忽略 cat.c，不忽略 build/cat.c
debug/*.obj: 忽略 debug/io.obj，不忽略 debug/common/io.obj 和 tools/debug/io.obj
**/foo: 忽略/foo, a/foo, a/b/foo等
a/**/b: 忽略a/b, a/x/b, a/x/y/b等
!/bin/run.sh: 不忽略 bin 目录下的 run.sh 文件
*.log: 忽略所有 .log 文件
config.php: 忽略当前路径的 config.php 文件


Git 忽略规则优先级
--
在 .gitingore 文件中，每一行指定一个忽略规则，Git 检查忽略规则的时候有多个来源，它的优先级如下（由高到低）：
- 从命令行中读取可用的忽略规则
- 当前目录定义的规则
- 父级目录定义的规则，依次地推
- $GIT_DIR/info/exclude 文件中定义的规则
- core.excludesfile中定义的全局规则 

tip
--
如果你创建.gitignore文件之前就push了某一文件，那么即使你在.gitignore文件中写入过滤该文件的规则，该规则也不会起作用，git仍然会对该文件进行版本管理。
.gitignore只能忽略那些原来没有被track的文件，如果某些文件已经被纳入了版本管理中，则修改.gitignore是无效的

解决办法：
  待定






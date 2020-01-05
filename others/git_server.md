##### git add
1. 文件名字
2. * 通配符
3. 多个文件名字,用空格隔开
4. add一个文件夹
4. . 指代当前文件夹
5. git add命令会更新索引

##### git配置文件
1. .git 子文件夹里边的config文件, 具有最高的优先权(只对所在的文档库有效)
2. 登录账号的 home directory中的 .gitconfig文件(只对登录用户有效)
3. Git程序的安装文件夹中的etc\gitconfig文件(对所有账号和所有git文档库都有效)
###### git config的用法
1. git config -l 显示当前的设置值
2. git config user.name 'abc' (记录在文档库的配置文件)
3. git config --global user.name 'aaa' (记录在登录账号的 home directory中.config文件内)
4. git config --system user.name 'aaa' (记录在Git安装文件夹中的 etc\gitconfig文件内)
5. git config --unset user.name (删除配置,添加--global --system删除对应配置位置)
6. git config alias.指令别名 '正式的指令和选项'
7. git config --unset alias.指令别名  (删除自定义指令)
8. git config --global core.editor notepad (修改默认的commit message 编辑器)
##### git diff
1. @@ 开头的部分是文件的差异
2. @@后面的两个数字"-1,3"  -表示a文件,1,3 值得是a文件中第一行开始的后面3行, + 表示b文件
3. 下一行用 - 开头表示a文件变成b文件的时候,这一行被删除
4. 下一行用 + 开头表示a文件变成b文件的时候,这一行被加入
5. 没有+-开头表示没有修改
##### 控制Commit
1. git rm 文件名 : 1.文件必须在git 索引中,且没有修改.以下情况不能删除 (只能删除git中没有变化过的文件,标记为delete, commit之后才真的删除)
    1. untrack的文件
    2. track的,同时修改过
    3. 新文件,git add进去的
2. git rm --cached 文件名
    1. git索引中的这个文件会被删除,同时从tracked变成untracked(最大区别是,没有在文件夹中删除文件)
3. git reset HEAD
4. git tag 自定义标签名称  节点标识符或者标签     git tag -d xxx (删除)

##### git merge
1. 打开冲突文件,删除冲突标识符. 然后 add commit
1. git cherry-pick 是合并commit节点到分支
git checkout
- undo changes，重置文件状态，对没有被track的文件没有作用

git clean -d
- undo changes， 只对没被track的文件起作用
- -d 代表directory，包含directory
- -f 代表force

git revert
- commit 一次抵消 上次commit 的操作
- git revert jhb124bh2l14b214kj2b 的意思是revert某个commit,注意dependency

git reset HEAD~1
- 直接回滚，删除commit记录
- git reset HEAD~1 回滚到head的前一个
- git reset HEAD~2 回滚到head的前两git个


git show fjp928h1f0h12nfunu134f-
- 把某次commit的改动显示
- 

git commit --amend -m 'added git notes'
- 修改commit的message

git log
- --graph
- --oneline
- --all 本地和remote都显示

git branch ```<branchname>```
- 创建分支，但在不会自动跳到新的branch
- git branch -d 删除没有改动的branch
- git branch -D 强制删除
- branch命名法：
  ```<type>/<ticket#>-<title>```
  eg. feat/JR-101-create0header-for-home-page

  - type: 
    - feat,feature
    - fix/bugfix/hotfix
    - chore(提升代码质量，改动用户看不见)

git checkout ``` <branchname>```
- 切换分支
- git checkout -b ```<branchname>``` 相当于 git branch ```<branchname> ```git checkout 也就是创建分支，然后切换到该分支

git merge ```<branch name>```
- 在被插入的branch，把b并进a
-




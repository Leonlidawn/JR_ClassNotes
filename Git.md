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

git branch
- 显示分支
- git branch -a 会显示所有（包括remote tracking branch）分支
- git branch ```<branchname>``` 创建分支，但在不会自动跳到新的branch
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
- 把指定的branch并入当前的branch， 
- 一般有conflict的话需要进行以下操作：
  - 3 way merge：互相都有不同更新
    - resolve conflict后 git add 文件
    - git merge --continue
  - fastforward merge: 另外的branch更新了，且之前原有代码没有不同
    - catch up merge, 直接把更新的内容merge到当前的branch。

git rebase ```<branchname|commit>```
- 把指定的点的新的改动都插入到当前branch的改动前面。 好处是：conflict可以自己在自己的branch先搞定，然后再在对方放那个branch merge一个fast forward merge了。




git clone
- 复制repo到本地
- git clone ```ssh 链接```


tracking branch的概念
- tracking branch 是一个本地的与remote有直接联系的分支, caches remote info,  the branch it tracks is called an “upstream branch”（upstream branch通常命名方式是```<remote>/<branch> eg.orgin/master```.  git就是在把远端branch同步到tracking branch然后把你local working branch与它比较的。
- tracking branch 只有在clone, fetch, pull 和 push的时候会被更新。
-  clone的时候会自动在本地创建tracking branch。 （checkout branch如果指定的branch只存在于远端的话也会创建）
  - 如果remote不是通过git clone加入的，而是git remote add ```<remote><url>```加入的，需要手动set remote tracking branch
- 如果没有设置remote tracking branch, fetch pull push 不能没有参数， 因为都不知道从哪个remote执行
  - 此时有两种途径解决：
    - 每次explicitly 指定 remote
      ```git pull <remote><branch>   ```
         eg.
      ```git pull origin/master```
    - 定义upstream
      - ```git branch --set-upstream-to= <remote><branch> <localbranch> ``` 
          eg.
        ```git branch --set-upstream-to=origin/master master ```
      或者
      - ```git branch -u origin/master```  
      - 省略localbranch的话就是指定当前branch
     
  
git remote
- 显示远端名字
- -v 显示详细链接信息， fetch 和 push的位置
- git remote rm ```<远端名字>```  会删除链接
- git remote add ```<远端名字（只用于本地显示）>  <远端以.git结尾的url>```   会添加origin
- git remote rename ```<oldname> <newname>``` 会改远端名字

git fetch
- 把remote的更新记录取下来， 通常会在之后merge一下。 origin/master


git pull
- 从远端同步东西下来，等同于
 ```
  git fetch <remote> 
  git merge origin/<current-branch>.
 ```

git push
- 把local的东西同步到远端
- ```git push -u <远端名字> <branch>``` 这里默认branch的名字是在本地和远端是相同的。
- ```git push <远端名字> <local branch>: <不相同名字的remote branch>``` 这个如果remobranch是新的，也会在本地创建新的branch,但这个不会把新branch放进的push的设置里面。
- 删除remote branch
  - git push -d ```<远端名字> <branch> ```
  - git push ```<远端名字>:<branch> ``` 这个等于push一个空的local branch上去，因为没有指定local branch. 然后远端就自动删除那个空的branch了
  

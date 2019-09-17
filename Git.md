undo changes:
git checkout
- 对没有被track的文件没有作用

git clean -d
- 只对没被track的文件起作用
- -d 代表directory，包含directory
- -f 代表force

git revert
- commit 一次抵消 上次commit 的操作
- git revert jhb124bh2l14b214kj2b 的意思是revert某个commit,注意dependency

git show fjp928h1f0h12nfunu134f-
- 把某次commit的改动显示
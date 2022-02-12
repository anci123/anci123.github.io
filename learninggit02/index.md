# LearningGit02

# git - branch 分支
<!--more-->

## 開始使用
- 列出分支  
`git branch`
    ```
    $ git branch
    * main
    branch-1
    meo
    ```
   - `*` 代表當前所在的分支
- 新增分支  
    `git branch BRANCH_NAME`
- 改變分支名稱  
    `git branch -m OLD_NAME NEW_NAME`
- 刪除分支  
    `git branch -d BRANCH`  
    如果要刪的分支還沒有被合併，則會出現error  
    - 這時可以使用強制刪除
        `git branch -D BRANCH`
- 切換分支  
`git checkout DIR_BRANCH`
    - `git checkout -b DIR_BRANCH`  
    如果有該分支，則直接切換；若沒有該分支，則git會先建立該分支再切換過去


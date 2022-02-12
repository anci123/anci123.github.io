---
title: "LearningGit01"
date: 2022-02-11T16:03:20+08:00
tags: ["git"]
categories: ["git"]
draft: false
---
# git - 安裝、初始設定及操作
<!--more-->
## 安裝
- 安裝指令  
`sudo apt-get install git`
- GUL工具  
`sufo apt-get install gitk`
## 初始設定
### 使用者設定
- 設定使用者名稱  
`git config --global user.name "USER_NAME"`
- 設定使用者信箱  
`git config --global user.email "USER_EMAIL"`
- 檢視使用者設定  
    1. `git config --list`
    2. `vim ~./gitconfig`
- 為特定專案設定使用者: 使用`--local`參數  
`git config --local user.name "USER_NAME"`  
`git config --local user.email "USER_EMAIL"`
### 其他設定
- 設定預設編輯器，將雙引號中的文字替換成你想用的文字編輯器即可  
`git config --global core.editor "vim"`
    - 設定完成之後也可以到`~/.gitconfig` 確認
- 設定縮寫，視個人情況而定  
    `git config --global alias.st status`  
    `git config --global alias.co checkout`  
    `git config --global alias.br branch`  
    `git config --global alias.l "log --oneline --graph"`
    `git config --global alias.ls 'log --graph --pretty=format:"%h <%an> %ar %s"'`
- 記住帳號密碼，這樣就不用每次push都要打帳密啦~  
`git config --global credential.helper store`
    - 修改: 直接去`~/.git-credential`修改  
    之後將cache daemon 退出  
    `git credential-cache exit`

## 基本操作
- `git init`: 初始化當前目錄，開始進行版控~(產生.git 目錄)
- `git status` : 查詢當前狀態(commit 前查看狀態)
- `git add`: 將檔案加入暫存區(commit 前 add)
    - `add --all`，`add .`
    - `add 資料夾`
    - `add 檔案`
- `git commit`: 儲存異動
    - 不加任何參數: 直接開啟預設文字編輯器，可在其編輯commit訊息
    - 直接加上commit message  
    `git commit -m "change abc.md"`  
    `-m` :後面加上這次有什麼變動的描述  
    - 沒有東西也可以commit XDD  
    `git commit --allow-empty`
    - add、commit一起搞定  
    `git commit -a -m "update content"`  
    不過對於`Untrack file`無效，所以如果有新增檔案或資料夾，務必add 完再commit
- `git log`: 檢視git紀錄
    - 讓輸出更精簡  
    `git log --oneline`  
    `git -oneline --graph`
    - 找 "manto" 這個人的commit  
    `git log --author="manto"`
    - 找兩個人的commit  
    `git log --oneline --author="USER_1\|USER_2"`
    - `git log --grep="add"`: 找commit massage 中符合該字串的訊息
    - `git log -S "FILE"`: 找commit 的內容中有符合該訊息的內容
    - 查詢特定時段的紀錄  
    `git log --oneline --since="9am" --until "12am"`  
    `git log --oneline --since="9am" --until "12am" --after="2020-07"`
    - 檢視特定檔案修改紀錄  
    `git log FILE`  
    查看詳細修改的內容  
    `git log -p FILE` 
- `git blame`: 查看某一行程式是誰寫的
    - 查看該檔案每一行各是誰寫的  
    `git blame FILE`
    - 查看特定行數  
    `git blame -L 5,10 FILE`
-  `git checkout`: 恢復被刪除的檔案
    - `git checkout DELETED_FILE`
    - 一次恢復所有被刪除的檔案  
    `git checkout .`
    - 用其他的版本來覆蓋被刪除的檔案  
    `git checkout HEAD~2 FILE`  
    `git checkout HEAD~2 .`  
    => 拿距離現在兩個版本以前的檔案來覆
    蓋
- `git reset`
    ```
    $ git log --oneline
    a305dd7 (HEAD -> main, origin/main) add heml01.md
    459aebc change name to index.en.md
    c92177f add .en to picture name
    8f1b6d5 change jpg to png
    ```
    -  相對做法  
    `git reset a305dd7^`  
        `git reset master^`  
        `git reset HEAD^`  
        以上都是回復到前一個commit 紀錄的意思
        - `^` 是前一個，`^^` 是前兩個，以此類推
        - `git reset master~5`
            則是倒退到前五個的意思
    - 絕對作法
    `git reset 459aebc`  
    代表回復到`459aebc`這一版的意思  
    =>
        ```
        $ git log --oneline
        459aebc (HEAD -> main, origin/main) change name to index.en.md
        c92177f add .en to picture name
        8f1b6d5 change jpg to png
        ```
    - 回復reset掉的commit  
    `git reset a305dd7 --hard`  
    其實那些被reset刪除的commit 並沒有消失，還是可以還原的
    - 查看所有紀錄，包括reset紀錄  
    `git reflog`
    - 三個模式
        - `--mixed` 只有暫存區會變動，檔案不會變動
        - `--soft` 只有head會移動
        - `--hard` 檔案跟暫存區都會變動

## 其他操作
### 讓 git 幫你刪除、變更檔案
- 讓git 幫你刪除檔案: 直接把檔案刪掉並將記錄加進暫存區  
`rm FILE` + `git add FILE`  
    => `git rm FILE`
- 將檔案從 git 移除，不過檔案仍在資料夾中  
`git rm FILE --cached`
- 讓git 幫你變更檔名: 直接把檔案改名並將記錄加進暫存區  
`mv FILE file` + `git add --all`  
    => `git mv FILE file`
### 修改最近一次commit紀錄
- 修改上一次的 commit message  
`git commit --amend -m "NEW_COMMIT_MESSAGE"`
- 追加檔案到最近一次commit  
`git add FILE`  
`git commit --ament --no-edit`
### .gitgnore
- 加入要忽略的檔案
```
*.zip
123.txt
```
- 接下來在資料夾中加入符合條件的檔案都會被 git 忽略
- 如果要加入一些符合gitgnore規則的檔案到git中  
`git add -f FILE`
- 不過gitgnore的規則只會對gitgnore建立之後新增的檔案有效，如果要將該規則朔及既往的話，先用 `git rm --cached` 將檔案刪除，之後就會被 git 忽略了
- 清除忽略檔案  
`git clean -fix`

### 只想提交部分文件
- `git add -p FILE`
- 之後選擇 `e`
- 之後便會跳轉到預設文字編輯器，即可編輯要提交的那些部分
## 注意事項
- 空的目錄無法被提交
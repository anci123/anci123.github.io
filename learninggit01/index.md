# LearningGit01

# 初始設定
- `git init`: 初始化當前目錄，開始進行版控~(產生.git 目錄)
- `git status` : 查詢當前狀態(commit 前查看狀態)
- `git add`: 將檔案加入暫存區(commit 前 add)
    - `add --all`，`add .`
    - `add 資料夾`
    - `add 檔案`
- `git commit`: 儲存異動
    - `-m` :後面加上這次有什麼變動的描述 ex:`git commit -m "change abc.md"`
    - `--allow-empty`: 沒有東西也可以commit XDD
    - `git commit -a -m "update content"`:add、commit一起搞定
    - `--author="manto"`: 找manto的commit
    - `git log --oneline --author="manto\|adam"`: 找兩個人的commit
- `git log`: 檢視git log 紀錄
    - `--oneline`、`--oneline 跟 --graph`: 讓輸出更精簡
- `git config --global credential.helper store`: 記住帳號密碼，這樣就不用每次push都要打帳密啦~
    - 修改: 直接去`~/.git-credential`修改  
    之後將cache daemon 退出  
    `git credential-cache exit`

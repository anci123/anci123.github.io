# Assembly01

# 學習組語
## 安裝 nasm
1.  安裝nasm
    ```
    sudo apt-get install nasm
    ```
2. 還沒安裝binutils或build-essential的話要裝一下
    ```
    subo apt-get install binutils
    ```
    ```
    subo apt-get install build-essential
    ```

## 編譯

1. 完成一個.asm檔之後照下面的指令開始編譯，就會產生一個.o檔啦~
    ```
    nasm -f elf64 hello_world.asm
    ```
2. 將.o輸出成一個可執行檔
    ```
    ld -s -o hello_world hello_world.o
    ```
3. 執行
    ```
    ./hello_world
    ```
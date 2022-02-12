# Program2

# 程式設計(二)
<!--more-->

## 解決 alignment 的問題

1. ```c
   __attribute__((packed))
   ```

2. ```c
   #pragma pack(push, 1)
   #pragma pack(pop)
   ```

3. ```c
   #pragma pack(push)
   #pragma pack(1)
   #pragma pack(pop)
   ```

# File

## fread

1. header: <stdio.h>
2. `size_t fread(void *ptr, size_t size, size_t nmemb, FILE *stream);`
3. 務必用型別為size_t 的變數去接回傳值
4. size 為 1 時，將回傳讀入多少 bytes

# Program Arguements

## getopt

*header: <unistd.h> (POSIX standard) 不一定能在windows上呼叫

* `int getopt(int argc, char * const argv[], const char *optstring);`
* argc: argument count(前面有加'`-`'，才會被當作 arguement)
* argv: argument array
* return value 是 command,若不再optstring 中則回傳 '`?`'，以 -1 標示結尾
* opstring: 放 command 的選項，若command後面要加參數，要在該字元後加 '`:`'
* 後接參數放在 optarg ，對於 optarg 要在 while loop 中處(或先 copy 出來)
* 小建議: switch block 中用變數去紀錄那些功能現在是開啟的 ex: `optionA = 1;`
* 使用 `printusage` 去偵錯

## getopt_long

* header: <getopt.h> 

* `int getopt_long(int argc, char * const argv[], const char *optstring, const struct option *longopts, int *longindex);`

* struct option

  ```c
  struct option {
      const char *name;
      int has_arg;
      int *flag;
      int val;
  };
  ```

  * 使用{0,0,0,0}標示結尾 -> 不用帶入 array 的size
  * name: the name of the long option.
  * has_arg:
    * 0: no arguments.
    * 1: required arguments.
    * 2: optional arguments.
    * flag: 當flag 不為 NULL ，將val 傳到 flag 的位址，且回傳值變為 0
    * val: 設定對應的 name 的 return value

* index

  * option array 中的 index

## Variable Length Arguement

* int printf(const char *format , ...);
* void printargs(int32_t args[], ...);
* double average(int32_t num, ...);
  * `...` 代表 arguement 的數量可改變
    * `va_list` 可將...中的變數取出(是一個 Macro )
    * `va_start(va_list ap, last)` : 設定起始位置
    * `va_arg(va_list, last)` :設定移動的單位
    * `va_end(va_list ap)` : 脫鉤
    * `va_cpy(va_list dest, va_list src)`

# Macro

* 在macro 定義一個函式
* `\` 表示換行
* 與一般宣告函式的區別:不占記憶體空間

```c
#define clearFgets(str,len,stream){\
fgets(str,len,stream);\
if(str[strlen(str)-1]=='\n')\
str[strlen(str)-1]=0;\
}
```

* Macro 要加`()`
* Macro 不加`;`

```c
#define add(a+b) a+b
int A=add(1+3)*10;
// A=1+3*10=31
```

```c
#define add(a+b) (a+b)
int A=add(1+3)*10;
//A=(1+3)*10
```

* 儘量不要加在Macro中宣告參數，避免重複宣告，不好除錯
* Macro 無法寫遞迴

# Some tricks

待了解: static link,htop,`top,htop -d 0`,`watch -n 0`,`cat /proc/stat | head -n 1`,MITM
待學習: GDB,awk,grep,cMake,makefile
***學資料結構時用C***

## #define

### ifdef

#### 一個條件：

1. 

```c
#ifdef 識別字
    /*若識別字被定義,編譯器會編譯此部分程式*/
#else
    /*否則編譯此部分程式*/
#endif
```

2. 

```c
#if defined(CONDITION_1)
    /*若識別字被定義,編譯器會編譯此部分程式*/
#elif
    /*否則編譯此部分程式*/
#endif
```

3. 

```c
#define CONDITION_1
#ifdef CONDITION_1
   /*編譯此部分程式*/
#else
   /*不編譯此部分程式*/
#endif
```

#### 兩個以上的條件

1. 

```c
#if defined(CONDITION_1) && defined(CONDITION_2)
   /*若條件達成,編譯器會編譯此部分程式*/
#endif
```

### ifndef 

```c
#ifndef 識別字
   /*若識別字沒有被定義,編譯器會編譯此部分程式*/
#else
   /*否則編譯此部分程式*/
#endif
```

### undef

```c
#undef 識別字
   /*取消定義*/
```

### #if #elif

1. 

```c
#if 條件式1
   /*若條件式1成立(true),編譯器會編譯此部分程式*/
#elif 條件式2
   /*若條件式2成立(true),編譯器會編譯此部分程式*/
#else
   /*若上述條件皆不成式,則會編譯此部分程式*/
#endif
```

2. 

```c
/*Eaxmple*/
#define CONDITION 1

#if CONDITION == 1
　 printf("Condition:1"); //會執行此行程式
#elif CONDITION == 2
   printf("Condition:2");
#else
   printf("Condition:other");
#endif
```


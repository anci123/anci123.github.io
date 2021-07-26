# Program1


# 程式設計(一)

## **注意事項**

* main函式先加 <font color=#00FFFF>return 0</font>
* 先初始化變數
* 使用 <font color=#00FFFF>\++i, --i</font> 而不是 i++
* scanf("%d",<font color=#00FFFF>&</font>a);

#  Arithmetic 計算

* **\ 跳脫字元**
  * \t -> tab
  * \n ->換行
  * \\" -> "
  * \\\ -> \
* **printf format**

| 類型字元     | 格式                               |
| ------------ | :--------------------------------- |
| %d           | 十進位帶號整數(int32_t)            |
| %ld          | (int64_t)                          |
| %hd          | (int16_t)                          |
| %hhd         | (int8_t)                           |
| %u           | 十進位無號整數(uint32_t)           |
| %lu,%hu,%hhu | (uint64_t)(uint16_t) (uint8_t)     |
| %f,%g,%e     | float(%g:去掉尾端的0)(%e:科學記號) |
| %lf,%lg,%le  | double                             |
| %x %X        | 十六進位整數(X:輸出為大寫)         |
| %o           | 八進位整數                         |
| %p           | 指標位址                           |
| %c           | 字元                               |
| %s           | 字串                               |

* a % b -> ( a/ b) * b + a % b = a -> -2 % 7=-2
* 

# string

## string functions

### string conversion functions

* 標頭檔: `#inlcude<stdlib.h>`
* strtod: `double strtod(const char *nptr, char **endptr);`
* strtol: `long int strtol(const char *nptr, char **endptr, int base);`

```C
int main(){
   char str[30] = "20.30300 This is test";
   char **ptr;
   double ret;

   ret = strtod(str, ptr);
   printf("The number(double) is %lf
", ret);
   printf("String part is |%s|", *ptr);

   return(0);
}
```

### intput/output fuctions

* getchar:`int getchar(void);`
* fgets:`char *fgets(char *s, int size, FILE *stream);`
  '\n'也會讀入，須對'\n'處理過才是一般的字串
* putcahr:`int putchar(int c);`
* puts: `int puts(const char *s);`
* snprintf: `int snprintf(char *str, size_t size, const char *format , ...);`
* sscanf: `int sscanf(const char *str, const char *format , ...);`


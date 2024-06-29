# Object Oriented Design

---

## 在程式碼裡，宣告```int a = 1```  

### 如何被記憶體儲存?

記憶體以bits (binary digit)為最小量化單位儲存資訊，代表為一個邏輯值:1/0、開/關等等
二進制數字系統（binary numeral system）是一種利用兩個不同的符號（通常是0和1）來表示數字的系統
結合二進制數字系統以及bits，即可表達不同進制的數字

具體會以幾個bits被儲存，會根據不同的計算機架構（16-bit/ 32-bit/ 64bit）、編譯器Complier、Processing(e.g. CPU最佳化)而有所不同

- [Integer numbers storage in computer memory](https://medium.com/@luischaparroc/integer-numbers-storage-in-computer-memory-47af4b59009)

- [進制簡介](https://notfalse.net/14/numeral-system-intro) *note*: 日常生活中常使用的是十進制(decimal, base 10)，逢十進位; 時間則為六十進制

### 如何被CPU拿出來運算?

1. 程式碼編譯
執行程式碼時，編譯器會將其轉化為機器碼([相關文章: .NET CLR](https://hackmd.io/CpUKcQMxTYOLjurv3UYPeA?view))，機器碼包含了一系列的指令，這些指令將被存儲在記憶體中。

2. 取指令 (Fetch)
CPU的控制單元(CU)會指示[程式計數模組 (Program Counter)](https://www.geeksforgeeks.org/what-is-program-counter/)儲存即將要執行的指令碼對應到的記憶體位置。
指令被讀取到[暫存器(CPU Register)](https://www.eagletek.com.tw/post/register-in-cpu)之後，Counter會更新到下一個位置

3. 解碼（Decode）
CU 解碼儲存在指令暫存器中的指令，決定需要進行的操作及操作所需的資料

4. 執行（Execute）
算術邏輯單元（ALU）執行計算或邏輯運算，加減乘除、AND、OR等等，然後將結果寫回到暫存器

- [ChatGPT-Brief Summary](https://chatgpt.com/c/1f0a5816-7274-4193-b5cb-d51fee08e5a1)
- [數據匯排流(Data Bus)](https://zh.wikipedia.org/wiki/%E6%80%BB%E7%BA%BF)

如果有一段古早的程式碼，可能長這樣

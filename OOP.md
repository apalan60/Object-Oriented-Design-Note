# Object Oriented Design

## 早期的程式語言可能如何開發?

### Int

**如何被記憶體儲存?**

記憶體以bits (binary digit)為最小量化單位儲存資訊，代表為一個邏輯值:1/0、開/關等等

二進制數字系統（binary numeral system）是一種利用兩個不同的符號（通常是0和1）來表示數字的系統

結合二進制數字系統以及bits，即可表達不同進制的數字

在程式碼裡，宣告```int a = 1``` 具體會以幾個bits被儲存，會根據不同的計算機架構（16-bit/ 32-bit/ 64bit）、編譯器Complier、Processing(e.g. CPU最佳化)而有所不同

- [Integer numbers storage in computer memory](https://medium.com/@luischaparroc/integer-numbers-storage-in-computer-memory-47af4b59009)

*note*: 日常生活中常使用的是十進制(decimal, base 10)，逢十進位; 時間則為六十進制

- [進制簡介](https://notfalse.net/14/numeral-system-intro)

**如何被CPU拿出來運算?**

- [ChatGPT](https://chatgpt.com/c/1f0a5816-7274-4193-b5cb-d51fee08e5a1)

如果有一段古早的程式碼，可能長這樣

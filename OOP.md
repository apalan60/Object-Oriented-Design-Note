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

## 字串及日期型別可能的底層實作

### String

字串也是一連串的記憶體位置，裡面包含類似整數的字元代碼
e.g.

```cSharp
string name = "Jill"
```

```cSharp
['J', 'i', 'l', 'l']
```

7-bit ASCII Code

```cSharp
[74, 105, 108, 108 ]
```

### DateTime

早期C#並沒有DateTime型別，而是在.NET Framework 1.0版引入的

如果有一段古早的程式碼要表達日期，需要使用int型別
e.g.

```cSharp
int birthdate = 20160229
```

如果要做日期的運算，又是更為麻煩，以計算明年的生日為例

```cSharp
int birthdate = 20160229
int year = birthdate / 10000;
int month = (birthdate % 10000) / 100;
int day = birthdate % 100;

int nextYear = year + 9;

 bool isLeapYear = (nextYear % 4 == 0 && nextYear % 100 != 0) || (nextYear % 400 == 0);

if (month == 2 && day == 29 && !isLeapYear)
{
    day = 28;
}

int birthDayInNextYear = nextYear * 10000 + month * 100 + day;

```

---

## Procedural Programming

**Problem Difinition**
如果每次計算明年的生日，都要執行上面那一段指令，會很冗餘

**Solution**
一連串的指令概括為一個代稱**Procedure**，並將這段指令放在Program裡，提供一個程式的進入點(Entry Point)，帶來了隱藏複雜性跟具複用性的好處

```csharp
program
{
   GetDateInNextYear(int now);
}
```

但仍存在一些問題，例如Temporal coupling

initialize(Similar to constructor)

## Modular Programming

**Problem Difinition**
在當前的program share 同一個Modual，如果任何一個caller需要不同初始化資訊來調用該
procedure，他們會覆蓋之前的Data，因為其放置在Shared Memory block

**Soultion**
指派一個新的變數(new memory block)來存放初始化出來的值，任何調用這個變數的Consumer，需要去記住這個變數的記憶體位置

這個行為形成了物件導向世界裡的**建構函數(Constructor)**，建構了一個**物件(Object)**

而Procedures改為傳入Object作為參數，使可以對該記憶體區塊做操作，使不同的caller，能用不同的數據來調用相同的Procedure，達到真正意義上的分離

Object解決了Module共享記憶體的問題，使可以創建相同結構，但獨立的數據副本，即為所謂的**實例(instance)**

```cSharp
module SchoolCalender
 int schoolMonth
 int schoolday
 int minAge

 initilize(int month, int day, int schoolMonth)
    schoolMonth = month
    schoolDay = day
    minAge = age

```

## Object Oriented Programming

隨著物件的出現，以上的型式便衍生了新的說法: class, field, function，
當宣告一個class，並有一個int型別的age，代表著物件被實例化時，會被分配4 bytes來儲存，這就是其中field的內涵。initialize()則被轉化為Constructor, procedure被轉化為function

### 記憶體分配

```CSharp
var pen = new Pen(color);
pen.Write();
```

此時pen已佔用了記憶體，若長期放置，在使用完後不被刪除，則會造成*Memory Leak*
在C++裡，可以手動釋放記憶體(*Memory Deallocation*)

```C++
delete pen
```

手動釋放記憶體存在一些可能的人為錯誤，包含:

1. 懸空指標(*Dangling pointer*) : 在仍有代碼有pointer指向某物件時，但他卻被刪除，指向的記憶體位址是空的。

2. Reading Garbage: 在上述情況，原記憶體區段被賦予了新的值，導致指向非預期的目標

3. Memory leak: 物件不使用了卻沒刪，導致記憶體占用問題

在C#裡，則會統一透過**Garbage Collection**管理記憶體，由系統判斷，在需要時調用，不需要時釋放
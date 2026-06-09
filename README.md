# Small-C 互動式解譯器 UML

> 主專案：[https://github.com/yubo1217/Small-C](https://github.com/yubo1217/Small-C)

**課程：** 物件導向軟體設計｜**學期：** Spring 2026｜**作者：** 林煜博

---

## 專案 UML 文件說明

本專案以 Small-C 互動式解譯器為標的，運用多種 UML 圖型對系統進行完整的物件導向分析與設計，涵蓋使用案例圖、使用案例描述、活動圖、類別圖與詞彙表，共五大類別。

### 使用案例圖（Use Case Diagram）

共 8 張，對應系統的 8 個功能面向，描述使用者或開發者與系統之間的互動關係，並以 `<<include>>` 與 `<<extend>>` 標示用例間的依賴與條件延伸。

| 編號 | 檔案 | 涵蓋內容 |
|------|------|---------|
| UC01 | `uc_01_repl_overview.png` | REPL 系統總覽：管理程式碼輸入、執行程式、語法檢查、查詢系統資訊、離開系統、TRACE 追蹤 |
| UC02 | `uc_02_program_input.png` | 程式碼輸入管理：直接輸入、LOAD 載入檔案、APPEND 附加、NEW 清空、SAVE 儲存 |
| UC03 | `uc_03_buffer_edit.png` | 緩衝區編輯：LIST 顯示、EDIT 修改行、DELETE 刪除行、INSERT 插入行、CLEAR 清除畫面 |
| UC04 | `uc_04_execution.png` | 程式執行：RUN 執行、CHECK 語法檢查、語法解析、AST 走訪執行、TRACE 追蹤、執行期錯誤回報 |
| UC05 | `uc_05_query.png` | 系統查詢：VARS 查看變數、FUNCS 查看函式、ABOUT 系統資訊、HELP 說明 |
| UC06 | `uc_06_language_data.png` | 語言資料宣告：int / char / 指標 / 陣列宣告，含記憶體配置與初始化 |
| UC07 | `uc_07_control_flow.png` | 控制流程：if/else、while、for、do-while、switch 多路分支、break/continue |
| UC08 | `uc_08_functions.png` | 函式呼叫：使用者定義函式、內建函式分派、引數傳遞、遞迴呼叫 |

### 使用案例描述（Use Case Description）

共 8 個使用案例，每個案例包含 3 張描述表：**正常流程**（normal）、**例外流程一**（ex1）、**例外流程二**（ex2），以結構化表格呈現前置條件、主要流程步驟、替代流程與後置條件。

| 編號 | 資料夾 | 涵蓋內容 |
|------|--------|---------|
| UCD01 | `ucd_01/` | REPL 主迴圈的啟動、指令分派、正常結束與例外處理 |
| UCD02 | `ucd_02/` | 程式碼輸入管理（LOAD、APPEND、SAVE、NEW）的正常與例外流程 |
| UCD03 | `ucd_03/` | 緩衝區行編輯（LIST、EDIT、DELETE、INSERT）的正常與例外流程 |
| UCD04 | `ucd_04/` | 程式執行（RUN / CHECK）的完整管線流程與各類錯誤情境 |
| UCD05 | `ucd_05/` | 系統查詢（VARS、FUNCS、HELP、ABOUT）的正常與例外流程 |
| UCD06 | `ucd_06/` | 語言資料宣告（int / char / 指標 / 陣列）的正常與例外流程 |
| UCD07 | `ucd_07/` | 控制流程語句（if、while、for、switch 等）的正常與例外流程 |
| UCD08 | `ucd_08/` | 函式定義與呼叫（使用者函式、內建函式、遞迴）的正常與例外流程 |

### 活動圖（Activity Diagram）

共 8 張，與使用案例一一對應，以活動節點、決策菱形與分叉/合流描述各功能的執行流程細節。

| 編號 | 檔案 | 涵蓋內容 |
|------|------|---------|
| AD01 | `ad_01_repl.png` | REPL 主迴圈：初始化、提示字元顯示、指令讀取、分派執行、回到提示符 |
| AD02 | `ad_02_input.png` | 程式碼輸入：依指令類型（LOAD / APPEND / SAVE / NEW / 直接輸入）分支執行 |
| AD03 | `ad_03_edit.png` | 緩衝區編輯：依指令類型（LIST / EDIT / DELETE / INSERT / CLEAR）分支執行 |
| AD04 | `ad_04_exec.png` | 程式執行管線：前置處理 → 詞法分析 → 語法解析 → AST 走訪，含 TRACE 與錯誤處理分支 |
| AD05 | `ad_05_query.png` | 系統查詢：依指令類型（VARS / FUNCS / ABOUT / HELP / TRACE）分支輸出 |
| AD06 | `ad_06_data.png` | 資料宣告：依宣告類型（一般變數 / 陣列 / 指標）分支配置記憶體與初始化 |
| AD07 | `ad_07_flow.png` | 控制流程：依 AST 節點類型（if / while / for / do-while / switch / break）分支執行 |
| AD08 | `ad_08_func.png` | 函式呼叫：引數求值 → 查找使用者函式或內建分派表 → 建立作用域 → 執行 → 回傳值 |

### 類別圖（Class Diagram）

共 1 張（`smallc_class.png`），涵蓋系統全部模組的類別結構與依賴關係：

- **`lexer.py`**：`Token`、`Lexer`，負責詞法分析與 `#define` 前置處理
- **`parser.py`**：`AST` 抽象基底、`Expr` / `Stmt` / `Decl` 抽象層次，以及 `Number`、`BinOp`、`Call`、`VarDecl`、`ArrayDecl`、`FuncDef`、`IfStmt`、`WhileStmt`、`ForStmt`、`SwitchStmt`、`Return` 等具體節點類別；`Parser` 遞迴下降解析器
- **`interpreter.py`**：`Interpreter` 樹狀走訪直譯器，`BreakException`、`ContinueException`、`ReturnException` 控制流程例外
- **`symtable.py`**：`Symbol`（型別、位址、指標/陣列旗標）、`SymbolTable`（作用域堆疊）
- **`memory.py`**：`Memory`（線性記憶體空間，bump allocator）
- **`builtins.py`**：`Builtins`（內建函式分派表）
- **`repl.py`**：`ReplInputCollector`（多行輸入收集）、`REPL`（互動環境主體）
- **`main.py`**：`Main` 進入點模組

### 詞彙表（Glossary）

共 1 張（`glossary.png`），以結構化表格定義專案中所有重要術語，分為五大區：

1. **直譯器核心技術**：Token、Lexer、preprocess()、Parser、AST、Interpreter、REPL、ReplInputCollector
2. **記憶體與符號管理**：Memory、int32()、heap\_top（Bump Allocator）、SymbolTable、Symbol、Scope
3. **控制流與內建功能**：BreakException、ContinueException、ReturnException、Builtins
4. **REPL 指令集**：LOAD/RUN、CHECK、TRACE ON/OFF、VARS/FUNCS、LIST/EDIT/INSERT/DELETE/APPEND、SAVE/NEW/CLEAR、ABOUT
5. **Small-C 支援語言特性**：#define 巨集、switch/case/default（fall-through）、複合賦值運算子、執行期錯誤處理

---

## 專案介紹目錄

1. [專案概述](#1-專案概述)
2. [REPL 互動環境](#2-repl-互動環境)
3. [Small-C 語言規格](#3-small-c-語言規格)
4. [內建函式規格](#4-內建函式規格)
5. [錯誤處理規格](#5-錯誤處理規格)
6. [系統架構](#6-系統架構)
7. [模組說明](#7-模組說明)
---

## 1. 專案概述

Small-C 互動式解譯器是一個以純 Python 3 實作的樹狀走訪（tree-walking）解譯器，支援 C 語言的核心子集。使用者可透過互動式 REPL（Read-Eval-Print Loop）直接輸入並執行 Small-C 程式碼，亦可載入完整程式檔案後批次執行。

**設計目標：**

- 實作標準 C 語言語意的核心子集，包含指標、陣列、遞迴函式
- 提供完整的互動式行編輯環境（緩衝區管理、逐行修改、存取檔案）
- 不依賴任何第三方套件，僅使用 Python 3 標準函式庫
- 提供 TRACE 追蹤模式以協助除錯

---

## 2. REPL 互動環境

REPL 維護一個**程式碼緩衝區**（buffer），所有行編輯操作均作用於此緩衝區。指令名稱**不區分大小寫**。

### 2.1 程式管理指令

| 指令 | 語法 | 說明 |
|------|------|------|
| `APPEND` | `APPEND` | 在緩衝區末尾逐行追加程式碼，輸入單獨一行 `.` 結束 |
| `LIST` | `LIST` / `LIST n` / `LIST n1-n2` | 列出全部、第 n 行、或第 n1 至 n2 行的緩衝區內容（附行號） |
| `EDIT` | `EDIT n` | 顯示第 n 行並等待輸入新內容取代；直接按 Enter 保留原內容 |
| `DELETE` | `DELETE n` / `DELETE n1-n2` | 刪除第 n 行或第 n1 至 n2 行，後續行號自動遞減 |
| `INSERT` | `INSERT n` | 在第 n 行之前插入一或多行，輸入單獨一行 `.` 結束 |
| `NEW` | `NEW` | 清空緩衝區並重置直譯器狀態；若有未儲存修改會先提示確認 |
| `LOAD` | `LOAD <filename>` | 從檔案載入原始碼到緩衝區；若有未儲存修改會先提示確認 |
| `SAVE` | `SAVE <filename>` | 將緩衝區內容儲存到指定檔案 |

### 2.2 執行指令

| 指令 | 語法 | 說明 |
|------|------|------|
| `RUN` | `RUN` | 對緩衝區程式進行前處理、解析並執行；需包含 `main()` 函式 |
| `CHECK` | `CHECK` | 對緩衝區程式進行語法檢查，不實際執行；顯示錯誤數量 |
| `TRACE` | `TRACE ON` / `TRACE OFF` | 啟用或關閉追蹤模式；啟用後每個執行步驟前輸出 `[line n] <statement>` |

**互動模式**：不使用以上指令時，直接在 `sc>` 提示符輸入 Small-C 程式片段（包含函式定義、敘述、運算式），即時解析並執行，無需 `main()` 函式。

### 2.3 狀態查詢指令

| 指令 | 語法 | 說明 |
|------|------|------|
| `VARS` | `VARS` | 列出所有全域變數的名稱、型別與目前數值 |
| `FUNCS` | `FUNCS` | 列出所有使用者定義函式（含回傳型別、參數、定義行號）與內建函式 |

### 2.4 系統指令

| 指令 | 語法 | 說明 |
|------|------|------|
| `HELP` | `HELP` / `HELP <cmd>` | 顯示所有指令摘要，或指定指令的詳細說明 |
| `ABOUT` | `ABOUT` | 顯示解譯器名稱、版本號、作者資訊與修課學期 |
| `CLEAR` | `CLEAR` | 清除終端機畫面 |
| `QUIT` / `EXIT` | `QUIT` 或 `EXIT` | 退出解譯器；若有未儲存修改會先提示確認 |

---

## 3. Small-C 語言規格

### 3.1 資料型別

| 型別 | 位元寬度 | 數值範圍 |
|------|---------|---------|
| `int` | 32 位元有號整數 | −2,147,483,648 ～ 2,147,483,647 |
| `char` | 8 位元有號整數 | −128 ～ 127 |
| `void` | 僅用於函式回傳型別 | — |
| 指標 `*` | 同 `int`（記憶體位址） | 0 ～ 65535 |

整數截斷：所有 `int` 運算結果均截斷為 32 位元有號整數範圍；`char` 賦值截斷為 8 位元有號整數範圍。

### 3.2 常數字面量

| 類型 | 範例 | 說明 |
|------|------|------|
| 十進位整數 | `42`, `-100` | 標準十進位表示 |
| 十六進位整數 | `0xFF`, `0xAB` | 前綴 `0x` 或 `0X` |
| 字元字面量 | `'A'`, `'\n'`, `'\0'` | 單引號包圍，支援跳脫序列 |
| 字串字面量 | `"hello\n"` | 雙引號包圍，儲存為 C 字串（null 結尾） |

支援的跳脫序列：`\n`、`\t`、`\r`、`\\`、`\'`、`\"`、`\0`。

### 3.3 運算子

**優先順序（由低至高）：**

| 優先順序 | 運算子 | 結合性 |
|---------|-------|-------|
| 1（最低） | `=` `+=` `-=` `*=` `/=` `%=` | 右至左 |
| 2 | `\|\|` | 左至右 |
| 3 | `&&` | 左至右 |
| 4 | `\|` | 左至右 |
| 5 | `^` | 左至右 |
| 6 | `&` | 左至右 |
| 7 | `==` `!=` | 左至右 |
| 8 | `<` `<=` `>` `>=` | 左至右 |
| 9 | `<<` `>>` | 左至右 |
| 10 | `+` `-` | 左至右 |
| 11 | `*` `/` `%` | 左至右 |
| 12（最高） | 前置 `++` `--` `!` `~` `-` `*` `&` | 右至左 |

**語意說明：**
- `%` 使用 C 語言截斷除法語意（符號跟隨被除數），而非 Python 的地板除法語意
- `&&` 與 `||` 支援短路求值（short-circuit evaluation）
- 前置 `++`/`--` 先修改值再使用；**不支援後置** `++`/`--`

### 3.4 宣告

```c
// 一般變數（可帶初始值）
int x;
int y = 42;
char c = 'A';

// 陣列（固定大小，索引從 0 起）
int arr[10];
char buf[50];
int data[5] = {1, 2, 3, 4, 5};

// 指標
int *p;
char *s;
```

**限制：** 依據規格，區域變數宣告應集中於函式開頭，不支援在區塊中途宣告變數。

### 3.5 函式

```c
// 函式定義
int add(int a, int b) {
    return a + b;
}

// 回傳指標的函式
int *get_ptr(int *arr, int i) {
    return &arr[i];
}

// void 函式
void print_hello() {
    printf("Hello\n");
}

// 程式進入點（緩衝模式需要）
int main() {
    return 0;
}
```

支援遞迴呼叫。參數傳遞為**值傳遞**；若要修改呼叫端變數，需傳遞指標。

### 3.6 控制流程

**條件：**
```c
if (x > 0) {
    printf("positive\n");
} else {
    printf("non-positive\n");
}
```

**迴圈：**
```c
while (i < n) { i += 1; }

for (i = 0; i < n; i += 1) { ... }

do {
    ...
} while (condition);
```

**Switch（支援 fall-through）：**
```c
switch (x) {
    case 1:
        printf("one\n");
        break;
    case 2:
    case 3:
        printf("two or three\n");
        break;
    default:
        printf("other\n");
}
```

**跳轉：**
- `break` — 跳出最近的迴圈或 switch
- `continue` — 跳到最近迴圈的下一次迭代
- `return` / `return expr` — 從函式返回

### 3.7 前置處理器

支援無參數的 `#define` 巨集：

```c
#define SIZE 8
#define MAX_VAL 1000
```

展開規則：以識別字邊界為準進行文字替換，不會誤替換識別字內的子串。

**不支援：** 帶參數的函式式巨集、`#include`。

### 3.8 註解

```c
// 單行註解：從 // 到行尾

/* 區塊註解：
   可跨越多行 */
```

---

## 4. 內建函式規格

### 4.1 I/O 函式

| 函式 | 簽名 | 說明 |
|------|------|------|
| `printf` | `void printf(char *fmt, ...)` | 格式化輸出；支援 `%d`（十進位整數）、`%c`（字元）、`%s`（字串）、`%x`（十六進位）、`%%`（百分號） |
| `scanf` | `int scanf(char *fmt, ...)` | 格式化輸入；支援 `%d`（讀入整數）、`%c`（讀入字元）；回傳成功讀入的項目數 |
| `putchar` | `int putchar(int ch)` | 輸出單一字元，回傳輸出的字元值 |
| `getchar` | `int getchar()` | 讀入單一字元，回傳字元的 ASCII 值；EOF 時回傳 -1 |
| `puts` | `void puts(char *s)` | 輸出字串並自動換行 |

### 4.2 字串函式

| 函式 | 簽名 | 說明 |
|------|------|------|
| `strlen` | `int strlen(char *s)` | 回傳字串長度（不含結尾 null） |
| `strcpy` | `void strcpy(char *dest, char *src)` | 將 `src` 複製到 `dest`（含結尾 null） |
| `strcmp` | `int strcmp(char *s1, char *s2)` | 比較兩字串；s1 < s2 回傳負值，相等回傳 0，s1 > s2 回傳正值 |
| `strcat` | `void strcat(char *dest, char *src)` | 將 `src` 附加到 `dest` 末尾 |

### 4.3 數學函式

| 函式 | 簽名 | 說明 |
|------|------|------|
| `abs` | `int abs(int x)` | 回傳絕對值 |
| `max` | `int max(int a, int b)` | 回傳較大值 |
| `min` | `int min(int a, int b)` | 回傳較小值 |
| `pow` | `int pow(int base, int exp)` | 回傳 base 的 exp 次方（整數） |
| `sqrt` | `int sqrt(int x)` | 回傳正整數平方根（截斷取整）；引數為負時產生執行期錯誤 |
| `mod` | `int mod(int a, int b)` | 同 `%` 運算子（C 語意截斷除法之餘數） |
| `rand` | `int rand()` | 回傳偽隨機整數 |
| `srand` | `void srand(int seed)` | 設定隨機數種子 |

### 4.4 工具函式

| 函式 | 簽名 | 說明 |
|------|------|------|
| `memset` | `void memset(char *ptr, int value, int size)` | 將 `size` 個記憶體單元設為 `value` |
| `sizeof_int` | `int sizeof_int()` | 回傳 `int` 型別大小（固定為 4） |
| `sizeof_char` | `int sizeof_char()` | 回傳 `char` 型別大小（固定為 1） |
| `atoi` | `int atoi(char *s)` | 將數字字串轉為整數 |
| `itoa` | `void itoa(int value, char *str)` | 將整數轉為十進位字串存入 `str` |
| `exit` | `void exit(int code)` | 以指定回傳碼終止程式 |

---

## 5. 錯誤處理規格

所有錯誤均捕捉於 REPL 層，印出訊息後回到 `sc>` 提示符，解譯器不崩潰。

### 5.1 語法 / 詞法錯誤

錯誤訊息格式依執行情境不同：

| 情境 | 格式 |
|------|------|
| 互動模式（直接輸入） | `Syntax error: <msg>` |
| `CHECK` / `RUN` 緩衝區模式 | `Error at line N: <msg>` |

範例：
```
Syntax error: unexpected token ';', expected expression.
Error at line 3: unexpected token ';', expected expression.
Error at line 5: Unterminated string literal.
```

詞法錯誤（例如未閉合的字串、非法字元、非法跳脫序列）同樣包裝成 `ParseError` 並以相同格式輸出。

### 5.2 執行期錯誤

| 錯誤情境 | 訊息格式 |
|---------|---------|
| 除以零 | `Runtime error: division by zero.` |
| 陣列索引越界 | `Runtime error: array index out of bounds (index 10, size 5).` |
| 空指標解參考 | `Runtime error: null pointer dereference` |
| 左移次數為負 | `Runtime error: left shift count is negative.` |
| 右移次數為負 | `Runtime error: right shift count is negative.` |
| `sqrt()` 引數為負 | `Runtime error: sqrt() argument must be non-negative.` |
| 記憶體不足 | `Runtime error: Out of memory` |
| 記憶體存取越界 | `Runtime error: Memory access out of bounds: address N` |
| 函式參數數量錯誤 | 執行期錯誤，顯示函式名稱與期望/實際參數數量 |

### 5.3 程式結束

緩衝區 `RUN` 時 `main()` 正常返回或呼叫 `exit()`，均輸出：

```
Program exited with return value N.
```

互動模式下呼叫 `exit()` 同樣輸出上述訊息，並不影響 REPL 繼續運作。

---

## 6. 系統架構

### 6.1 管線架構

資料從原始碼到輸出，嚴格單向流動：

```
原始碼（字串）
    │
    ▼
preprocess()           ← 展開 #define 巨集
    │
    ▼
Lexer.tokenize()       ← 詞法分析，產生 Token 序列
    │  Token(kind, value, line)
    ▼
Parser.parse()         ← 語法分析，產生 AST
    │  Program / FuncDef / Stmt / Expr 節點
    ▼
Interpreter.execute()  ← 樹狀走訪，直接執行
    │
    ▼
標準輸出（stdout）
```

### 6.2 記憶體模型

採用線性堆疊式配置器（bump allocator）：

- 全域空間大小：65,536 個整數單元
- `allocate(n)`：從 `heap_top` 往高位址方向延伸 n 個單元
- `free_to(addr)`：將 `heap_top` 回退到 `addr`，批次釋放函式的區域變數
- 所有變數、陣列、字串均配置於此空間

### 6.3 符號表模型

採用作用域堆疊：

- `scopes[0]` — 全域作用域（永久保留）
- `scopes[1+]` — 每次函式呼叫時 push，函式返回時 pop
- `lookup()` 由內向外搜尋，實現 C 語言的變數遮蔽（shadowing）語意

### 6.4 控制流程實作

`break`、`continue`、`return` 透過 Python 例外實作：

| 控制流程 | Python 例外 | 捕捉點 |
|---------|------------|-------|
| `break` | `BreakException` | 最近的迴圈或 switch |
| `continue` | `ContinueException` | 最近的迴圈 |
| `return expr` | `ReturnException(value)` | 函式呼叫點 |

---

## 7. 模組說明

| 檔案 | 職責 |
|------|------|
| `main.py` | 程式進入點，實例化 `REPL` 並呼叫 `run()` |
| `lexer.py` | `preprocess()`（#define 展開）+ `Lexer`（詞法分析器）+ `Token` 資料類別 |
| `parser.py` | 所有 AST 節點類別（`Expr` / `Stmt` / `FuncDef` / `Program` 階層）+ `Parser`（遞迴下降解析器） |
| `interpreter.py` | `Interpreter`（AST 樹狀走訪直譯器）；包含 `BreakException`、`ContinueException`、`ReturnException` |
| `symtable.py` | `SymbolTable`（作用域堆疊）+ `Symbol`（型別、位址、指標/陣列旗標） |
| `memory.py` | `Memory`（線性記憶體空間）；提供 allocate / free_to / read / write / read_string / write_string |
| `builtins.py` | `Builtins`；實作所有內建函式的分派與執行邏輯 |
| `repl.py` | `ReplInputCollector`（多行輸入收集器）+ `REPL`（互動環境主體） |

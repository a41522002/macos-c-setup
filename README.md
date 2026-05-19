# macOS C 語言開發環境安裝流程

> 適用於全新的 macOS 電腦，從零開始建立 C 語言開發環境。
> 環境參考：Apple Silicon (arm64) + macOS + VSCode + Clang。

---

## 📋 流程總覽

1. 安裝 **Xcode Command Line Tools** (提供 Clang 編譯器、make)
2. 驗證編譯器
3. 安裝 **VSCode**
4. 安裝必要的 **VSCode 擴充功能**
5. 建立第一個 C 專案測試

---

## 1️⃣ 安裝 Xcode Command Line Tools (編譯器)

macOS 預設**沒有**內建 `clang` / `gcc` 指令，需要透過 Command Line Tools 安裝。

打開「終端機 (Terminal)」執行：

```bash
xcode-select --install
```

執行後會跳出 GUI 安裝視窗，按「安裝」並同意授權條款，約 5–10 分鐘完成。

> 💡 **不需要**裝完整的 Xcode (那個有十幾 GB)，Command Line Tools 就夠寫 C 了。

### 安裝完成後會取得：

| 工具 | 用途 |
|---|---|
| `clang` | C/C++ 編譯器 (Apple 官方版本) |
| `gcc` | clang 的別名 (macOS 上指向 clang) |
| `make` | Makefile 建置工具 |
| `lldb` | 除錯器 |
| `git` | 版本控制 |

---

## 2️⃣ 驗證編譯器是否安裝成功

在終端機執行以下指令：

```bash
clang --version
gcc --version
xcode-select -p
which make
```

### 預期輸出範例：

```
Apple clang version 17.0.0 (clang-1700.0.13.5)
Target: arm64-apple-darwin25.2.0
InstalledDir: /Library/Developer/CommandLineTools/usr/bin

/Library/Developer/CommandLineTools

/usr/bin/make
```

只要有版本資訊跑出來，就代表安裝成功 ✅

---

## 3️⃣ 安裝 VSCode

從官網下載 macOS 版本：

🔗 https://code.visualstudio.com/

安裝後建議啟用「在終端機輸入 `code` 開啟 VSCode」的功能：

1. 打開 VSCode
2. `Cmd + Shift + P` 開啟命令面板
3. 輸入並執行：`Shell Command: Install 'code' command in PATH`

之後就可以在終端機用 `code .` 開啟當前資料夾。

---

## 4️⃣ 安裝 VSCode 擴充功能

開啟 VSCode 後，按 `Cmd + Shift + X` 進入擴充功能面板，搜尋安裝以下套件：

### 🔧 必裝 (核心開發)

| 擴充功能 | ID | 用途 |
|---|---|---|
| **C/C++** | `ms-vscode.cpptools` | IntelliSense、除錯、程式碼瀏覽 |
| **C/C++ Extension Pack** | `ms-vscode.cpptools-extension-pack` | 整合包 (含 CMake Tools) |
| **C/C++ Themes** | `ms-vscode.cpptools-themes` | 語法高亮配色 |

> 💡 安裝 **Extension Pack** 會自動帶入 `cpptools` + `cmake-tools`，所以實際只需要點兩三個套件。

### ⚡ 推薦 (一鍵編譯執行)

| 擴充功能 | ID | 用途 |
|---|---|---|
| **C/C++ Compile Run** | `danielpinto8zz6.c-cpp-compile-run` | 按 **F6** 編譯、**F7** 編譯+執行 |
| **Code Runner** | `formulahendry.code-runner` | 通用執行器，點右上角 ▶️ 一鍵跑 |

> 兩者功能重疊，**擇一安裝即可**。新手推薦 **Code Runner**，操作最直覺。

### 🚀 一行指令安裝全部 (進階)

如果 `code` 指令已設定好，可以直接在終端機跑：

```bash
code --install-extension ms-vscode.cpptools
code --install-extension ms-vscode.cpptools-extension-pack
code --install-extension ms-vscode.cpptools-themes
code --install-extension formulahendry.code-runner
```

---

## 5️⃣ 建立第一個 C 專案測試

### 步驟 1：建立資料夾

```bash
mkdir ~/c-practice
cd ~/c-practice
code .
```

### 步驟 2：建立 `hello.c`

在 VSCode 中新增檔案 `hello.c`：

```c
#include <stdio.h>

int main(void) {
    printf("Hello, C on macOS!\n");
    return 0;
}
```

### 步驟 3：執行

**方法 A — 用 Code Runner (推薦)**
點右上角 ▶️ 按鈕，下方終端機會顯示輸出。

**方法 B — 手動編譯**
在 VSCode 終端機 (`` Ctrl + ` ``) 執行：

```bash
clang hello.c -o hello
./hello
```

預期輸出：
```
Hello, C on macOS!
```

---

## 🎯 常用 Clang 編譯指令備忘

```bash
# 基本編譯
clang hello.c -o hello

# 開啟所有警告 (建議養成習慣)
clang -Wall -Wextra hello.c -o hello

# 指定 C 標準 (C11 / C17 / C23)
clang -std=c17 hello.c -o hello

# 開啟除錯資訊 (給 lldb 用)
clang -g hello.c -o hello

# 多檔編譯
clang main.c utils.c -o app
```

---

## ✅ 完成檢查清單

- [ ] `xcode-select --install` 已執行
- [ ] `clang --version` 有輸出版本號
- [ ] VSCode 已安裝且 `code` 指令可用
- [ ] C/C++ Extension Pack 已安裝
- [ ] Code Runner (或 C/C++ Compile Run) 已安裝
- [ ] `hello.c` 成功編譯並輸出結果

全部打勾 → 環境設定完成，可以開始寫 C 了 🎉

---

## 📚 補充參考

- Clang 官方文件：https://clang.llvm.org/docs/
- VSCode C/C++ 官方指南：https://code.visualstudio.com/docs/languages/cpp
- C 語言標準參考：https://en.cppreference.com/w/c

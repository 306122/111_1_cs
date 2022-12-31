# 111_1_cs
### 計概筆記
#####  資科一A 房謙
* 我將會在這裡記錄我在**計算機概論實習課**中所學之內容
* **
#### 目錄：
* 為什麼要學 **Git** 和 **Linux** ？ 
* 正規表達示
* **awk** 與 **sed** 指令的介紹與實作
* **git** 實作
* **SSH**金鑰 與其對 **github** 的連線
* Git flow
***
### 為什麼要學 **Git** 和 **Linux** ？

**Git** 是一个開元的的分布式版本控制系统，有效率地處理項目版本管理是它最大的特點之一。是[Linus Tojrvalds](https://baike.baidu.com/item/Linus%20Torvalds/9336769)了幫助Linux内核開發而開發的的免費版本控制軟體。

##### 應用實例：要做BIM建模，對模型初稿做修改
* 修改萬一出錯但已經保存了，就會無法撤銷。所以就得一直複製出新的文件一一修改。
* **文件數量慢慢增加，你不見得會記得你都改了什麼。**

#### git可以幫你...
當你修改了文件並保存後，就用git的相關指令給其管理，git就會產生快照，記錄保存的狀態，之後不論你對原文件進行任何修改，**只要沒有刪除git檔案，就可以隨時恢復。也讓許多散亂的檔案變成輕巧的一份小檔案，方便流通。

**Linux** 可以讓你根據需要**自定義系統**、隨心所欲地安裝 [GUI]([讓使用電腦不再黑白的人生 - GUI 圖形使用者界面 - Engadget 中文版](https://chinese.engadget.com/chinese-2011-04-13-gui.html)) 界面或僅使用「終端」管理伺服器。使用 Linux，您可以選擇各種工具和實用程序來管理所有與伺服器相關的活動，例如：
* 添加用戶
* 管理服務和網絡
* 安裝新應用程式以及監控性能

***
### 正規表達式

* 正規表達式的各種指令可將各種文字中出現的符號或文字用指令去概括起來。
* 應用：在一串文字中取得想要的資訊，例如價錢、日期、評價...等等
* 練習的網站：[Regex101](https://regex101.com/)
* 教學：[正規法教學](https://www.minwt.com/webdesign-dev/html/20352.html4)

**實作練習**：

* 1. 手機號碼：十個字元的數字，前兩個字元是”09” e.g. 0912345678
* 2. 郵遞區號：五個字元的數字，前三個字元是”1-9” e.g. 10087
* 3. 用正規表達法表達下列所有網址 e.g.
transbiz.com.tw/post55688/text
transbiz.com.tw/post58588/text
* 4. 表達IP
192.141.9.3
192.141.7.3
192.141.4.3
* 5. 表達網址
transbiz.com.tw/fb/post01
transbiz.com.tw/fb/post02
transbiz.com.tw/fb/post03
* [我的練習](https://docs.google.com/presentation/d/1qf4LGCV-Uzq3wdccnBVyVN0rAMWRQt-zOYDOZK1_QLs/edit?usp=sharing)
***
### **awk** 與 **sed** 指令的介紹與實作

### 一、awk

### 1. awk語法講解
##### 程式碼
***
**awk [options] ‘scripts’ var=value filename7**
***
#### 在程式碼中：
-F 指定分隔符(可是字串或正規表達法)，預設是空白(space)
-f 從指令碼檔案(awk script)中讀取awk命令
-v var=value賦值變數，將外部變數遞給awkawk [options] 

#### awk 參數
➔\$0 : 當前record（列、橫行）
➔$1~$n : 當前record的第 N 個欄位
➔FS : 輸入field直欄分隔符（-F相同作用）預設空格
➔RS : 輸入record（列、橫行）分割符，預設換行符
➔NF : 欄位個數
➔NR : record 數，就是行號，預設從 1 開始
➔OFS : 輸出欄位分隔符，預設空格
➔ORS : 輸出record分割符，預設換行符9

搭配許多運算子以執行多種動作
[awk的運算子的詳細列表與解釋](http://tw.gitbook.net/awk/awk_operators.html)

### 2. awk print record & field

##### 程式碼：
***
**awk -F “\tab” ‘{print $0}’ fruit.txt**
**awk ‘{print $1, $2, $4}’ fruit.txt**
***
\$0：entire line
\$1：column 1
\$2：column 28

### 二、sed
#### 1.sed 文字分析工具界紹
* **「stream editor 」的縮寫，顧名思義是進行串流 (stream) 的編輯**
* **字串取代、複製、刪除的功能**
* **自動化的修改文字檔**

#### 2.Sed指令
**程式碼：**
***
**sed \[option] ‘\[n1,n2] \[command] / \[pattern] / \[replacement] / \[flag]’ file.txt**
***
* 1. **option**：以 - 符號開頭的功能，如 -n、-r、-i，可省略**n1,n2**：代表開始行數和結尾行數，不輸入代表每行都會執行command
* 2. **command**：進行的動作，如**s, a, c, d, i**
* 3. **pattern**：給command使用的參數
* 4. **replacement**：當使用s指令時會使用
* 5. **flag**：當使用s指令時會使用

[更多關於option、command、pattern、replacement、flag個別的詳細解說與示範：](https://www.1ju.org/sed/sed-basic-syntax)

#### Grep, Awk, Sed比較

**grep:** 可用正規表達法，**找出匹配的內容。**
**sed:** 一次處理一行內容，可搭配正規表達法，可用來**自動編輯一個或多個檔案，** 簡化對檔案的反覆操作。
**awk:** 主要用在對文字和資料進行分析處理，以空格為預設分隔符號，同時也是程式語言，用於**處理有欄位規則的行內內容，並支援格式化輸出**。

[實作練習](https://docs.google.com/presentation/d/1Zmy-b2UdgVuinDmhrsuPwMZLCeYbQtNek85jWbUu_Js/edit?usp=sharing)
____

### **Git flow**

#### Git Flow 分支應用

1. 主要的分支有master、develop、hotfix、release以及feature
2. 各種分支負責不同的功能
3. Master以及Develop這兩個分支又被稱做長期分支，會一直存活在整個 Git Flow 裡
4. 其它的分支大多會因任務結束而被刪除

Master 分支：
* 用來放穩定、隨時可上線的版本。這個分支的來源只能從別的分支合併過來
* 通常會在這個分支上的 Commit 上打上版本號標籤。

Develop 分支
* 所有開發的基礎分支
* 當要新增功能的時候，所有的 Feature 分支都是從這個分支切出去的。而功能完成後，也都會合併回來這個分支。

Hotfix 分支
* 當線上產品發生緊急問題的時候，會從 Master 分支開一個 Hotfix 分支出來進行修復，Hotfix 分支修復完成之後，會合併回 Master 分支，也同時會合併一份到 Develop 分支。* Release 分支。
* 當認為 Develop 分支夠成熟了，就會合併到 Release 分支，在這邊進行上線前的最後測試。

Release 分支
* 測試完後，此分支將會同時合併到 Master 以及 Develop 這兩個分支上。

Feature 分支
* 當要開始新增功能的時候
* Develop 分支來的，完成之後再併回 Develop 分支。

[git flow詳細解說](https://gitbook.tw/chapters/gitflow/why-need-git-flow)

[git flow分支模型圖](https://gitbook.tw/images/tw/gitflow/why-need-git-flow/flow.png)

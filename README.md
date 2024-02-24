筆記內容大部份節錄於[wiki.csie.ncku.edu.tw/linux/schedule](https://)
感謝成大老師的資源分享. 如有問題煩請提醒我刪除. 謝謝

# veginciao

如果你已安裝 Git bash，輸入以下命令以啟動 ssh-agent
# start the ssh-agent in the background
```
$ ssh-agent -s
SSH_AUTH_SOCK=/tmp/ssh-XXXXXXskAzIe/agent.86; export SSH_AUTH_SOCK;
SSH_AGENT_PID=87; export SSH_AGENT_PID;
echo Agent pid 87;
p04@DESKTOP-3OIJSUQ:~$ ssh-add ~/.ssh/id_rsa
Could not open a connection to your authentication agent.
p04@DESKTOP-3OIJSUQ:~$ ssh-agent bash
p04@DESKTOP-3OIJSUQ:~$ ssh-add ~/.ssh/id_rsa
Identity added: /home/p04/.ssh/id_rsa (lo.yuing@gmail.com)
p04@DESKTOP-3OIJSUQ:~$
```

$ git remote add origin git@github.com:你的帳號名稱/你的專案名稱.git
$ git push -u origin master


Rebase 是 "Re-" 與 "Base" 的複合字，這裡的 "Base" 代表「基礎版本」的意思，表示你想要重新修改特定分支的「基礎版本」，把另外一個分支的變更，當成我這個分支的基礎。

我們現在就來做一個簡單的 Rebase 示範，我們大概做幾件事：

切換至 branch1 分支： git checkout branch1
然後執行 Rebase 動作，把 master 當成我們的基礎版本： git rebase master
先切換到 master 分支，然後直接執行 git merge branch1，這時會引發 Git 的快轉機制(Fast-forward)。所謂的「快轉機制」，就是 Git 得知這個合併的過程，其實會依序套用 branch1 原本就有的變更，直接移動到 branch1 的 HEAD 那個版本。
先切換到 master 分支，然後直接執行 git merge branch1 --no-ff 即可。

git rebase 92f9..... -i
![image](https://hackmd.io/_uploads/SJ39h63qT.png)

```
git rebase -i [commit_id]
git commit --amend


---
我重新整理一下本日學到的 Git 指令與參數：

git push origin master
git push -u origin master
git pull origin master
git config --global push.default simple
git push
git fetch
git merge origin/master
git --version
git pull origin master --allow-unrelated-histories
```

>git fetch + git merge origin/master =git pull 
>git push origin master


# Makefile
You need a file called a makefile to tell *make* what to do. Most often, the makefile tells *make* how to compile and link a program.

Makefile 的語法規則：
Makefile 是由很多相依性項目（dependencies）和法則（rules）所組成。
* 相依性項目，描述目標項目（target，要產生的檔案）和產生該檔案之相關的原始碼檔案。
* 法則是說明如何根據相依性檔案，來建立目標項目。
* make 命令分析 Makefile，先決定依序建立哪些目標項目，再決定依序喚起哪些法則。
* 每一個命令前面要有一個[Tab]作為起始行


![image](https://hackmd.io/_uploads/rkSrF92oT.png)


**萬用字元/使用變量**
![image](https://hackmd.io/_uploads/rJrWVjpoa.png)

語法
變數（巨集）定義
可讓我們脫離那些冗長乏味的編譯選項，縮減撰寫 Makefile 的撰寫成本，如︰
OBJECTS= filea.o fileb.o filec.o 
使用時在前面加 $() 的符號，如︰$(OBJECTS)

:=
變數的值決定於它在 Makefile 中的位置，而非整個 Makefile 展開後最終的值

?=
若變數未定義，則替它指定新的值。否則，採用原有的值。
如: FOO ?= bar
若 FOO 未定義，則 FOO = bar；若 FOO 已定義，則 FOO 的值維持不變。

+=
此時 CFLAGS 的值就變成 -Wall -g -O2
> CFLAGS = -Wall -g \
> CFLAGS += -O2

注意事項

```
= 與 ?= 會延後至它們被使用時，才會被展開
:= 則會立即展開右邊的值
```


```
object = foo.o bar.o
all: $(objects)
$(objects): %.o: %.c
    $(CC) -c $(CFLAGS) $< -o $@
```
規則如同以下描述
```
foo.o: foo.c
    $(CC) -c $(CFLAGS) foo.c -o foo.o
bar.o: bar.c
    $(CC) -c $(CFLAGS) bar.c -o bar.o
```
# 自動生成依賴
透過-M 自動搜尋源文件內部包含的'#include'文件,生成依賴文件,例如
```
gcc -M Main.c
會產生
main.o : main.c A.h b.h .....
```


**- [ ] perf**

Perf 能觸發的事件分為三類：

hardware : 由 PMU 產生的事件，比如 cache-misses、cpu-cycles、instructions、branch-misses …等等，通常是當需要瞭解程序對硬體特性的使用情況時會使用。
software : 是核心程式產生的事件，比如 context-switches、page-faults、cpu-clock、cpu-migrations …等等。
tracepoint : 是核心中的靜態 tracepoint 所觸發的事件，這些 tracepoint 用來判斷在程式執行時期，核心的行為細節，比如 slab 記憶體配置器的配置次數等。

!背景知識

記憶體存取很快，但仍無法和微處理器的指令執行速度相提並論。為了從記憶體中讀取指令 (instruction) 和資料 (data)，微處理器需要等待，用微處理器的時間來衡量，這種等待非常漫長。cache 是一種 SRAM，它的存取速率非常快，與微處理器處理速度較為接近。因此將常用的資料保存在 cache 中，微處理器便無須等待，從而提高效能。cache 的尺寸一般都很小，充分利用 cache 是軟體效能改善過程中，非常重要的部分。

硬體特性之cache: pipeline, superscalar, out-of-order execution提昇效能最有效的方式之一就是平行 (parallelism)。微處理器在設計時也儘可能地平行，比如 pipeline, superscalar, out-of-order execution。

branch prediction 指令對軟體效能影響較大。尤其是當微處理器採用管線設計之後，假設 pipeline 有三級，且目前進入 pipeline 的第一道指令為分支 (branch) 指令。假設微處理器順序讀取指令，那麼如果分支的結果是跳躍到其他指令，那麼被微處理器 pipeline 所 fetch 的後續兩條指令勢必被棄置 (來不及執行)，從而影響性能。為此，很多微處理器都提供了 branch prediction，根據同一條指令的歷史執行記錄進行預測，讀取最可能的下一條指令，而並非順序讀取指令









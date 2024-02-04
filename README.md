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
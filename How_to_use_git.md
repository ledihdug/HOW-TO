# **How to use git**

- [Basic Git commands](https://rubygarage.org/blog/most-basic-git-commands-with-examples)  
- [いろいろやらかして困ったとき](http://qiita.com/muran001/items/dea2bbbaea1260098051)

# 最初にやること
## ローカルリポジトリ初期化
これはまあ，説明するまでもなく  
```
$ cd [path]
$ git init
```

## リモートリポジトリ初期化
- ブラウザ内でポチポチする
- **Init Readme.md** のチェックを外しておく

## リモートリポジトリを登録
```
$ git remote add origin git@github.com:hogehoge/hello.git
```
以降originという識別子で`git@github.com:hogehoge/hello.git`を指すようになる  

## リモートリポジトリへの送信とupstreamの追加
まずはmasterブランチにいることを確認する  
```
$ git branch
  * master 
  
$ git push -u origin master
```

## master以外のブランチをリモートリポジトリへ送信する
まずは新たにブランチを作る  
```
$ git checkout -b feature_branch
```
確かにfeature_branchにいることを確認  
そして送信と同時にupstreamの追加  
```
$ git branch
    master 
  * feature_branch
  
$ git push -u origin feature_branch
```

# **リモートリポジトリ**から**clone**して作業を開始するとき
リモートブランチの話はちょっと難しいので以下のURLを参照  
[Git で「追跡ブランチ」って言うのやめましょう](http://qiita.com/uasi/items/69368c17c79e99aaddbf)  

とりあえず**リモートリポジトリ**のURLを拾ってくる  
たとえば**github**の**Linux Kernel** リポジトリ https://github.com/torvalds/linux.git  
それから作業用のディレクトリに移動して以下のコマンドをたたく
```
$ git clone https://github.com/torvalds/linux.git
```
作業する**topicブランチ**がリモートに存在する場合  
作業用のtopicブランチを確認し，  
リモート追跡ブランチが上流のローカルブランチを作る
```
$ git fetch -a
$ git branch -a
   * master
     remotes/origin/HEAD -> origin/master
     remotes/origin/master
     remotes/origin/hogehoge
     
$ git checkout --track origin/hogehoge
```
リモート追跡ブランチが上流にあるブランチを作れたか確認する
```
$ git branch -vv
```

存在しない場合は，上記の[master以外のブランチをリモートリポジトリへ送信する](master以外のブランチをリモートリポジトリへ送信する)を参照する



# 作業サイクル    
- まずはトピックブランチを切れ!! **checkout -b**
- **submodule**使っている場合は**以下参照**
- **push**する前にはリモートリポジトリの更新を取り込む!!
- 取り込む前には**stash**
- それから**fetch**
- さらに**diff**
- それから取り込み，**以下参照**
- それからやっと**push**


## **リモートリポジトリ**から更新を取り込むとき
作業中のファイルは邪魔になるので**git stash**  
[**git stash**の参考](http://qiita.com/fukajun/items/41288806e4733cb9c342)  
```
$ git stash save
```

更新を取り込みたいブランチに移動，もしくは確認
```
$ git checkout topic_branch
$ git branch
    master 
  * topic_branch
  
```
リモートリポジトリの状態をとりこみ差分を確認

```
$ git fetch [origin/<取り込みたいブランチ>]
$ git diff [origin/<取り込みたいブランチ>]
```

=== **NOTE** ==================================  
ここから**marge**するか**rebase**するか考える  
トピックブランチの更新を取り込むなら**rebase**のほうが履歴が綺麗  
しかし，**rebase**は履歴変更可能という**パワー系**コマンドなので  
運用方針で禁止されている場合は**merge --no-ff**を使用すること  
     = =========================================  


## **marge**するとき
```
$ git checkout topic_branch
$ git merge --no-ff [origin/]<取り込みたいブランチ>
```
**conflict**すると自動で**commit**されることはない  
そのときは**conflict**したファイルを開いて直した後に  
```
$ git add <conflictを解消したファイル>
$ git commit -m "merge updata"
```
したら**merge**コミットが適用される  

もし**marge**で**conrlict**して，マージを中止し，元の状態に戻すときは以下のコマンドを使う
```
$ git merge --abort
```



## **rebase**するとき
until

## **リモートリポジトリ**に**push**するとき
until


## ブランチの削除
```
$ git branch -d [削除したいブランチ名]
```

# **submodule**使うとき
## **clone**してきたブランチが**submodule**を含んでいるとき
**submodule**として登録されているディレクトリは**clone**してきたときには空なので  
以下のコマンドをたたく  
このコマンドではサブモジュール内のサブモジュールも再帰的に更新してくれる
```
$ git submodule update --init --recursive
```
## **submodule**を追加するとき
```
$ git submodule add git://example.com/repo.git [ディレクトリを指定したい場合はパスを記入]
```
## **submodule**のリポジトリのブランチを変更するとき
**submodule**のディレクトリに行って個々のリポジトリとして管理する
```
$ cd <submodule>のパス
$ git checkout [利用したいブランチ]
```
あとは**submodule**の変更を親のブランチにも**commit**する必要がある
## リモートにある**submodule**リポジトリの更新を適用するとき
これは簡単で，再帰的に更新したい場合は **--recursive**をつける
```
$ git submodule update [--recursive]
```
## **submodule**を削除する
```
$ git submodule deinit <submoduleのパス>
$ git rm <submoduleのパス>
```



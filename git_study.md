# git_study.md  

## upstream 이란?
fork한 원본 소스를 지칭, 거의 대부분 upstream 라는 명칭으로 지정함.
fork한 소스를 최신화 하기위한 참조용 리포지토리로 사용된다. 푸쉬는 하면 안됨.

---

## 다른 개발자가 pull request 한 것을 취득하고 싶을때.
다른개발자의 수정내용을 레뷰할 경우에 사용하는 명령어

예를들어 
pull request번호가 #457인 feature/abc 브렌치의 수정내용을 pull을 한다면,

```
git fetch upstream pull/457/head:feature/abc
```


## pull request한 내용이 complict되었다면,
github의 pull request목록에서 확인가능하다.

먼저 fetch 를 실행. upstream/develop 에 로컬레포지토리를 최신화 한다.

```
git fetch --all
```

upstream/develop을 원본으로 하여 로컬레포지토리 develop에 pull 을 실행한다.
이 작업으로 로컬레포지토리가 최신화됨. 작업폴더가 develop인 상태에서..

```
git pull upstream/develop
```

로컬develop가 최신화 되었으므로 orgin/develop를 최신화 한다.(origin에다가 push)

```
git push origin/develop
```

이상태에서 내작업브렌치에서 리베이스 실행, rebase는 커밋된 카운트만큼 실행한다.
(applying메세지가 나올때까지)
내 작업 브렌치를 mywork라고 한다면,

```
git rebase develop
```

complict가 된다면 status로 확인한 후 수동으로 머지, 그다음 인덱스에 추가한다.

```
git status

```
```
git add .
```

머지작업이 끝나면 rebase를 진행시킨다.

```
git rebase --continue
```

만약 문제가 생겨 rebase를 중지시키고 싶다면,

```
git rebase --abort
```

완료되면 origin/mywork에 강제로 푸시를 해준다.

```
git push -f origin
```

마지막으로 github홈페이지에서 pull request를 확인 complict가 해결됬는지 확인한다.



---

## .gitignore の設定を反映させる

```
git rm -r --cached .
git add .
git commit -m ".gitignore is now working"
git push origin master
```

## 間違ったブレンチにコミットしてpushまでやってしまった時には

間違ってPushしたのを戻す

```
git reset —soft HEAD^
```

戻したファイル確認

```
git status
```

強制Push(戻したファイルはコミットしてないので対象外になる)
これによってpush前の状態になる。

```
//developの場合
git push -f origin develop
```

新しいブレンチを作成
修正分をベットブレンチへ反映するために

```
//ブレンチ名がbug_fix/xxxの場合
git branch bug_fix/xxx
```

修正分コミット、そしてpush

```
git commit　-m "修正分"
git push origin
```

---

## ブランチとブランチへのRebase

git rebase --onto `くっつけるブランチ` `Rebaseしたいブランチもとのブランチ` `Rebaseしたいブランチ`

例）
```
git rebase --onto master develop unit-test

                    G - H - I(unit-test)
                   /
          D - E - F (develop)
         /
A - B - C (master)

//実行後下記のようになる


          D - E - F (develop)
         /         
A - B - C - (master) - G' - H' - I'(unit-test)

```

---

## 間違ってPushしてしまい、Revertする場合

> revertコマンドとは
> すでにpushされているcommitを打ち消す(もとに戻す)コマンドの事。
> 取り消したいコミットを打ち消すようなコミットを新しく作成する。

```
$ git revert <commit ID>
```

commitしない方法は、-nを指定する。
* 複数のcommitを戻して、1つのcommitとしてpushする場合に便利。*

```
$ git revert <commit ID> -n
```

コミットメッセージを編集しない場合
コミットメッセージを編集しなくていいときは --no-edit を使用する。

```
$ git revert --no-edit <commit ID>
```

---

## コミットをまとめて１つにしてPRする

作業ブランチをチェックアウト

```
$ git checkout -b feature/work origin/develop 
```

git add や commit などして作業完了（コミットが多数生成したとする）

Pull Request用ブランチをチェックアウト

```
$ git fetch
$ git checkout -b feature/work_pr origin/develop
```

作業ブランチをマージ

```
$ git merge --squash feature/work
```

必要な時に手動マージ作業し、Pull Requestに出すコミットを作成

```
$ git commit -m "merged"
$ git push origin feature/work_pr
```

---

## git diffのいろいろ

https://qiita.com/shibukk/items/8c9362a5bd399b9c56be

git pull する前にリモートとの変更点を見る

```
$ git diff HEAD..リモート名/ブランチ名
```

git push する前にリモートとの変更点を見る

```
$ git diff リモート名/ブランチ名..HEAD
```

git add する前に変更点を見る

```
$ git diff
```

git add した後に変更点を見る

```
$ git diff --cached
```

今回コミットした変更点を見る

```
$ git diff HEAD^
```

どれくらい変更したかだけを見る

```
$
git diff --stat
```

ファイル名だけ見る

```
$ git diff --name-only
```

## 絞り込み

git branch | grep 検索文字列


　```
 git branch | grep 検索文字列
 ```
 
 git log --grep 検索文字列
 
```
 git log --grep あああ
 ```
 

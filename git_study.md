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
git rm -r --cached .
git add .
git commit -m ".gitignore is now working"
git push origin master





### 왜 git flow 전략을 사용하는가?

프로젝트의 규모가 커지고 협업하는 인원이 많아지면서 master 브랜치 하나만으로는 프로젝트를 관리하는 데 어려움이 생긴다. 따라서, 개발자들 간의 상호 약속을 정한 방법론이 필요하고, 이 중 가장 많이 사용하고 있는 것이 git flow 전략이다. git flow는 5가지 브랜치를 이용하여 프로젝트를 효율적으로 개발 및 관리할 수 있다. git flow는 최종 배포에 쓰인 master, 배포전 QA를 위한 release, 개발기능이 합쳐진 develop, 기능 단위 개발을 위한 feature, 오류 수정을 위한 hotfix로 이루어진다. 



### git flow의 5가지 전략

**master**

기준이 되는 브랜치

제품 출시

 

**release**

develop에서 개발을 마치고 master에서 출시하기 전에 준비하기 위한 브랜치

QA 작업 수행

 

**develop**

다음 출시 버전을 위해 개발하는 브랜치

개발자들이 이 브랜치를 기준으로 각자 작업한 기능들을 합친다.

출시된 버전에서 발생한 버그들을 수정하여 develop으로 merge

버그를 수정한 커밋들이 상시 추가됨

 

**feature**

단위 기능 개발

개발이 끝나거나 중간에 기능 단위로 원격 저장소에 저장하고 싶다면 publish를 이용

개발이 끝나 기능을 develop으로 merge하고 싶다면 finish를 이용

 

**hotfix**

버그가 생기면 긴급 수정을 위한 브랜치

출시된 버전에서 발생한 버그들을 수정하여 develop이나 master로 merge



### 흐름

1. master branch에서 develop branch 생성

2. 기능 추가시엔 feature branch를 생성하여 진행
3. 개발이 끝났거나 중간에 원격저장소에 저장하고 싶다면 publish를 사용하여 push (생략 가능)
4. 개발이 완료되면 finish를 사용하여 develop으로 merge
5. 버그 발생시 hotfix branch로 버그 수정하고, 해결하면 상황에 따라 develop이나 master로 merge
6. 출시하기 전에 develop branch를 release branch로 보내서 QA 진행
7. release branch에서 QA가 완료되면 master branch로 merge 하여 배포



### git flow 구조

![img](https://blog.kakaocdn.net/dn/MjcR5/btqJDYR3eyc/cqHG5sSh683fEyVqToXlSk/img.png)



### git flow 명령어

1. develop 브랜치 생성

   -d를 붙이면 develop이라는 이름의 브랜치 생성된다.

   ```bash
   $ git flow init -d
   ```

2. feature branch 생성

   ```bash
   $ git flow feature start 브랜치명
   ```

3. feature branch에서 stage로 올리기

   ```bash
   $ git add .
   $ git commit -m 'message'
   ```

4. 

   1. feature branch를 remote로 원격저장소에 저장

      ```bash
      $ git flow feature publish 브랜치명
      ```

   2. feature branch에서 develop브랜치로 merge하고 feature branch 삭제

      ```bash
      $ git flow feature finish 브랜치명
      ```

   3. merge된 develop branch에서 원격 저장소에 저장

      ```bash
      $ git push origin develop
      ```

      

### hotfix

hotfix는 이슈를 해결하기 위한 브랜치이다. hotfix finish를 하면 develop과 master로 병합이 된다.

no tag 경고 메시지가 뜨는데 아래 코드를 적용하면 더이상 뜨지않고 정삭적으로 develop과 master에 병합된다.

```
git config --global gitflow.release.finish.notag true
git config --global gitflow.hotfix.finish.notag true
```



#### 참고

> https://woowabros.github.io/experience/2017/10/30/baemin-mobile-git-branch-strategy.html
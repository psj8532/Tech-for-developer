## 일반 레포지터리 미러링

1. 복사할 레포지터리를 가져온다.

   ```bash
   git clone --bare https://gitlab.com/exampleuser/old-repository.git
   ```

2. 레포지터리 이동 후 붙여넣기 할 레포지터리에 푸쉬한다.

   ```bash
   cd old-repository.git
   git push --mirror https://github.com/exampleuser/new-repository.git
   ```
   
   



## 대용량 파일 포함 레포지터리 

github에 100MB가 넘는 파일의 `커밋`이나 `히스토리`가 있을 경우, `push`가 거부된다. 따라서 미리 제거해줘야한다.

**Git lfs**와 **BFG Cleaner**를 이용하는 방법이 있다. 하지만 내 경우엔 git lfs 명령어가 제대로 먹히지 않았고, 실제로 해결이 안됐다는 후기도 많았다. 그래서 BFG Cleaner 방법을 이용했다.

### BFG Cleaner

1. 복사할 레포지터리를 가져온다.

   ```bash
   git clone --mirror <https://gitlab.com/exampleuser/old-repository.git>
   ```

2. BFG Cleaner를 설치한다.

   https://rtyley.github.io/bfg-repo-cleaner/

3. 용량이 큰 파일을 찾고, 히스토리까지 지워준다.

   ```bash
   # 클론했던 디렉토리에서 진행
   java -jar ~/downloads/bfg-1.14.0.jar --strip-blobs-bigger-than 100M s03p31a307.git
   ```

   




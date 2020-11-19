### 목적

보안상의 이유 등으로 특정 파일을 git의 관리 대상에서 제외시켜야 할 경우가 있다. 이때, .gitignore에 추가해주면 local에는 존재하지만 git의 관리 대상에서는 제외되어 git 저장소에는 추가되지 않는다

 

### 만들기

폴더 최상단에 .gitignore 파일을 만들어야한다.

 

### 적용하기

처음부터 gitignore를 만들고 시작하면 push할때, 바로 적용된다. 하지만 이미 만들어진 프로젝트에서 적용하려면 git에 있던 정보를 지우고 다시 적용해야된다.

```bash
# 정보 지우기
git rm -r --cached
git add .
git commit -m 'Apply .gitignore'
```
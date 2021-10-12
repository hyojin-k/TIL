# git branch 명령어 

##local에서 branch 생성하기

### branch 생성
```
git branch <브랜치명>
```

### branch 이동
```
git checkout <이동하려는 브랜치명>
```

**branch 생성과 함께 해당 브랜치로 이동하기**
```
git checkout -b <브랜치명>
```

### git remote branch 생성
```
git push origin <브랜치명>
```

### local remote 연동
```
git branch --set-upstream-to origin/<브랜치명>
```


### branch 삭제
- #### local branch 삭제
```
git branch -d <브랜치명>
```
- #### 원격 branch 삭제
```
git push origin --delete <브랜치명>
```

## NOTE

---

![image](https://user-images.githubusercontent.com/74589585/192918577-c18f6307-a7fc-4e51-9c4d-d222693652f1.png)

한글로 파일이름을 작성하면 아마 이런식으로 파일명이 나옵니다. (폴더명 또한 같아요)

[GITDocs링크](https://git-scm.com/docs/git-config#Documentation/git-config.txt-corequotePath)

## GIT : 한글이잖아? "usual" 하지 않다 이 문자는 "unusual"한 문자로 표시함!

원인은 깃이 파일 경로(path)를 출력하는 명령어가 실행될 때 한글 인코딩이 UTF-8에 들어가기 때문에

0x80 보다 큰 바이트를 가진 비정상적인 문자로 인식하고 처리해서 그래요.

git에서 변수 설정을 변경해서 처리할 수 있는데

`core.quotePath` 변수를 false로 설정하면

이 변수가 false로 설정되면 0x80보다 높은 바이트는 더 이상 "비정상적"으로 간주되지 않습니다.

git 명령어

```
git config --global core.quotepath false
```

![image](https://user-images.githubusercontent.com/74589585/192919498-d7fc468b-a5cc-4a6e-8905-a09dceb248c7.png)

실행하고 status 확인해보면 변경되어 있습니다.

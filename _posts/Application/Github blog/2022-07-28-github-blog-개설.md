---
layout: post
title: github blog 개설 방법
date: 2022-07-28 03:02 +0900
categories: [Application, Github blog]
toc: true
---
# １. github 블로그 개설 방법

[초보자를 위한 GitHub Blog 만들기 - 1
](https://wlqmffl0102.github.io/posts/Making-Git-blogs-for-beginners-1/)

위 링크는 이 블로그를 개설할 때 참고한 21년 10월 16일 게시글이다. 이미지가 많지 않아 왕초보에겐 적합하지 않을 것 같다..  
**window, 64bit** 기준, **vsc, github desktop** 앱을 사용한다.


위 블로그 링크와 다르게 한 점은 ruby 다운 받을 때 제일 최신 버전을 이용하였다.  
나중에 찾아보니 jekyll theme가 구버전과 호환이 된다는 글이 있으니, 블로그 글 그대로 이용하는 게 좋겠다. 근데 나는 아직 호환이 안되는 문제는 없다


나는 chirpy theme를 적용했다. 
[chirpy theme link](https://jekyll-themes.com/chirpy/)  
이 테마에서 맘에 든 점은
- 왼쪽 카테고리창을 고정할 수 있는 기능
- 우측에 카테고리 기능
- 동적으로 크기 조절

그 외에 맘에 든 테마는 이 [테마](https://jekyll-themes.com/prologue/).. 근데 많은 글을 쓰는 블로그엔 적합하지 않는 듯함

# ２. 오류 발생 사항
## ２.１  Conflict: c:/github exists and is not empty.
jekyll new . 할 경우 
Conflict: c:/github exists and is not empty. 이런 식의 에러가  났다. 
`jekyll new . --force` 하면 된다. 이 명령어를 쓰면 폴더를 강제로 덮어쓰게되는데 문제 없다

## ２.２ `require': cannot load such file -- webrick (LoadError)
루비 cmd 창에 `bundle add webrick` 명령어를 친다. 

([참고링크](https://junho85.pe.kr/1850))

# ３. 추가 팁
## ３.１ VSC를 마크다운 편집기로 사용하는 방법
`Markdown All in One` 플러그인을 설치해서 본다.

([참고링크](https://sianux1209.github.io/etc/markdown_editor_vscode/))



근데 vsc로 md를 편집하려니 한쪽은 문서창 한쪽은 md viewer창으로 나눠서 봐야돼서 불편했다..
원래 md 문서 편집기로 typora를 썼는데 유료화가 돼서

지금은 급한대로 obsidian을 설치해서 쓰고 있다.
obsidian은 한글로 된 자료가 거의 없고 사용법을 보려면 영어 커뮤니티를 뒤져야한다 ㅎ


# ４. 의문점
![](image-20220801141040794.png)

chirpy 테마에서는 게시물 오른쪽 옆에 목차가 붙는다. (정식용어는 Table Of Contents를 줄여서 toc라고 부른다)   
jekyll에서 샘플로 주어진 게시물에서는 스크롤할 때마다 목차가 움직이는데   
내가 작성한 게시물엔 목차가 안움직여서 계속 찾아봤더니

```
# 안녕?    // 목차가 정상적으로 움직임
# 1. 안녕? // 앞에 숫자를 붙이면 목차가 움직이지 않음
# １. 안녕? // 야매 방법(ㅈ+한자)으로 숫자를 붙여서 목차를 움직임
```

태그 옆에 숫자를 붙이면 목차가 안움직인다... 해결방법은 못찾겠다 ㅠ
일단 ㅈ+한자를 누르면 숫자 이모티콘을 사용할 수 있는데 이 방법으로 넘버링을 하기로 결정.. 
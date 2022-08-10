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

<br/>   

위 블로그 링크와 다르게 한 점은 ruby 다운 받을 때 제일 최신 버전을 이용하였다.  
나중에 찾아보니 jekyll theme가 구버전과 호환이 된다는 글이 있으니, 블로그 글 그대로 이용하는 게 좋겠다. (근데 나는 아직 호환이 안되는 문제는 발생하지 않았다)

<br/>  

또한 댓글 기능으로 disqus를 이용하지 않고 **utterance** 를 이용했다.  
disqus는 무겁고 광고가 많이 뜬다는 단점이 있다  
utterance 댓글 연동은 이 블로그([링크](https://www.irgroup.org/posts/utternace-comments-system/))가 잘 설명해주고 있다  

<br/>  

나는 chirpy theme를 적용했다. 
([chirpy theme link](https://jekyll-themes.com/chirpy/)  )  
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

## ２.３--- layout: home # Index page ---

로컬 환경에서는 테마가 정상적으로 적용되는데  
웹사이트에서는 --- layout: home # Index page --- 이런 텍스트(index.html 파일 내용)만 뜨는 경우이다.  

![](https://sonmansu.github.io/images/2022-07-28-github-blog-개설/img-220803-012701-955.png)


본인 깃헙 블로그 레포지토리에서 Setting - Pages에 가면 Source에서 Branch를 바꿀 수 있는데     
여기서 gh-pages, /(root)를 선택하고 Save를 누른다.  
3-5분 기다리면 블로그가 정상적으로 뜬다

## ２.４ 404 error
깃헙 레포 visibility를 private으로 바꿨다가 블로그가 정상적으로 안떠서 (private으로 블로그를 운영하고 싶으면 enterprise plan을 써야한다고함..)   
public으로 다시 바꿨더니 404 에러가 발생했다.

![](https://sonmansu.github.io/images/2022-07-28-github-blog-개설/img-220803-012712-955.png)

본인 깃헙 블로그 레포지토리에서 Setting - Pages에 갔더니 Branch 설정이 풀려있어서 다시  
gh-pages, /(root)를 선택하고 Save를 눌렀다.  

그래도 여전히 404 에러가 떴다...


검색해보니 현재 블로그 코드를 commit후 push를 하면 접속이 된다고 한다.  
아마 푸시가 발생할때 github pages 에서 빌드가 발생하는 거 같다고 한다..  
그러나 이 방법으로 되지 않았다.

내가 해결한 방법은  
https://[사용자명].github.io/ 뒤에 index.html을 붙였더니 페이지에 접속이 됐다.  
이 이후로는 index.html을 붙이지 않아도 접속이 정상적으로 된다. 


## ２.５ 이미지가 뜨지 않음 
구글에 지킬 이미지 넣기를 검색해보면  
다들 루트 폴더에 images폴더를 생성해 이미지를 넣고  
```
![](/images/사진.jpg) 
```
이런 식으로 이미지 주소를 상대경로로 지정하는 데 나는 죽어도 사진이 안떴었다..  
아래처럼 깃헙 주소까지 포함해서 절대 경로로 지정해주는 경우에만 사진이 제대로 떴다.
```
![Image8](https://sonmansu.github.io/images/의자.jpg)  
```

<br/>
하지만 이미지 경로를 일일히 지정해주는 게 귀찮아서..  
지킬 블로그 설명 문서를 다시 읽어보다가 해결 방법을 찾아냈다.  

_config.yml 파일에
```
# img_cdn: 'https://raw.githubusercontent.com/cotes2020/chirpy-images/main'
```
img_cdn을 주석시키면 된다.  
이 cdn 주소가 '/'가 붙은 모든 경로 앞에 붙어있었기 때문에 이미지가 안떴었던 것이다.  

<br/>
<br/>
위 주소를 주석시키고 나면  
avatar(대표사진으로 쓰일 이미지 파일) 경로를 재지정하라는 오류가 뜨는데 
그거는 avatar에 지정돼있던 이미지가 위 경로에서 가져온 이미지 이기 때문이다.  

_config.yml 에
avatar 경로를 재지정 해준다. 일반적으로 `/assets/img/` 폴더에 이미지를 넣고 불러 쓴다.

```
avatar: '/assets/img/myicon.png'
```


# ３. 추가 팁
## ３.１ VSC를 마크다운 편집기로 사용하는 방법
`Markdown All in One` 플러그인을 설치해서 사용한다.

([참고링크](https://sianux1209.github.io/etc/markdown_editor_vscode/))




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
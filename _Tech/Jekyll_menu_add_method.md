---
title: "[Jekyll] Git page category menu 추가 방법 - Basically Basic theme"
---

현재 github page의 테마로 [Basically Basic Theme](https://mmistakes.github.io/jekyll-theme-basically-basic/)을 사용중이다.  
아래와 같이 홈페이지의 메뉴를 추가하는 방법을 확인해 보자.

![My Git Page Menu](/assets/images/my_page_menu.jpg)


Jekyll은 기본적으로 Markdown, Liquid, HTML & CSS로 구성되어 있어, 어느 것도 익숙하지 않은 내게는 어디서 부터 손대야 할지 막막할 때가 많다.
기본적으로 모든 Theme가 유사한 구조를 가지고 있다. 아래의 3단계 스탭을 통해서 어떻게 진행하는지 확인해 보자.
아래의 예시에서는 만들고자 하는 메뉴 이름이 'Tech'이다.

Basically-Basic theme은 아래의 폴더 구성을 가지고 있으니 참고 하자!  

* File directory hierarchy  
![File directory hierarchy](/assets/images/hierarchy.bmp)

### 1. Tech.md 파일 생성, _Tech 폴더 생성  
 아래와 같은 형식의 Tech.md 파일을 root directory에 생성하고 _Tech 폴더를 생성한다.

- Tech.md 파일

```
---
title: IT & Tech
layout: collection
permalink: /Tech/
collection: Tech
entries_layout: grid
---

IT & Tech tips for you!
```

### 2. _data folder의 theme.yml 파일 수정  
theme.yml 파일의 navigation_pages에 Tech.md 파일 추가  
(실제로 홈페이지의 메뉴에 표시해 주는 역할을 한다.)

```
navigation_pages:
  - about.md
  - cv.md
  - algorithms.md
  - Tech.md
```

### 3. _config.yml 파일 수정:
Collections 항목에 Tech를 추가해 준다.  
(생성된 메뉴에 _Tech 폴더의 내용을 링크를 연결해 표시해 준다.)

```
# Collections
collections:
  Tech:
    output: true
    permalink: /:collection/:path/
```

defaults에 Tech path와 type을 설정해 준다.  
(단순한 HTML 페이지에서 default thema를 입혀주는데 필요하다)

```
defaults:

# 단순한 HTML 페이지에 default sheme을 입혀주는데 필요
  - scope:
      path: "_Tech"
      type: Tech
    values:
      layout: post
      read_time: true

```

자신이 사용하는 Jekyll의 theme에 따라 defaults.html이 없다던지, theme.yml의 위치가 변경되던지 작은 변경 사항은 있을 수 있다. 하지만, 기본적으로 위의 구조만 이해할 수 있다면 적용이 어렵진 않을 것이다.

---
title:  "Github 블로그 HOWTO - [5]"
search: true
categories: 
  - Blog
tags:
  - Customizing
  - Minimal Mistakes
  - main.scss
  - Stylesheets
  - table of contents
date: 2024-01-04   
last_modified_at: 2024-01-04
excerpt_separator: 
---
블로그 테마를 수정하는 것은 상당히 다양하고 개인의 취향과 목적에 따라 크게 달라진다. 따라서 이번에는 Minimal Mistakes 테마를 직접 커스터마이징한 부분을 중점으로 다루려고 한다.

### 1. Stylesheets
Minimal Mistakes 테마는 `_sass/` 디렉토리 내부의 여러 SCSS 파일에 나뉘어 작성되어 있다.

```shell
<your project>
├── _sass
|  └── minimal-mistakes
|     ├── skins
|     |   ├── _air.scss, ...   # skin theme
|     ├── vendor               # vendor SCSS partials
|     |   ├── breakpoint       # media query mixins
|     |   ├── magnific-popup   # Magnific Popup lightbox
|     |   └── susy             # Susy grid system
|     ├── _animations.scss     # animations
|     ├── _archive.scss        # archives (list, grid, feature views)
|     ├── _base.scss           # base HTML elements
|     ├── _buttons.scss        # buttons
|     ├── _footer.scss         # footer
|     ├──  ...                 # 생략
├── assets
|  ├── css
|  |  └── main.scss            # main stylesheet, loads SCSS partials in _sass
```
<br/>
테마의 스타일을 수정하는 데에는 주로 두 가지 방법이 있다. 첫 번째는 속성이 정의된 파일을 직접 편집하는 것이며, 두 번째는 `'프로젝트 디렉토리'/assets/css/main.scss`(이하 main.scss) 파일에 Sass 변수나 속성을 재정의하여 덮어쓰는 방식이다. 여기서는 수정한 내용을 별도로 관리하기 위해 `main.css`에 변수를 작성하는 방식으로 진행한다. 이를 통해 기존 파일을 유지한 채 필요한 부분만을 수정할 수 있다.
 
테마의 링크 색상을 바꾸고 싶다면, `main.css`에 해당 변수`($link-color)`를 설정해서 변경하면 된다. 예를 들어 'red'로 설정하면 기존의 설정 값을 덮어쓰고 링크 색상이 빨간색으로 바뀌게 된다. 변수를 설정할 때는 @import 문 이전에 두고, 설정된 변수를 통해 속성을 변경하는 설정은 @import 문 이후에 배치한다. 그러면 변수 설정이 먼저 이뤄지고, 그 값을 이용해 속성을 변경할 수 있게 된다.

``` scss
//    main.scss
@charset "utf-8";

$link-color: red;  
{% raw %}
@import "minimal-mistakes/skins/{{ site.minimal_mistakes_skin | default: 'default' }}"; // skin
@import "minimal-mistakes"; // main partials
{% endraw %}
```


### 2. 테마 색상 수정

`mint` 스킨을 기본 테마로 선택했기 때문에, 기본 색상 구성은 주로 `mint.scss` 파일에 정의되어 있다. 그러나 앞서 말한대로 배경색 등 관련된 변수들을 `main.scss`에서 재정의했다. 브라우저를 새로고침하면 변경된 색상이 반영된 화면이 표시된다. <br>  

```scss
//    main.scss
// Colors -- @import 이전에 배치 
$background-color: #ffffff !default;
$primary-color: #358CA7 !default;
$footer-background-color: #016172 !default;
$link-color: #358CA7 !default;
```
![색상 수정후 스크린샷](/assets/images/screenshot/color_changed.png){:class="align-center" width="80%" } 

### 3. Content 영역의 폭 조정

Minimal Mistakes의 `single` 레이아웃에서는 `default`와 `wide` 두 가지 옵션이 가능하다.   
default 설정에서는 본문 영역인 `content`를 중심으로 양쪽에 `sidebar`가 배치되어 있다. content 영역의 기본 설정 폭이 좁아서 조금 답답한 느낌이 들 수 있다. wide로 설정하면 content 영역이 넓어지지만, 이에 따라 오른쪽에 보이는 목차(Table of Contents)가 content 영역 상단 고정되어 표시된다. 현재 사용중인 Table of Contents의 기능을 유지하기 위해 default 설정에서 content 영역을 확대하려고 한다.  <br/>
#### 3.1. sidbar 폭 줄이기

sidebar의 폭을 줄이면 상대적으로 content 영역이 넓어진다. `_variables.scss`에 있는 기본값을 참고해서 적절한 값으로 조정한다.  

```scss
//    main.scss
// Grid -- @import 이전에 배치 
$right-sidebar-width-narrow: 180px !default;
$right-sidebar-width: 270px !default;
$right-sidebar-width-wide: 360px !default;
```
#### 3.2. $max-width 재정의
default 설정에서 `$max-width`는 1280px로 정의되어 있다. 따라서 브라우저 창 크기를 키워도 content 영역의 폭이 일정 수준 이상으로 커지지 않는다. 이를 원하는 수준(예시:1440px)으로 변경한다.  

```scss
//    main.scss
// Breakpoints -- @import 이전에 배치 
$max-width: 1440px !default; 
```

#### 3.3. content와 sidebar 사이의 간격 조정
다음은 content와 sidebar 사이 간격을 조정하기 위한 설정이다.
```scss
 //  오른쪽 사이드바의 패딩 설정 -- @import 이후에 배치 
.sidebar__right {
    @include breakpoint($large) {
        padding-left: 1.5em;  // 숫자가 커지면 간격이 커짐 
    }
}
```

### 4. TOC(Table of Content)
게시글을 작성하면 제목들이 수집되어 목차가 자동으로 생성된다. 이 기능을 활용하려면 YAML Front Matter에  사용 여부를 설정하면 된다. 목차 기능은 모든 게시글에 공통으로 사용되므로, 아래의 예시처럼 `_config.yml`에 파라미터들을 추가한다. 

#### 4.1. _config.yml 설정
Table of Contents 기능을 사용하려면 toc 속성을 true로 설정해준다. 아이콘은 [Font Awesome](https://fontawesome.com/v5/search?s=solid&m=free)에서 제공하는 아이콘으로 대체할 수 있고, `toc_label`에는 타이틀을 입력한다. 
```yml
# Defaults
defaults:
  - scope:
      path: ""
      type: posts
    values:
      layout: single
# ... 중략  
      toc: true                 # toc를 사용하려면 true로 설정
      toc_sticky: true          # toc 위치를 화면에서 고정시키려면 true로 설정
      toc_icon: list            # toc의 아이콘 설정
      toc_label: 컨텐츠 개요      # toc의 타이틀 설정
```  

#### 4.2. TOC 스타일 수정
나머지 스타일은 `main.css`에서 관련 속성 값을 변경한다.   

```scss
//  TOC의 스타일 설정 -- @import 이후에 배치 
.toc {
    .nav__title {  //table head 영역
        background: $primary-color;
        text-align: center;
    }
    .active a {                         
        @include yiq-contrasted(#ffffff); 
        color: $primary-color;            
    }
}
```

### 5. 블로그 헤더 
#### 5.1. 이미지 설정
헤더 영역 이미지는 overlay_image 속성에 이미지 URL을 입력하여 설정한다. YAML Front Matter 영역 또는 _config.yml에서 설정할 수 있다.
```yml
header:
  overlay_image: /assets/images/image.jpg     # 배경 이미지
  overlay_filter: rgba(100, 255, 255, 0.05)   # 필터 설정
  caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
```
#### 5.2. 헤더의 높이
헤더에는 제목, 블로그 요약(excerpt), 날짜 정보 등이 표시된다. 헤더의 높이는 이 내용들의 길이에 따라 **자동**으로 결정된다. 보통 제목과 날짜 정보의 높이는 거의 고정적이므로, 블로그 요약문의 길이가 헤더의 높이를 결정하는 주된 요인이다. 요약문은 본문 내용의 일부분이고, 원하는 길이의 요약문을 얻기 위해서는 excerpt_separator 속성을 설정하여 길이를 조절할 수 있다. 

요약문의 길이가 결정되면, 요약문의 영역의 너비와 글자 크기를 수정하여 헤더의 높이를 어느 정도 조정할 수 있다.

```scss
.page__hero {
    &--overlay {
        .page__lead { //요약문 표시 영역
            max-width: 768px;
            font-size: 0.9em;
        }
    }
}
```

### 6. 기타
다음은 검색창 키워드의 글자 크기를 바꾸고, `<a>` 태그의 밑줄을 제거하기 위한 설정이다. 그외의 글자 크기나 색상 등 소소한 변경은 생략하기로 한다. 
```scss
// 검색 키워드 글자 크기
.search-content .search-input {
    font-size: 1.2em !important;
}
//  모든 링크의 밑줄 제거
a {
    text-decoration: none !important;
}
```
<br/>

------
>**참고한 글**  
> 
> 기록으로 남겨주셔서 감사합니다. 덕분에 이 글이 완성됐어요.  &nbsp; <i class="fa fa-gift" style="color: MediumVioletRed"></i> 
 1. [Minimal Mistakes Guide - Stylesheets](https://mmistakes.github.io/minimal-mistakes/docs/stylesheets/)  
 2. [Personal Website with Minimal Mistakes Jekyll Theme HOWTO - Part II](https://www.cross-validated.com/Personal-website-with-Minimal-Mistakes-Jekyll-Theme-HOWTO-Part-II/)  

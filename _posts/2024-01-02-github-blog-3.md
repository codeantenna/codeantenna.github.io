---
title:  "Github 블로그 HOWTO - [3]"
search: true
categories: 
  - Blog
tags:
  - YAML Front Matter
  - _config.yml
  - tzinfo
  - tzinfo-data
date: 2024-01-03
last_modified_at: 2024-01-03
excerpt: 
---
Minimal Mistakes 테마가 완벽히 설치됐으니, 현재 진행 상황을 파악하기 위해 간단한 글을 작성하고 포스팅하기로 한다. 

### 1. 샘플 게시글 작성하기

게시물은 _posts 디렉토리에 저장되며, 파일 이름은 'YEAR-MONTH-DAY-title.md' 형식을 따라야 한다. 여기서 YEAR는 글 작성 년도, MONTH는 월, DAY는 일을 나타내며, title은 게시글 제목을 나타낸다. 이 파일 이름 규칙을 준수해야 Jekyll이 해당 파일을 블로그 글로 인식하고 게시할 수 있다.  

또한, 각 글의 상단에는 Front Matter가 있어야 하는데, 이 부분에는 게시글의 정보(레이아웃, 제목, 날짜, 카테고리 등)가 포함되어야 한다. Front Matter는 `'---'`로 시작하여 `'---'`로 끝나는 구간이고, 그 안에 YAML 형식으로 정보를 작성해야 한다.

아래 그림을 참조하여 단계별로 샘플 게시글을 작성해보자. <br/> <br/>
![샘플포스팅](/assets/images/screenshot/sampleposting1.png){:class="align-center"  width="90%" } 
- 프로젝트 내에 `_posts` 폴더를 생성한다. ('프로젝트 디렉토리'/_posts)
- _posts 내에 파일을 생성하고, 이름은 `'YYYY-MM-DD-title.md'`로 설정한다. 
- 프론트 매터(Front Matter) 영역에 `title`을 설정한다. <br/> <br/>
 
로컬에서 실행 중인 브라우저를 새로고침하면 새로운 게시글이 보인다. 이 게시글의 링크를 클릭하면 텍스트 파일이 렌더링되어 화면에 나타나는데, 여기서 작성한 내용과 비교하면 텍스트 이외의 요소들이 미리 설정되어 있는 것을 확인할 수 있다. 설정된 요소들은 템플릿이나 기본 레이아웃 등이다.

![샘플포스팅](/assets/images/screenshot/sampleposting2.png){:class="align-center"  width="100%" }


### 2. YAML 프론트 매터(Front Matter)
YAML 프론트 매터(Front Matter)는 파일의 맨 위에 `'---'`로 구분된 블록으로 배치된다. 이 블록을 포함하는 모든 파일은 Jekyll에 의해 특별하게 처리된다. 프론트 매터 안에서는 미리 정의된 변수를 설정하거나 사용자가 만든 변수를 사용할 수 있는데, 이를 통해 파일의 설정이나 데이터를 유연하게 조작할 수 있다.  <br/><br/>
이 블로그에서 자주 사용하는 변수들은 아래와 같다. 각각의 게시글 파일마다 변수를 다르게 설정할 수 있다. 하지만 모든 게시글에 공통적으로 필요한 변수들은 반복해서 작성하는 대신 `_config.yml` 파일에 추가하면 동일한 효과를 얻을 수 있다. 이를 통해 파일들 간 설정의 일관성을 유지하고, 관리를 효율적으로 할 수 있다. 만일 변수 설정이 중복되는 경우, 마크다운 파일에 있는 변수 설정이 우선적으로 적용된다. 

``` yml
---
title:  게시글 제목
excerpt: 게시글 요약문
search: true          # 게시글이 검색 결과에 나타나도록 설정
categories:           # 카테고리 목록 작성
  - blog
tags:                 # 태그 목록 작성
  - Github
  - Jekyll
date: 2023-12-22               # 포스팅 시간
last_modified_at: 2023-12-22   # 업데이트 시간
toc: true             # 목차 (Table of Contents) 사용    --> _config.yml로
toc_sticky: true      # 목차를 화면에서 고정된 위치에 배치   --> _config.yml로
header:               # 페이지의 상단에 이미지 설정         --> _config.yml로
  overlay_image: /assets/images/pic.jpg
---
```

### 3. Jekyll의 설정 파일 (_config.yml)
`_config.yml`은 웹사이트의 전반적인 동작과 외형을 결정하는 데 사용된다. 이 파일에서 사이트 정보, 테마, 플러그인 등의 정보를 설정하면, 웹사이트 전체에 영향을 미친다.
`_config.yml`에는 설정에 대한 예제와 기본값이 설명과 함께 제공되어 있어서 설정들을 변경하거나 새로운 설정을 추가하기가 비교적 쉽다. 변경 후에는 사이트를 다시 빌드해서 변경사항이 적용되도록 해야 한다. 즉 서버를 껐다가 다시 구동시키는 과정이 필요하다. <br/>  
테마 스킨, 사이트 기본 설정, 저자 정보 등 쉽게 찾을 수 있는 설정부터 바꿔보기로 한다. `date_format` 설정은 [strftime 테이블](https://www.webisland.agency/blog/how-to-format-dates-in-jekyll/)을 참조하여 날짜 형식을 새로 지정했고, `remote-theme`이 제대로 적용되도록 관련 plug-in을 추가하였다. 나머지 사이트 정보 및 기타 세부 정보를 입력한다.

```yml
# Theme Settings - 테마 설정
remote_theme             : "mmistakes/minimal-mistakes"
minimal_mistakes_skin    : "mint"   # 스킨 변경
```
``` yml
# Site Settings - 사이트 설정
locale                   : "ko-KR"            # 언어 설정
date_format              : "%Y년 %m월 %d일"    # 날짜 형식 변경을 위해 '새로 추가'
title                    : "XXX"    # 사이트 탭에 표시되는 타이틀
name                     : "XXX"    # 화면 하단에 표시되는 이름
description              : "XXX"    # 사이트 소개글
search                   : true     # 검색 기능 사용
```
```yml
# Site Author - 사이트 저자 소개
author:
  name             : "XXX"
  avatar           : "/assets/images/pic.jpg"
  bio              : "XXX"
  location         : "대한민국"
  email            :
  links:
    - label: "Email"
      icon: "fas fa-fw fa-envelope-square"
      url: "mailto:your.name@email.com"
```

```yml
# Plugins (previously gems:)
plugins:
  - jekyll-remote-theme
```

```yml
# Outputting
timezone: Asia/Seoul  # 대한민국 표준시로 변경 
```

<br/>
설정을 변경한 후에는 반드시 서버를 재시작해야 하는데, 이때 설정이 제대로 적용되지 않으면 문제가 발생할 수 있다. 서버를 재시작하니 `Dependency Error`가 발생했고, 그것이 `tzinfo`와 관련이 있다면, 이는 일반적으로 시간대(Timezone) 라이브러리와 관련된 문제일 가능성이 있다.

``` shell
D:\realBlog>bundle exec jekyll serve 
Configuration file: D:/realBlog/_config.yml
  Dependency Error: Yikes! It looks like you don't have tzinfo or one of its dependencies installed. In order to use Jekyll as currently configured, you'll need to install this gem. If you've run Jekyll with `bundle exec`, ensure that you have included the tzinfo gem in your Gemfile as well. The full error message from Ruby is: 'cannot load such file -- tzinfo' If you run into trouble, you can find helpful resources at https://jekyllrb.com/help/!
jekyll 4.3.2 | Error:  tzinfo
# 생략
```

<br/>
해당 문제를 해결하기 위해서는 먼저 `tzinfo`와 관련된 Gem의 버전을 확인하고, 최신 버전으로 업데이트하거나 필요한 버전을 명시적으로 설치해야 한다. 여기서는 `Gemfile`에 필요한 의존성을 추가하기로 한다.

``` shell
gem "jekyll-remote-theme"  # remote-theme 관련
gem 'tzinfo'                
gem 'tzinfo-data'
```
<br/>
다시 서버를 시작하니, `mint`스킨이 적용된 화면에서 언어 설정은 한글로 변경되어 있다. 검색 아이콘이 오른쪽 상단에 표시되었고, `hello'라는 키워드에 대한 검색 결과가 정상적으로 나타난다. 이 외에도 바뀐 내용이 제대로 적용됐는지를 꼼꼼하게 확인한다.  <br/><br/> 
![설정 변경 후](/assets/images/screenshot/configure_changed.png){:class="align-center"  width="100%" }

<br/> 
공개할 글이 준비되면 `git push`를 실행하여 로컬에서 작업한 내용을 서버에 업데이트한다. 웹에서의 화면과 로컬에서의 화면이 동일한지 비교해보고, 이렇게 함으로써 로컬에서의 변경사항이 서버에 적용됐음을 알 수 있다.<br/> <br/> 

------
>**참고한 글**  
> 
> 기록으로 남겨주셔서 감사합니다. 덕분에 이 글이 완성됐어요.  &nbsp; <i class="fa fa-gift" style="color: MediumVioletRed"></i> 
 1. [Minimal Mistakes Quick-Start Guide](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/)  
 2. [GitHub Pages 블로그 따라하기](https://devinlife.com/howto/)  

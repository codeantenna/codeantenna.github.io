---
title:  "Github 블로그 HOWTO - [2]"
search: true
categories: 
  - Blog
tags:
  - Github Repository
  - Jekyll
  - Minimal Mistake Theme
  - git 명령어
date: 2024-01-02
last_modified_at: 2024-01-02
excerpt: 
---
로컬에서의 환경이 준비됐다면, 블로그가 실제로 운영될 저장소인 Github Repository 설정과 Jekyll theme에 대해 알아볼 차례이다.

### 1. Git Repository 생성하기
Github Pages로 공개된 블로그를 웹에서 볼 수 있도록 하려면 **`Public`** 상태로 설정되어야 한다. 이 설정은 Github repository에 업로드된 모든 코드들을 누구나 자유롭게 사용할 수 있다는 것을 의미한다. Private으로 설정하면 방문자의 사용 권한을 제한할 수 있지만 이에는 추가 비용이 발생할 수도 있다.
- [Github](https://github.com)에 로그인한 다음, Dashbord 화면에서 `Create repository`를 선택한다. <br/><br/>
![리포지토리생성1](/assets/images/setup/create_repo1.jpg){:class="align-center"  width="75%" } <br/>
- Repository name을 **`username.github.io`**의 형태로 입력하고 다른 옵션들은 그대로 둔다. 
설정을 마치면 화면 오른쪽 아래에 위치한 `Create repository` 버튼(아래 이미지에서는 보이지 않음)을 클릭한다.<br/><br/>
![깃허브리포지토리1](/assets/images/setup/create_repo2.jpg){:class="align-center" width="75%" } <br/>

### 2. Jekyll 테마 가져오기 - Minimal Mistakes
Jekyll은 사이트의 디자인을 손쉽게 변경할 수 있는 다양한 템플릿과 스타일을 제공한다. Jekyll 테마를 제공하는 사이트에서는 데모를 통해 미리 경험하고, 마음에 드는 테마를 선택할 수 있다. 선택한 테마의 소스코드는 Github에 공개되어 있어서 자유롭게 활용할 수 있다. 지금의 블로그는 [Minimal Mistakes](https://github.com/mmistakes/minimal-mistakes)를 기본 테마로 사용하고 있다.
>
**Jekyll 테마를 제공하는 사이트 모음** 
  - [GitHub.com #jekyll-theme repos](https://github.com/topics/jekyll-theme)  
  - [jamstackthemes.dev](https://jamstackthemes.dev/ssg/jekyll/)  
  - [jekyllthemes.org](http://jekyllthemes.org/)  
  - [jekyllthemes.io](https://jekyllthemes.io/)  
  - [jekyll-themes.com](https://jekyll-themes.com/)  
{: .notice--info .text-justify}
 
 아래 그림에서 볼 수 있듯이, Github에 공개된 코드를 가져오는 주된 방법은 Download(*.zip), Clone, 그리고 Fork가 있다. 각각의 방법에 따라 작업 내용이 다르고 문제가 발생할 경우 대응 방법이  달라질 수 있기 때문에 Git에 대한 기본적인 이해가 필요하다. 이 튜토리얼에서는 프로젝트를 **Clone**하여 로컬 환경으로 가져오기로 한다. Clone은 해당 저장소의 모든 파일과 히스토리를 복사해와서 로컬 환경에서 작업할 수 있도록 한다.
  <br/>

![깃허브](/assets/images/setup/mm_gitrepo.png){:class="align-center" width="75%" } 

- Windows cmd에서 로컬 저장소에 디렉토리 `realBlog`를 새로 생성한다.

``` shell
// 디렉토리 생성
D:\>mkdir realBlog
```
- **`git clone`** 명령으로 Minimal Mistake 저장소 내용을 복제한다. `git clone '테마저장소 주소' '디렉토리 이름'`을 차례로 입력하여 명령어를 완성한다. <br/>

``` shell
// minimal-mistakes 저장소 내용을 realBlog로 복제하기
D:\>git clone https://github.com/mmistakes/minimal-mistakes.git realBlog
Cloning into 'realBlog'...
remote: Enumerating objects: 18943, done.
remote: Total 18943 (delta 0), reused 0 (delta 0), pack-reused 18943Receiving obReceiving objects: 100% (18943/18943), 45.04 MiB | 5.55 MiB/s, done.

Resolving deltas: 100% (11248/11248), done.
```

### 3.  Minimal Mistakes 프로젝트 정리하기 
Minimal Mistakes 테마 가이드를 보면, 다음 목록의 폴더와 파일들은 삭제해도 좋다고 한다. `docs, test` 폴더에는 다양한 예제들이 포함되어 있고, 이들은 참고용으로 로컬 저장소에만 보관하기로 한다. `README.md` 파일은 실제 사용하고, 나머지 파일들은 삭제하기로 한다.  <br/>

```
.editorconfig                     -- 제거
.gitattributes                    -- 제거
.github                           -- 제거
/docs                             -- 로컬 저장소에만 보관 --> .gitingnore에 추가
/test                             -- 로컬 저장소에만 보관 --> .gitingnore에 추가
CHANGELOG.md                      -- 제거
minimal-mistakes-jekyll.gemspec   -- 제거
README.md                         -- 사용
screenshot-layouts.png            -- 제거
screenshot.png                    -- 제거
```
<!-- <br/> -->

클론한 테마는 Git의 관리를 받는 프로젝트로서, 이미 커밋 이력이 존재하기 때문에 선택적으로 관리 방식을 변경하면 충돌이 발생할 수 있다. 따라서 docs와 test 폴더를 로컬 저장소에 남긴 채 원격 저장소에 push하지 않기 위해서는 기존의 커밋 이력을 삭제하고 이후의 변경 사항을 추적하지 않도록 설정하는 작업이 필요하다.

- 먼저 제거하기로한 파일과 폴더는 프로젝트 내부에서 삭제한다.
- Visual Studio Code로 테마프로젝트를 열어서 `.gitignore`파일의 하단에 다음을 추가한다. <br/>

![.gitignore](/assets/images/setup/gitignore.jpg){:class="align-center" width="80%" } <br/>

- `realBlog` 폴더로 이동하여 관리 이력을 삭제하는 명령을 실행한다. 

```shell
// realBlog 디렉토리로 이동
D:\>cd realBlog

// docs, test 폴더와 하위 파일들의 캐시기록 삭제 실행
D:\realBlog>git rm -r --cached docs test
rm 'docs/Gemfile'
rm 'docs/_config.dev.yml'
// 생략...
```
- 작업 디렉토리의 변경 내용을 스테이징 영역에 추가한 다음 메시지와 함께 커밋한다.

```shell
// 스테이징 영역에 추가
D:\realBlog>git add .

// 커밋
D:\realBlog>git commit -m "블로그 생성 & ignore 수정"
[master 0aa373a5] 블로그 생성 & ignore 수정
 576 files changed, 4 insertions(+), 17899 deletions(-)
 delete mode 100644 .editorconfig
 delete mode 100644 .gitattributes
 delete mode 100644 .github/CONTRIBUTING.md
 // 생략...
```
### 4.  git push하기

- Github의 계정 정보와 동일하게 이메일 계정과 사용자 이름 설정한다.

``` shell
D:\realBlog>git config --global user.email "이메일계정"
D:\realBlog>git config --global user.name "사용자이름"
```

- 설정되어 있는 원격저장소의 주소를 삭제한 다음, 위에서 생성한 Repository를 원격저장소로 추가한다. 

```shell
// 기존의 원격저장소 주소 삭제하기
D:\realBlog>git remote remove origin

// 새로 생성한 repository를 원격저장소로 추가하기
D:\realBlog>git remote add origin "respository 주소"
```

- `git push` 명령으로 로컬저장소에 있는 커밋들을 원격저장소로 올려보낸다.

```shell
// 로컬저장소 내용을 origin의 master 브랜치로 push하기
D:\realBlog>git push origin master
Enumerating objects: 16953, done.
Counting objects: 100% (16953/16953), done.
Delta compression using up to 16 threads
Compressing objects: 100% (6565/6565), done.
Writing objects: 100% (16953/16953), 44.34 MiB | 4.48 MiB/s, done.
Total 16953 (delta 10115), reused 16947 (delta 10112), pack-reused 0
remote: Resolving deltas: 100% (10115/10115), done.
To https://github.com/codeantenna/codeantenna.github.io.git
 * [new branch]        master -> master
```

- git push 명령이 정상적으로 실행되면 원격저장소와 로컬저장소의 구조를 비교하여 변경사항이 원하는대로 반영되었는지를 확인한다. <br/>

![my repository](/assets/images/setup/gitrepoafterpush.png){:class="align-center" width="75%" } <br/>


- 이제부터는 브라우저에서`https://사용자명.github.io`로 접속할 수 있다. <br/>

![my blog](/assets/images/setup/blog_web.png){:class="align-center" width="75%" } 

### 5.  localhost에서 접속하기
컨텐츠를 작성하고 실행 여부를 확인하기 위해서는 로컬에서 검증하는 작업이 반드시 필요하다. `realBlog`폴더로 이동하여 서버를 구동시키니 `Gemfile`을 파싱하는 과정에서 오류가 발생했다.

```shell
D:\realBlog>bundle exec jekyll serve

[!] There was an error parsing `Gemfile`: There are no gemspecs at D:/realBlog. Bundler cannot continue.
```

구글링한 결과 여러 가지 해결책이 나오지만, 지금은 Minimal-Mistakes 가이드에서 제시한 방법을 따라 `Gemfile` 파일을 수정하기로 한다. 아래의 코드대로 수정한 다음 다시 서버를 구동하면, 정상적으로 실행되고 문제가 해결되었음을 알 수 있다.

<script src="https://gist.github.com/codeantenna/0b0ed19a8de8ddbedcfa96896ff99a07.js"></script> <br/>

------
>**참고한 글**  
> 
> 기록으로 남겨주셔서 감사합니다. 덕분에 이 글이 완성됐어요.  &nbsp; <i class="fa fa-gift" style="color: MediumVioletRed"></i> 
 1. [Minimal Mistakes Quick-Start Guide](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/)  
 2. [GitHub Pages 블로그 따라하기](https://devinlife.com/howto/)  


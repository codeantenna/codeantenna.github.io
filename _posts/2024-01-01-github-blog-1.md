---
title:  "Github 블로그 HOWTO - [1]"
search: true
categories: 
  - Blog
tags:
  - Github Pages
  - Ruby
  - Jekyll
date: 2024-01-01
last_modified_at: 2024-01-01
excerpt_separator: <!--more-->
---
기술 블로그를 위한 플랫폼으로써 **GitHub Pages**는 꽤 이상적인 선택이다. 저장소에서 바로 호스팅을 시작할 수 있고, 설정도 간편해서 빠르게 시작할 수 있다. <!--more--> 개발자들에게 익숙한 GitHub 환경에서 Markdown 파일을 업로드하면 자동으로 콘텐츠가 게시되니 상당히 편리하다. 하지만 현실적으로 정돈된 글을 올리기까지 조금은 까다롭고 번거로운 과정이 기다리고 있다. 나름의 이유로 Github를 선택한 용감한 이들에게 소소한 정보와 경험을 공유하고자 한다.


### 1. 블로그 작업에서 사용할 기술
플랫폼을 정했으니, 다음은 **사용할 기술**을 검토할 단계이다. 구글 검색 결과, 다수의 Github 기반 블로거들이 선호하는 기술 조합을 정리하면 아래와 같다. 참고할 레퍼런스와 가이드가 쌓여 있다는 사실은 언제나 선택의 부담을 덜어준다. 하지만 순수하게 블로깅이 목적이라면 다른 플랫폼을 고민해보는 것도 좋겠다.

>
 **Markdown** : 간단한 문법으로 구조화된 텍스트를 작성하는 경량 마크업 언어로, HTML로 변환이 가능  
 **Jekyll** : Ruby로 작성된 정적 사이트 생성기로, Markdown으로 작성된 내용을 HTML 웹 페이지로 렌더링하는 작업 수행  
 **Github Pages** : GitHub가 제공하는 서비스로 정적 웹사이트를 손쉽게 만들고 호스팅함
{: .notice--info}

위의 기술들로 작업을 진행하려면 몇 가지 툴이 필요하다. GitHub는 회원 가입 후 즉시 사용할 수 있는 서비스이고, 나머지 도구들은 설치가 필요한 오픈소스 프로그램이다.  
<br/>
 ![Github](/assets/images/setup/toolkit.png){:class="align-center"  width="80%"}

  참고로 로컬에 설치된 버전을 공유하자면, 
 - [Git](https://git-scm.com/downloads) - 2.41.0.windows.1
 - [Visual Studio Code](https://code.visualstudio.com/download)  - 1.76.0
 - [Ruby_DevKit](https://rubyinstaller.org/downloads/) - 3.2.2
 - Jekyll - 4.3.2  이다.
 <br/>

기존의 Git과 VS Code가 설치되어 있는 환경에 Ruby와 Jekyll을 추가하여 사용하고 있기에, 여기서는 새롭게 추가된 프로그램의 설치 과정만을 소개하기로 한다.

### 2. 블로그 작업 환경과 기능
 
![블로그 작업 환경](/assets/images/setup/setup.png){:class="align-center"  width="80%"}  
<br/>
 블로그 작업 환경에서 툴의 기능과 작업 내용들을 그림과 함께 간단하게 정리해 보았다.  
1.  VS Code를 사용하여 Markdown 문법에 맞게 컨텐츠를 작성하거나 디자인 편집(HTML, CSS 등)을 한다.
2.  Jekyll 명령어로 서버를 구동시키면 **http:127.0.0.1:4000**인 로컬 환경에서 작성된 내용을 미리 확인할 수 있다.  
3.  편집된 결과물을 git 명령어로 원격지 저장소인 Github의 Repository에 push한다.
4.  Github는 **https://username.github.io**의 네이밍 규칙에 따라 생성된 저장소(repository)의 내용을 게시해준다. 이제부터는 웹에서 직접 블로그에 접속하여 내용을 확인할 수 있다. 



### 3. 블로그 작업 환경 준비하기 (Ruby, jekyll 설치)
 1. [https://rubyinstaller.org/downloads/](https://rubyinstaller.org/downloads/)에서 ruby+devkit을 다운로드한다.  <br/><br/>
![루비다운로드](/assets/images/setup/rubysite.jpg){:class="align-center"  width="65%" }  <br/><br/>
 2. 라이선스 사용 동의, 설치 경로 설정 등의 과정을 거쳐 Ruby 설치가 완료된다.  <br/><br/>
  ![라이선스동의](/assets/images/setup/rubylicense.jpg){:class="align-center"  width="65%" } <br/>
  ![설치경로](/assets/images/setup/destination.jpg){:class="align-center"  width="65%" } <br/>
  ![구성요소선택](/assets/images/setup/component.jpg){:class="align-center"  width="65%" } <br/>
 ![루비설치완료](/assets/images/setup/finished.jpg){:class="align-center"  width="65%" } <br/>  
 3. 이어지는 설치 옵션에서 1을 입력하여 MSYS2 base를 선택한다.<br/><br/> 
  ![MSYS2 base 설치 옵션](/assets/images/setup/msys2installer1.jpg){:class="align-center" width="75%"  } <br/>
 4. 설치 완료 메시지를 확인한 후, Enter를 입력하여 마무리한다.<br/><br/> 
  ![MSYS2 base 설치 완료](/assets/images/setup/msys2installed.jpg){:class="align-center"  width="75%" } <br/><br/>
 5. `Start Command Prompt with Ruby` 프로그램을 실행시킨 다음 `gem install jekyll bundler` 명령을 실행하여 Jekyll을 설치한다. <br/><br/>
  ![지킬 설치](/assets/images/setup/jekyll_install.jpg){:class="align-center"  width="76%" }  <br/>
 6. `jekyll new myBlog`를 실행하면 `myBlog`라는 이름의 폴더 함께 새로운 블로그가 생성된다. <br/><br/>
  ![지킬 설치](/assets/images/setup/jekyll_new.jpg){:class="align-center"  width="76%" }  <br/> 
 7. `myBlog`로 이동 후, `bundel exec jekyll serve`를 입력하면 주소 `http://127.0.0.1:4000/`에서 서버가 실행된다. 만일 서버를 중지시키려면 `Ctrl+C`를 입력한다.<br/><br/>
  ![서버 실행](/assets/images/setup/jekyll_serve.jpg){:class="align-center"  width="76%" }  <br/>
  ![서버 실행](/assets/images/setup/jekyll_serve_port.jpg){:class="align-center"  width="76%" }<br/>
  8. 브라우저에서 `http://127.0.0.1:4000/`를 입력하면, 현재 실행중인 블로그를 확인할 수 있다.  <br/><br/> 
  ![블로그](/assets/images/setup/jekyll_initial.jpg){:class="align-center"  width="76%" }  <br/>

지금까지 블로그 작업을 위한 로컬 환경에 대해 주로 살펴보았다. `jekyll new`로 생성된 블로그는 간단한 샘플 페이지로 구성되어 있다. 검색이나 댓글 등 필요한 기능을 처음부터 구현하려면 상당한 시간이 필요하다. 그래서 Jekyll 테마를 활용하고, 커스터마이징하는 방법을 작업 순서대로 소개하면서 블로그를 완성하려고 한다.



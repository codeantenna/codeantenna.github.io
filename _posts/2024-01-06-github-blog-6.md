---
title:  "Github 블로그 HOWTO - [6]"
search: true
categories: 
  - Blog
tags:
  - comments
  - Utterances
  - Github Issue
date: 2024-01-08 
last_modified_at: 2024-01-08
excerpt_separator: <!--more-->
---
블로그의 댓글 기능은 독자들이 게시물에 대한 질문이나 피드백을 주고받으며 상호작용할 수 있게 한다. 특히 기술 블로그에서는 이 기능이 다른 어떤 것보다도 중요한 역할을 한다. <!--more--> 댓글을 통해 독자들은 작성자와 소통하고, 자신의 생각을 나누며, 추가적인 정보나 의견을 제공할 수 있지만, 때로는 스팸이나 부적절한 내용이 올라올 수 있으므로 적절한 모니터링이 필요하다. 또한, 댓글 시스템은 익명성을 유지하면서도 적절한 품질을 유지할 수 있는 방식으로 설정할 필요가 있다.

Jekyll은 기본적으로 내장된 댓글 시스템을 제공하지 않지만 외부 서비스를 통해 댓글 기능을 추가할 수 있다. 대개 블로그에서는 'Disqus', 'Discourse', 'Utterances'와 같은 시스템을 사용하는데, 현재 이 블로그에서는 'Utterances'를 사용하고 있다.

`Utterances`는 GitHub Issue를 댓글 시스템으로 활용한다. 마크다운을 지원하며 코드 블록을 삽입하기 쉽고, 이러한 댓글은 GitHub Issue에 저장되어 관리 및 모니터링이 편리하다. 또한 Utterances는 무료로 이용할 수 있으면서 광고 없이 서비스를 제공해주는 점이 다른 댓글 시스템들과 비교했을 때 매우 매력적이며, 사용자들은 GitHub 계정을 이용하여 댓글을 작성할 수 있다.


### 1. Utterances 설정

 1. [Utterances App](https://github.com/apps/utterances) 설치 페이지로 이동하여 App을 설치한다. <br/> <br/>
![Utterances Site](/assets/images/screenshot/utterances_site.png){:class="align-center"  width="80%"}
<br/>
 2. 댓글을 저장할 Issue를 관리하기 위한 repository를 선택한다. 이 저장소는 반드시 `Public` 상태여야 하므로, 블로그의 공개 여부와는 관계없이 댓글을 독립적으로 관리할 수 있도록 별도의 댓글 전용 repository를 지정한다. <br/> <br/>
![Utterances Repository](/assets/images/screenshot/utterances_repo.png){:class="align-center"  width="80%"} <br/>
 3. 설치가 완료되면 설정 페이지로 이동하여, `repo`의 입력란에 Issue 생성 권한을 부여했던 Repository를 [User Name]/[Respository] 형식으로 작성한다. 그 후, 블로그 게시물과 이슈 간의 연결 방식과 블로그 테마에 어울리는 스타일을 선택한다. 그러면 Utterances가 설정된 옵션에 맞게 자바스크립트 코드를 생성해준다. <br/> <br/>
![Utterances Configuration](/assets/images/screenshot/utterances_config1.png){:class="align-center"  width="80%"}
![Utterances Configuration](/assets/images/screenshot/utterances_config2.png){:class="align-center"  width="80%"}
<br/>
 4. Javascript 코드가 적용될 템플릿의 위치는 _includes/comments-providers/utterances.html이다. 해당 스크립트는 `_config.yml`에 정의된 파라미터들을 활용하고 있으며, 최대한 원본의 코딩 스타일을 유지하며 적용하려 한다.  

 - `_config.yml`에 파라미터들을 아래와 같이 설정한다. 

 ``` yml
comments:
provider               : utterances  
utterances:
  repo                 : codeantenna/blog_comments   # 새로 추가한 속성
  theme                : github-light 
  issue_term           : url
 ```

 - 위에서 설정한 파라미터들은 /_includes/comment-providers/utterances.html 에서 사용된다. 새로 추가한 파라미터 `'repo'`(13번 라인) 부분만을 수정하면 템플릿이 완성된다.  

{% highlight html linenos %}
<script>
  'use strict';

  (function() {
    var commentContainer = document.querySelector('#utterances-comments');
    if (!commentContainer) {
      return;
    }
{% raw %}
    var script = document.createElement('script');
    script.setAttribute('src', 'https://utteranc.es/client.js');
    // 수정된 부분  ↓
    script.setAttribute('repo', '{{ site.comments.utterances.repo | default: site.repository }}'); 
    script.setAttribute('issue-term', '{{ site.comments.utterances.issue_term | default: "pathname" }}');
    {% if site.comments.utterances.label %}script.setAttribute('label', '{{ site.comments.utterances.label }}');{% endif %}
    script.setAttribute('theme', '{{ site.comments.utterances.theme | default: "github-light" }}');
    script.setAttribute('crossorigin', 'anonymous');

    commentContainer.appendChild(script); {% endraw %}
  })();
</script>
{% endhighlight %}

### 2. 댓글 기능 사용 설정
_config.yml 또는 마크다운 파일에서 `comments` 파라미터를 `true`로 설정해준다. 이렇게 함으로써 해당 파일에 댓글 기능을 활성화시킬 수 있다.
``` yml
# Defaults
defaults:
  # _posts
  - scope:
      path: ""
      type: posts
    values:
    # 생략 ...
      comments:  true
    # 생략 ...
```

### 3. 댓글 기능 확인
블로그에 Utterances 댓글 기능이 추가됐으니, 변경된 내용을 git push하여 해당 기능이 제대로 동작하는지 확인한다. 
- 블로그의 하단에 댓글 창이 표시되며, Github 계정으로 로그인한 상태에서 댓글을 작성할 수 있다. 작성한 댓글은 마크다운 형식에 맞게 작성한 경우 미리보기로 보여진다.

![Utterances Comments](/assets/images/screenshot/comment_url.png){:class="align-center"  width="80%"}
- Utterances를 통해 작성된 댓글은 GitHub의 이슈로 생성되어, 관련 repository의 issues 탭에서 모아 볼 수 있다.

![Github Issue](/assets/images/screenshot/issue_url.png){:class="align-center"  width="80%"}

<br/>

------
>**참고한 글**  
> 
> 기록으로 남겨주셔서 감사합니다. 덕분에 이 글이 완성됐어요.  &nbsp; <i class="fa fa-gift" style="color: MediumVioletRed"></i> 
 1. [블로그 댓글 utterances로 변경하기](
https://hyeon9mak.github.io/블로그-댓글-utterances로-변경하기/)  
 2. [Comment feature in Jekyll blog](https://deku.posstree.com/en/jekyll/utterances/)  

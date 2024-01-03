---
title:  "Github 블로그 시작하기 - [4]"
search: true
categories: 
  - Blog
tags:
  - Markdown
  - Jekyll
date: 2024-01-03   
last_modified_at: 2024-01-03
excerpt_separator: <!--more-->
---
**Markdown**은 텍스트를 사용해 문서를 만드는 간단한 마크업 언어다. HTML보다 쉽고, 텍스트 편집기만 있으면 누구나 빠르고 간편하게 글을 편집할 수 있다. <!--more--> 이제 글을 쓰기 전에 기본적인 마크다운 문법을 알아보기로 한다. 이해를 돕기 위해 문법의 예시와 렌더링된 결과를 비교하여 정리했다.  

<!-- ### 1. 마크업: HTML 태그 및 포맷 -->

### 1. HTML 제목  
`#`을 사용하여 HTML 제목을 만든다. `#`의 개수에 따라 제목의 수준이 1에서 6수준까지 달라지는데, 개수가 많아질수록 하위 수준의 제목으로 표현된다.

**`Markdown 문법`**
```html
# Header One         --> 제목 1수준 
## Header two        --> 제목 2수준
#### Header four     --> 제목 4수준
```
{% capture notice-2 %}
**`화면 출력`**
# Header One
## Header two
#### Header four 
{% endcapture %}
<div class="notice">{{ notice-2 | markdownify }}</div>

### 2. 줄바꿈  
HTML 태그인 \<br\>을 삽입하여 마크다운 프로세서가 줄 바꿈을 삽입하도록 강제할 수 있다.

**`Markdown 문법`**
```html
If you really look closely, <br>most overnight successes<br> took a long time.
```

{% capture notice-3 %}
**`화면 출력`**  

If you really look closely, <br>most overnight successes<br> took a long time.
{% endcapture %}
<div class="notice">{{ notice-3 | markdownify }}</div>

### 3. 수평선 표기
수평선을 표시하는 방법은 여러 가지가 있다. 아래에 제시한 바와 같이 `---`, `***`, `___`을 사용해 수평선을 나타낼 수 있다. 이것들은 텍스트에서 구분선으로 사용된다.

**`Markdown 문법`**
```html
***
---
_________________
```

{% capture notice-3 %}
**`화면 출력`**  

***
---
_________________
{% endcapture %}
<div class="notice">{{ notice-3 | markdownify }}</div> 

### 4. 순서가 있는 목록
순서가 있는 목록은 숫자를 사용하여 항목을 나열하는 목록이다. 보통 숫자로 표시되며, 순서에 따라 숫자가 매겨진다. 항목 안에 서브 항목들을 중첩해서 나열할 수 있다. 이는 각 항목 아래에 기호 `(*, +, -)`와 함께 들여쓰기로 구분하여 써주면 된다. 여러 단계로 중첩된 항목들도 만들 수 있다.

**`Markdown 문법`**
```html
1. 코미디
  - 극한직업
2. 뮤지컬
3. 액션
```
{% capture notice-3 %}
**`화면 출력`**  
1. 코미디
  - 극한직업
2. 뮤지컬
3. 액션
{% endcapture %}
<div class="notice">{{ notice-3 | markdownify }}</div> 

### 5. 순서가 없는 목록  
순서 없는 목록은 항목들을 순서 없이 나열하는 목록이다. 이 목록은 항목들 간의 순서가 중요하지 않을 때 사용된다. 각 항목을 나열하고자 할 때 사용되며, `(*, +, -)`로 표현할 수 있다.  

**`Markdown 문법`**
```html
* 코미디
  * 극한직업
* 뮤지컬
* 액션
```
{% capture notice-3 %}
**`화면 출력`**  
* 코미디
  * 극한직업
* 뮤지컬
* 액션
{% endcapture %}
<div class="notice">{{ notice-3 | markdownify }}</div> 


### 6. Blockquotes 
인용구를 표현하는 데 사용되는 요소이며, 다른 사람의 말이나 외부 소스에서 인용한 내용을 나타낸다. 이를 표현하기 위해 `>` 기호를 사용하여 문장을 시작한다.  

**`Markdown 문법`** 
```html
> 첫 번째 수준의 인용
>> 두 번째 수준의 인용

> If you really look closely, most overnight successes took a long time.
<cite>스티브 잡스</cite>
```
{% capture notice-3 %}
**`화면 출력`**  
> 첫 번째 수준의 인용
>> 두 번째 수준의 인용

> If you really look closely, most overnight successes took a long time. <cite>스티브 잡스</cite>
  
{% endcapture %}
<div class="notice">{{ notice-3 | markdownify }}</div> 


### 7. 텍스트내 링크 추가
**`Markdown 문법`** : \[텍스트\]\(텍스트에 연결된 URL\)
```html
[구글](http://www.google.com)로 이동하기
```
{% capture notice-3 %}
**`화면 출력`**  
  
[구글](http://www.google.com)로 이동하기 
{% endcapture %}
<div class="notice">{{ notice-3 | markdownify }}</div> 

### 8. 이미지 추가 
이미지를 삽입하려면 아래의 형식을 사용한다. 여기서 대체 텍스트는 이미지를 설명하는 텍스트이고, 이미지 주소는 이미지 파일의 URL이다. 예시에서 이미지 속성을 직접 지정하고 있지만, HTML과 CSS를 사용하면 이미지에 더 많은 속성을 부여할 수 있다.

**`Markdown 문법`** : \!\[대체 텍스트\]\(이미지 파일의 URL\)
```html
![Github](/assets/img/logos/github.png)
![Github](/assets/img/logos/github.png "이미지 위에 마우스를 올려 보세요."){:class="align-center" width="20%"}
```
{% capture notice-3 %}
**`화면 출력`**   
![Github](/assets/images/logos/github.png)
![Github](/assets/images/logos/github.png "이미지 위에 마우스를 올려 보세요."){:class="align-center" width="20%"}
{% endcapture %}
<div class="notice">{{ notice-3 | markdownify }}</div> 


### 9. 테이블 삽입
테이블을 만들려면 세 가지 요소를 사용한다. `|`, `-`, 그리고 콜론 `:` 이다.  

헤더를 만들기 위해서는 각 열의 제목을 `|`로 구분하고, 그 아래 행에 하이픈 `-`을 사용하여 각 열을 나타낸다. 테이블 셀의 너비는 보통 콘텐츠에 따라 자동으로 조정된다. 또한 콜론 `:`을 사용하여 텍스트를 정렬할 방향을 지정할 수 있다. \(Column 1: 왼쪽 정렬, Column 2: 중앙 정렬, Column 3: 오른쪽 정렬\)

**`Markdown 문법`**   
```html
| Column 1  | Column 2 | Column 3  |
|:----------|:--------:|----------:|
| row 1     | item 1   | **item2** |
| row 2     | item 3   |   *item4* | 
```
{% capture notice-3 %}
**`화면 출력`**   

| Column 1  | Column 2 | Column 3  |
|:----------|:--------:|----------:|
| row 1     | item 1   | **item2** |
| row 2     | item 3   |   *item4* |
{% endcapture %}
<div class="notice">{{ notice-3 | markdownify }}</div> 

### 10. 백슬래시 마스킹
마크다운 프로세서에서 기본적으로 마크다운 구문으로 해석되는 기호를 사용하려면 기호 앞에 백슬래시 `\`를 함께 배치한다.    

**`Markdown 문법`**
```html
\*  \-  \_  \(\) \. \!  \{\}  \[\]  \#  \`  \\
```
{% capture notice-3 %}
**`화면 출력`**  
  
\*  \-  \_  \(\) \. \!  \{\}  \[\]  \#  \`  \\
{% endcapture %}
<div class="notice">{{ notice-3 | markdownify }}</div> 


### 11. 텍스트 접기 
다음 코드를 사용하면 텍스트 섹션을 접은 채로 표시할 수 있다. 왼쪽의 `▶`기호를 클릭해서 펼치면 숨겨진 내용을 볼 수 있다.

**`Markdown 문법`**
```html
<details>
<summary>숨겨진 글을 찾아보세요</summary>
<br>
Stay Strong!
```
{% capture notice-3 %}
**`화면 출력`**  
  
<details>
<summary>숨겨진 글을 찾아보세요</summary>
<br>
Stay Strong!
{% endcapture %}
<div class="notice">{{ notice-3 | markdownify }}</div> 

### 12. 구문 강조 표시  
구문 강조 표시는 **\`\`\`** 나 **~~~**로 감싼 코드 블록에 적용할 수 있다. Jekyll에서 지원하는 구문 강조 언어들이 여러 가지 있고, 보다 자세한 정보는 링크된 [글](https://www.fabriziomusacchio.com/blog/2021-08-11-Syntax_Highlighting_in_Jekyll/)에서 확인할 수 있다.   

**`Markdown 문법`**
~~~ html
  ```python
  import numpy as np
  a=np.arange(5)
  print(a+a)
  ```
~~~
{% capture notice-3 %}
**`화면 출력`**  
  
```python
import numpy as np
a=np.arange(5)
print(a+a)
```
{% endcapture %}
<div class="notice">{{ notice-3 | markdownify }}</div> 

------
>**참고한 글**  
> 
> 기록으로 남겨주셔서 감사합니다. 덕분에 이 글이 완성됐어요.  &nbsp; <i class="fa fa-gift" style="color: MediumVioletRed"></i> 
 1. [Minimal Mistakes Quick-Start Guide](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/)   
 2. [Minimal Mistakes Cheat Sheet](https://www.fabriziomusacchio.com/blog/2021-08-11-Minimal_Mistakes_Cheat_Sheet/)

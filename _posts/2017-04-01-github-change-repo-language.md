---
layout: post
title:  "Github의 레파지토리에 기본 언어 변경하기"
date:   2017-04-01 16:34:00 +0900
categories: github
---

Github는 Git 기반의 원격 VCS(Version Control System) Repository 서비스입니다.  
기본적으로 공개 Repository의 경우 무료로 사용할 수 있고, private Repository는 월 과금으로 유료로 사용할 수 있습니다.

종종 Github를 Git 서비스를 제공하는 VCS 서비스로만 생각하시는 분들이 계시는데요.  
Github에는 상당히 다양한 서비스와 소소한 재미거리들이 있습니다.

대표적인 것이 Markdown 문서를 html로 파싱하여 보여주는 Github pages 서비스가 있습니다.  
이 서비스는 Jekyll이라 불리는 Ruby 기반의 오픈소스 솔루션을 사용한 서비스로 많은 개발자분들(저를 포함한)이 Github에 블로그를 만들게 하였죠.  

그외에도 OAuth 서비스를 비롯한 플랫폼 서비스와 이슈 관리, 소셜 기능 등을 제공합니다.  

오늘 살펴볼 서비스는 Repository에 어떤 개발 언어로 만들어진 소스가 저장되어 있는지 알려주는 `repository language` 서비스 입니다.

<br/>

### Github가 레파지토리의 언어를 분석하는 방법

![Github user profile](/asserts/2017-04-01-github-change-repo-language/01.jpg)

Github에 로그인한 후 Profile 페이지로 이동하면 위와 같은 개인화 페이지를 볼 수 있습니다.  
이 중 레파지토리 목록을 보면, 해당 레파지토리가 어떤 언어의 소스를 담고 있는지 노출하고 있는데요.

이 정보는 Github에서 소스를 분석하여 자동으로 보여주는 부분입니다.  

Github에서는 [Linguist](https://github.com/github/linguist)라는 라이브러리를 사용해 레파지토리의 언어를 분석하고 있습니다.  
기본적으로는 해당 파일이 텍스트 기반 파일인지, 바이너리 파일인지를 분류하고 텍스트 기반 파일인 경우 해당 파일이 어떠한 언어로 작성되어 있는지를 분석합니다. 예를 들면 `.dat` 파일은 바이너리 파일일 수도 있고, 텍스트 파일일 수도 있습니다. Github 레파지토리에 `.dat` 파일이 등록되어 있고, 변경 이력이 관리되고 있다면 해당 파일이 바이너리인지 텍스트인지를 명시적으로 정의해 줄 수 있습니다.
또한 Linguist는 개별 파일 혹은 파일들에 대해 Github의 code highlight를 지정하는 기능도 가지고 있으므로, `.dat` 파일이 예를 들어 텍스트 파일이고, CSS의 표현식을 갖추고 있다면 CSS의 code highlight로 지정해 줄 수도 있습니다. (자세한 내용은 linguist의 레파지토리를 방문해 보세요.)

<br/>

### Linguist가 수행하는 Github 언어 분석의 문제점

![where is analisys language rate](/asserts/2017-04-01-github-change-repo-language/02.jpg)

위 스크린샷은 제 개인 프로젝트 소스를 담고 있는 레파지토리입니다.  
레파지토리의 Root 페이지에 진입하면 상단에 Commit, Branch 수 등을 볼 수 있는데요.  
이 하단의 바(스크린샷에서는 붉은색, 노란색, 갈색, 보라색으로 표기된)가 분석된 언어의 비중을 보여주고 있습니다.  
이 바를 클릭하면 아래와 같이 언어 비중이 출력됩니다.

![language rate](/asserts/2017-04-01-github-change-repo-language/03.jpg)

현재 제 레파지토리는 HTML이 85.9%, Javascript가 7.8%, Java는 겨우 4.7%의 비중을 가지고 있다고 분석되었습니다.  
언어명을 클릭하면 아래 스크린샷과 같이 상세한 파일 목록을 볼 수 있습니다.  

![matched language rate](/asserts/2017-04-01-github-change-repo-language/04.jpg)

이 언어 분석 기능은 레파지토리에 등록된 전체 파일을 검사하는데, 간혹 잘못된 언어가 분석되는 경우가 있습니다. (잘못되었다기 보다는 의도하지 않은...)  
특히, 웹 프로젝트의 경우 많은 라이브러리가 text 기반의 파일로 생성되고, 배포됩니다.  
만약 jquery라던가, angularJS 등과 같은 Javascript 라이브러리를 CDN에서 읽어오지 않고 레파지토리에 등록해 하드 링크를 사용한다면 대표 언어가 javascript로 분석되는 경우가 있습니다. 또한 bootstrap의 템플릿등을 등록했다면 HTML 혹은 CSS로 분류되기도 합니다.  

그래서 제 개인 프로젝트는 Java 소스가 상당한 비중을 차지하는데에도 불구하고 위의 스크린샷과 같이 HTML의 비중이 높게 분석되었습니다. (현재 위 레파지토리에는 다른 장비들에서도 공유해서 작업하기 위한 bootstrap 테마가 등록되어 있습니다.)

<br/>

Git에서는 여러가지 설정 파일을 사용할 수 있습니다.  
대표적이면서 많이 알려진 것이 `.gitignore` 설정 파일입니다. 이 파일은 Git으로 관리되지 않아야하는 파일 목록을 담고 있습니다. `.gitignore`에 등록된 파일 혹은 경로는 Git의 변경 내역으로 잡히지 않습니다.  

그 외에 오늘 문제를 해결하는 Key인 `.gitattributes`가 있습니다.

.gitattributes는 git 레파지토리의 다양한 속성 및 설정을 정의할 수 있는 설정 파일입니다.  

<br/>

### .gitattributes를 이용하여 언어분석 예외 추가하기

우리가 git에서 변경사항을 추적하기를 원하지 않는 파일 혹은 경로 목록을 .gitignore를 통해 관리하듯이 .gitattributes를 통해 Github가 언어분석하기를 원하지 않는 파일이나 경로를 지정할 수 있습니다.  

우선 Repository 경로 루트에 `.gitattributes`라는 파일을 하나 생성합니다.  
그리고 아래와 같이 내용을 기록합니다.

{% highlight text %}
web/dist/* linguist-vendored
web/template/* linguist-vendored
web/vendor/* linguist-vendored
{% endhighlight %}

위 예시는 각각의 특정 경로에 대해 linguist가 처리하지 않도록 정의하고 있습니다.  
사용법은 간단합니다. linguist가 분석하지 않길 바라는 경로의 목록을 기록하고 그 뒤에 `linguist-vendored`라고 적어줍니다.  
그럼 해당 파일 혹은 경로가 Github에 push되었을 때 linguist가 분석을 하지 않습니다.

파일 혹은 경로는 정규표현식으로 표현할 수 있습니다.

몇가지 예시를 들어보면...

1. 경로 하위의 모든 파일을 제외 : 경로/*
2. 특정 확장자를 제외 : *.md
3. 특정한 형태의 파일명을 가진 파일을 제외 : test*.java

등이 있을 수 있습니다. 자세한 내용은 정규표현식을 확인해 보세요.

<br/>

위의 경로 혹은 특정 패턴의 파일을 언어 분석에서 제외하는 방법과 함께 파일의 mime 타입을 지정하여 언어 분석을 돕는 방법도 있습니다.
예를 들어 자바 웹 프로젝트의 경우 .html, *.js, *.css, *.java 등은 text로 지정하여 언어 분석에 사용하고, *.jar, *.jpg 등은 바이너리 파일로 지정하여 언어 분석에서 제외하는 방법입니다.

{% highlight text %}
*.css           text
*.class         binary
{% endhighlight %}

위와 같이 특정 확장자를 가진 파일을 text 혹은 binary로 분류하여 text 유형의 파일만 언어 분석하도록 지정하는 것입니다.
다만, 프로젝트의 모든 파일을 일일이 분류하는 것은 어려우면서도 많은 노력이 들어갑니다.

그래서 대표적인 프로젝트 별로 .gitattributes를 템플릿으로 제공해주는 오픈 소스 프로젝트도 있습니다.
대표적인 것이 [alexkaratarakis라는 사용자의 gitattributes 프로젝트](https://github.com/alexkaratarakis/gitattributes)가 있습니다.
이 프로젝트에서는 언어 별, 대표 프로젝트 유형별로 .gitattributes 템플릿을 제공하고 있습니다.

<br/>

### .gitattributes 적용 후

그럼 .gitattribute에 alexkaratarakis의 .gitattributes templates을 이용해 적용한 결과를 보겠습니다.

![fixed language](/asserts/2017-04-01-github-change-repo-language/05.jpg)

위 스크린샷은 수정된 언어 분석 결과입니다.  
제 개인 프로젝트 레파지토리(좌측 상단의 sz21c_services 레파지토리)는 아직은 SpringBoot로 개발된 자바 소스가 많은 비중을 차지하기 때문에 Java로 대표 언어가 출력되어야 하는데, 언어가 잘 추천되고 있습니다.

![fixed match language rate](/asserts/2017-04-01-github-change-repo-language/06.jpg)

언어 비율에서도 Java가 가장 많은 비중을 차지는 것으로 출력되고 있습니다.

<br/>

### 참고

- [How to Change Repo Language in GitHub](https://medium.com/black-tech-diva/how-to-change-repo-language-in-github-c3e07819c5bb)
- [About repository languages](https://help.github.com/articles/about-repository-languages)
- [8.2 Customizing Git - Git Attributes](https://git-scm.com/book/en/v2/Customizing-Git-Git-Attributes)
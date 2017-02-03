---
layout: post
title:  "GitHub Pages의 jekyll 테마를 변경하자"
date:   2017-02-03 16:26:00 +0900
categories: jekyll
---
jekyll에서의 테마 변경은 처음에만 어렵지 한번만 해보면 꽤 쉽습니다.  
저도 이번에 기본 테마를 사용하다가 새로운 테마로 변경해 보았습니다.

<br/>

## 테마 고르기
우선 jekyll에서 사용할 수 있는 테마를 골라야 하는데요.  

jekyll의 테마를 검색할 수 있는 곳은 [GitHub Pages themes](https://github.com/pages-themes)와 [jekyll theme on RubyGems](https://rubygems.org/search?utf8=✓&query=jekyll-theme)이 있습니다.  
두 사이트는 같은 소스를 공유하면서 약간 다른 소개 페이지를 제공하는데요.

제가 느낀 차이점이라면 jekyll theme on RubyGems가 UI나 접근성이 더 좋았습니다.  
그리고 jekyll theme on RubyGems에서는 아래에서 이야기할 로컬 jekyll 서버에 수동으로 테마를 설치하기 위한 .gem 파일을 좀 더 쉽게 다운로드 할 수 있습니다.

두 사이트 중 jekyll theme on RubyGems를 이용한 테마 검색 및 테마 적용 방법을 좀 더 이야기해 보겠습니다.

<br/>

[jekyll의 공식 사이트](http://jekyllrb.com)에서는 [테마를 적용하는 방법](http://jekyllrb.com/docs/themes)을 알려주고 있는데요.  
중간 즈음에 보면 "jekyll theme on RubyGems"라는 RubyGems을 이용해 테마를 검색하고 적용할 수 있는 방법을 가이드 하고 있습니다.

참고 : [jekyll theme on RubyGems](https://rubygems.org/search?utf8=✓&query=jekyll-theme)

위 링크를 방문해 보면 다양한 jekyll의 테마를 볼 수 있습니다.

![jekyll theme on RubyGems 스크린샷](/asserts/2017-02-03-change-jekyll-theme/cjt_01.jpg)

이 페이지에서 검색 가능한 테마 중 "for GitHub Pages"라는 표기가 있으면 Github 블로그에서 사용할 수 있습니다.  

각 테마의 소개 페이지는 아래와 같이 구성되어 있습니다.

![https://rubygems.org/gems/jekyll-theme-modernist 페이지 스크린샷](/asserts/2017-02-03-change-jekyll-theme/cjt_02.jpg)

- VERSIONS : 현재 테마의 각 버전 별 링크 (테마의 버전에 따라 지원되는 jekyll의 버전과 플러그인이 다를 수 있으니 꼭 확인해야 합니다.)
- RUNTIME DEPENDENCIES : 현재 테마가 지원하는 jekyll 버전과 필요한 플러그인 및 플러그인 버전

우측 사이드 메뉴 중 중요부분

- GEMFILE : RubyGems를 이용해 원격에서 .gem 파일을 다운로드 받을 수 있는 명령어
- INSTALL : RubyGems를 이용해 원격에서 테마를 설치할 수 있는 명령어

우측 사이드 메뉴 중 링크

- Homepage : 현재 테마의 홈페이지 (GitHub 링크인 경우 대부분 미리보기 페이지를 제공하므로 이 링크를 통해 해당 테마를 확인해 볼 수 있습니다.)
- Documentation : 현재 테마의 적용 및 셋팅 가이드 문서
- Download : 현재 테마의 .gem 파일 다운로드 링크

이 페이지에서 제일 불편한 점은 테마의 미리보기 스크린샷을 제공하지 않는 것인데, 우측 사이드 메뉴 중 링크의 Homepage를 통해 일일이 확인해 보는 수 밖에는 없습니다.

![https://github.com/pages-themes/modernist 페이지 스크린샷](/asserts/2017-02-03-change-jekyll-theme/cjt_03.jpg)

테마의 GitHub Repository를 방문해 보면 상단에 GitHub Pages의 미리보기를 할 수 있는 링크를 제공하고 있습니다.

![https://pages-themes.github.io/modernist/ 페이지 스크린샷](/asserts/2017-02-03-change-jekyll-theme/cjt_04.jpg)

링크를 클릭해보면 이렇게 테마의 기본 적용 모습과 Markdown 문법이 어떻게 출력되는지 확인할 수 있습니다.

<br/>

## jekyll 버전 확인
제가 선택한 modernist 테마는 jekyll 3.3 이상을 요구하고 있습니다.  
GitHub 블로그에 적용하기 전에 필요한 부분을 수정하기 위해 로컬에 적용해 봅니다.  

우선 현재 로컬에 설치된 jekyll의 버전을 확인합니다.  
jekyll의 설치 위치에서 아래의 명령을 실행합니다.

```
jekyll --version
```

그럼 아래와 같이 버전이 표기됩니다.

{% highlight shell %}
kr-zephyr$ jekyll --version
jekyll 3.1.3
{% endhighlight %}

제 로컬의 jekyll 버전은 3.1.3이므로 modernist 테마를 적용하기 위해서는 jekyll을 업데이트 해야 합니다.

<br/>

## jekyll 업데이트
gem을 이용해 jekyll을 최신 버전으로 업데이트 합니다.  
super user 권한이 필요하니 sudo도 빼먹지 말고, 아래와 같이 명령어를 입력합니다.

```
sudo gem update jekyll
```

그러면 jekyll과 필요한 dependency들을 업데이트 합니다.

{% highlight shell %}
kr-zephyr$ sudo gem update jekyll
Password:
Updating installed gems
Updating jekyll
Fetching: colorator-1.1.0.gem (100%)
Successfully installed colorator-1.1.0
...
Installing ri documentation for jekyll-watch-1.5.0
Installing darkfish documentation for jekyll-watch-1.5.0
Gems updated: colorator forwardable-extended pathutil public_suffix addressable jekyll jekyll-sass-converter jekyll-watch
{% endhighlight %}

위와 같이 다소 긴 출력이 지나가고...  
다시 jekyll의 버전을 확인해 보면...

{% highlight shell %}
kr-zephyr$ jekyll --version
jekyll 3.3.1
{% endhighlight %}

이렇게 3.3.1로 업데이트된 것을 확인할 수 있습니다.

<br/>

## 테마 설치

이제 본격적으로 테마를 적용해 볼텐데, jekyll의 테마를 적용하는 방법은 두가지가 있습니다.  
gem을 이용해서 원격에서 다운로드 받거나, 수동으로 파일을 설치하는 방법입니다.  

### 방법1 자동 설치
gem을 이용해서 자동으로 설치하는 방법은 테마의 소개 페이지에 `INSTALL` 부분에서 제공하는 RubyGems 명령어를 이용합니다.  
super user 권한이 필요하니 sudo를 넣어 주고요.  
아래의 명령어를 실행합니다.

```
sudo gem install jekyll-theme-modernist
```

{% highlight shell %}
kr-zephyr$ sudo gem install jekyll-theme-modernist
Password:
Fetching: jekyll-theme-modernist-0.0.3.gem (100%)
Successfully installed jekyll-theme-modernist-0.0.3
Parsing documentation for jekyll-theme-modernist-0.0.3
unable to convert "\x89" from ASCII-8BIT to UTF-8 for assets/images/checker.png, skipping
Installing ri documentation for jekyll-theme-modernist-0.0.3
1 gem installed
{% endhighlight %}

그럼 간단히 테마가 설치됩니다.


### 방법2 수동 설치
만약 어떠한 이유로 원격으로 설치를 할 수 없다면 .gem 파일을 다운로드 받아 설치할 수 있습니다.  
.gem 파일의 다운로드 링크는 위의 테마 소개 페이지의 우측 링크를 `GEMFILE` 부분의 명령어를 이용해 다운로드 받을 수 있습니다.
또는 우측 사이드 메뉴의 Download를 이용해 바이너리 파일을 다운로드할 수도 있습니다.

.gem 파일이 위치한 경로에서 아래의 명령을 통해 테마를 설치할 수 있습니다.

```
sudo gem install xxxxx.gem
```

테마가 설치된 후에는 로컬에서 jekyll을 기동하여 적용된 테마를 확인하고, 필요한 작업들(스크립트나 스타일 적용 등)을 하시면 됩니다. (제 블로그에서는 modernist 테마를 적용한 후 일부 스타일을 조정하였습니다.)  
플러그인 활성화나 적용 및 셋팅 방법은 `Documentation` 메뉴에서 볼 수 있습니다.

<br/>

## GitHub Pages의 블로그에 테마 적용
GitHub Pages의 jekyll에 적용하는 방법은 아주 쉽습니다.
`_config.yml`에 `theme`만 추가하면 됩니다.

jekyll 경로의 Root에서 `_config.yml`을 열어 아래의 내용을 추가해 줍니다.  
만약 `theme`라는 항목이 있다면 테마 이름만 변경해 주세요.  
(자세한 셋팅 방법은 테마 소개 페이지의 `Documentation` 메뉴를 참고하시면 됩니다.)

```
theme: jekyll-theme-modernist
```

이제 `_config.yml`을 GitHub에 Push하시면 테마가 적용된 블로그를 볼 수 있습니다.
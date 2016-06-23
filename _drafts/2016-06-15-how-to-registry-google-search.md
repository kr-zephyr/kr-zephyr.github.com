---
layout: post
title:  "깃허브 Jekyll 블로그를 구글 검색에 노출시키기"
date:   2016-06-23 10:30:00 +0900
categories: jekyll
---
깃허브에 블로그를 운영하기로 결정하고 몇가지 포스트를 올려봤습니다.

그런데.. 구글 검색에 걸리지 않는 문제가..

일단 구글의 검색엔진 도구인 [`Search Console`](https://www.google.com/webmasters/tools/home){:target="_blank"}에 블로그를 연결하고 상황을 지켜보니 검색엔진에 전혀 노출이 안되고 있는 상황이었습니다.

> ### 구글의 Search Console 이란?
>
>[https://www.google.com/webmasters/tools/home](https://www.google.com/webmasters/tools/home){:target="_blank"}
>
>구글의 검색 엔진에 크롤링 및 인덱싱되는 상태를 확인할 수 있는 사이트 운영자용 도구입니다. 도메인을 등록해 두면 언제 크롤링이 되었고, 몇 페이지가 인덱싱되었는지, 어떤 키워드가 인덱싱되었는지, 키워드로 페이지가 얼마나 노출되었고 얼마나 히트되었는지 등의 통계를 볼 수 있습니다.
>
>![](/asserts/2016-06-15-how-to-registry-google-search/005.png)
>
>`Google Analytics`가 사이트에 대한 전반적인 통계를 제공한다면 `Search Console`은 구글 검색엔진에서의 사이트에 대한 통계, 도구를 제공하고 있습니다.
>
>구글을 이용한 검색 유입을 중요하게 생각한다면 꼭 이용해야 하는 도구입니다.

일단 사이트라도 크롤링이 되는지 확인하기 위해 구글 검색엔진에서 검색을 해봤습니다.

{% highlight text %}
site:kr-zephyr.github.io
{% endhighlight %}

결과가 전혀 나오지 않습니다.

구글에서 크롤링이 제대로 되고 있지 않은 것으로 보입니다.
이때 조치할 수 있는 방법은 몇가지가 있습니다.
- robot.txt 작성
- Search Console에 site map 제출
- 노출이 잘되고 있는 사이트 혹은 페이지에 링크 게제
- 구글에 강제 크롤링 신청

위의 방법은 시스템, 구글 검색 엔진을 이용한 일종의 꼼수이고 시간을 들여 SEO를 맞추는 것이 가장 효율적인 방법이긴 합니다.

하지만 저는 [SEO](https://support.google.com/webmasters/answer/35291?hl=ko){:target="_blank"}를 맞추는 것은 이후로 미루고 우선 빨리 검색 노출 여부를 판단하기 위해 위의 꼼수를 써봅니다. (블로그를 다른 곳으로 개설할지 여부를 판단하기 위해서...)

#### robot.txt 작성
원래는 robot.txt가 작성되어 있지 않았는데, 혹시나 하는 마음에 일반적인 모든 허용으로 robot.txt를 작성했습니다. robot.txt가 확인되지 않는 경우 구글 검색엔진은 사이트의 모든 내용을 크롤링하기 때문에 사이트의 모든 내용이 노출되길 원한다면 굳이 robot.txt를 만들 필요는 없습니다.

{% highlight text %}
User-agent: *
Allow: /

User-agent: Mediapartners-Google
Allow: /
{% endhighlight %}

#### Search Console에 site map 제출
다음으로 Search Console에 site map을 제출했습니다.
site map은 컨텐츠의 모든 링크 구조를 가지는 파일로 Jekyll에서는 RSS 규격의 xml 문서를 만들어 주므로 이를 활용했습니다.

![](/asserts/2016-06-15-how-to-registry-google-search/006.png)

site map은 제출하면 처리에 다소 시간이 걸리는 모양입니다. 총 4개의 페이지가 제출되었고, 이 포스트를 작성하는 6월 23일 기준으로 제출 후 18시간 정도가 지났는데 아직 처리가 되지 않았습니다.

#### 노출이 잘되고 있는 사이트 혹은 페이지에 링크 게제
기존에 검색에 잘 걸리고 있는 티스토리 블로그에 링크 추가 및 소개 포스트 하나 올림

#### 구글에 강제 크롤링 신청
http://www.google.com/submityourcontent 에 사이트를 등록하여 강제 처리하게 한다.

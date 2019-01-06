---
layout: post
title:  "Ruby gem 사용 시 SSL_connection 오류가 발생하는 경우 해결책"
date:   2017-01-25 18:00:00 +0900
categories: gem
tags: ['ruby','gem']
---

* content
{:toc}

오늘 블로그의 테마를 바꿨습니다.  
바꾸는 김에 jekyll의 로컬 실행을 위한 업데이트도 진행했구요. (사실 테마가 jekyll 3.3 이상을 요구해서 업데이트를...)

그런데 업데이트 중 오류를 만났습니다.  

jekyll은 루비 기반으로 개발되어 있는데요. 루비의 각종 기능을 이용하기 위해서는 rubygems(이하 gem)을 이용해야 합니다.  
이 gem에서 오류가 발생했습니다.



### gem 사용 시 SSL 오류 발생
{% highlight shell %}
D:\private-project\kr-zephyr.github.com.git-writing-non-ga>gem update jekyll
Updating installed gems
ERROR:  While executing gem ... (Gem::RemoteFetcher::FetchError)
    SSL_connect returned=1 errno=0 state=SSLv3 read server certificate B: certificate verify failed (https://api.rubygems.org/specs.4.8.gz)

D:\private-project\kr-zephyr.github.com.git-writing-non-ga>
{% endhighlight %}

위와 같이 jekyll의 업데이트를 실행하기 위해 `gem update jekyll`이라는 명령을 실행했는데 `ERROR:  While executing gem ... (Gem::RemoteFetcher::FetchError)`가 반환되었습니다.

이 오류는 gem이 서버에 접근하기 위해 https로 접근하면서 클라이언트 인증이 되지 않아 발생하는데요.  
rubygems 사이트에 해당 오류의 해결 방법, 즉, 인증서 업데이트 방법이 등록되어 있습니다.


### 해결 방법
참고 : [Ruby gems의 SSL CERTIFICATE UPDATES 가이드](http://guides.rubygems.org/ssl-certificate-update)

간단히 설명하면 rubygems-update-x.x.x.gem을 다운로드 받아 수동으로 업데이트하는 것으로 해결이 됩니다.  
위 링크에서 `INSTALLING USING UPDATE PACKAGES` 항목을 찾아 `rubygems-update-2.6.7.gem` 파일을 다운로드 받은 후 문서의 가이드에 따라 `gem install --local rubygems-update-x.x.x.gem` 명령으로 업데이트 하면 됩니다.



### 해결!...될 줄 알았는데...

하지만 항상 그렇듯이 한방에 되면 이상한거죠.  
당연하게도 저는 위의 방법으로 해결이 되지 않았습니다.  

위 문서에서는 저처럼 rubygems를 수동으로 업데이트하여 해결되지 않는 사람들을 위해 수동으로 인증서를 업데이트하는 방법을 가이드하고 있습니다.

[MANUAL SOLUTION TO SSL ISSUE](http://guides.rubygems.org/ssl-certificate-update/#manual-solution-to-ssl-issue)

위의 링크에서 가이드하는데로 Step by Step으로 처리하면 됩니다.  
다만, Step1에 `GlobalSignRootCA.pem`라는 인증서 링크가 있으니 이 인증서만 놓치지 않으시면 됩니다. 전 처음에 이게 인증서 파일 링크라고 생각하지 않고 그냥 다음 Step 들로 지나갔습니다;;;

인증서를 무사히 설치하고 나면...

{% highlight shell %}
D:\private-project\kr-zephyr.github.com.git-writing-non-ga>gem update jekyll
Updating installed gems
Updating jekyll
Fetching: colorator-1.1.0.gem (100%)
Successfully installed colorator-1.1.0
Fetching: forwardable-extended-2.6.0.gem (100%)
Successfully installed forwardable-extended-2.6.0
...
Parsing documentation for pathutil-0.14.0
Parsing documentation for public_suffix-2.0.5
Done installing documentation for addressable, colorator, forwardable-extended, jekyll, pathutil, public_suffix after 2 seconds
Gems updated: addressable colorator forwardable-extended jekyll pathutil public_suffix

D:\private-project\kr-zephyr.github.com.git-writing-non-ga>
{% endhighlight %}

요렇게 정상적으로 gem이 동작합니다.
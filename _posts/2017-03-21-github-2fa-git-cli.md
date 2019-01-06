---
layout: post
title:  "GitHub 2단계 인증 활성화 후 Command Line에서 인증하기"
date:   2017-03-21 21:00:00 +0900
categories: github
tags: ['github','2단계인증']
---
최근의 인터넷 서비스를 이용하다보면 2단계 인증이 많이 쓰이고 있는 것을 알 수 있습니다.  
2단계 인증은 ID와 비밀번호를 이용하던 기존 인증 체계에 추가적인 인증을 받는 강화된 인증 방식입니다.  
<br/>
기존보다 한단계(혹은 여러단계) 더 입력해야 할 것이 늘어나는 것만으로도 다소 번거롭기는 한데요.  
국내에서는 주로 SMS를 통한 인증이 많이 사용되고, 해외에서는 OPT 방식을 많이 사용하고 있는 것으로 보입니다.  
<br/>
이 OTP를 이용한 방식 중 Google에서 제공하는 OTP 기능을 많은 서비스에서 적용하고 있는데요.  
Google에서는 Authenticator라는 App을 통해 OTP 기능을 제공하고 있습니다. 이미 여러 게임 서비스사들이나 에버노트 같은 많은 서비스가 이 기능을 활용해 2단계 인증 서비스를 제공하고 있습니다.  
<br/>
![Google에서 제공하는 Authenticator App](/asserts/2017-03-21-github-2fa-git-cli/DSC05520.jpg)
<br/>
GitHub도 Google의 Authenticator App을 이용한 2단계 인증을 제공하고 있습니다.  
GitHub에서 2단계 인증을 활성화하는 것은 계정 Settings의 Security 항목에서 가능합니다. (자세한 내용은 직접해보세요. 어렵지 않아요... ^^)  
<br/>
2단계 인증을 통해 보안을 강화한 것은 좋은데, 저처럼 무턱대고 적용하면 몇가지 문제에 곧 봉착하게 됩니다.  
가장 큰 문제는 잘 사용하던 Atlassian의 SourceTree와 같은 git client에서 GitHub 계정에 대한 인증 오류가 발생합니다.  
그리고 Command Line을 이용한 git bash에서도 동일하게 발생하구요.  
사실 SourceTree나 git bash나 결국 같은 문제이기는 합니다. SourceTree가 내부적으로 git client를 통해 명령을 수행하기 때문이죠.  
<br/>
{% highlight shell %}
kr-zephyr@kr-zephyr-MBP:~/Documents/workspace/private_exmaple/test$git push
Username for 'https://github.com': kr-zephyr
Password for 'https://kr-zephyr@github.com': 
remote: Invalid username or password.
fatal: Authentication failed for 'https://github.com/kr-zephyr/private_exmaple.git/'
{% endhighlight %}
<br/>
위와 같이 git 명령을 수행할 때 GitHub에 인증하려고 하면 Authentication fail이 발생합니다.  
GitHub의 2단계 인증이 활성화되어 계정 정보 이외에 OTP를 통한 인증까지 받아야 하지만, GitHub와 무관한 Git Client에서는 이런 추가 인증 수행이 불가능하죠.  
<br/>
당장 손쉽게 해결할 수 있는 방법은 [GitHub의 공식 Desktop App](https://desktop.github.com)을 사용하는 방법입니다.  
<br/>
![GitHub Desktop](/asserts/2017-03-21-github-2fa-git-cli/01.jpg)  
<br/>
물론 GitHub Desktop App도 좋은 App이지만 그외에는 대안이 없느냐?  
아닙니다.  
<br/>
GitHub에서는 2단계 인증과 관련된 문서를 제공하고 있습니다.  
<br/>
참고 : [https://help.github.com/articles/providing-your-2fa-authentication-code](https://help.github.com/articles/providing-your-2fa-authentication-code)  
<br/>
GitHub의 공식 가이드 문서로 결론만 이야기 하자면 `Personal Access Token을 생성해서 비밀번호 대신 사용`하면 됩니다.  
<br/>
Personal Access Token이란 사용자가 임의로 생성할 수 있는 특별한 값입니다.  
이 Personal Access Token은 사용자의 목적에 따라 여러개를 생성할 수 있으며, 지금과 같이 GitHub 공식 채널이 아닌 git과 관련된 서비스, App 등에서 활용할 수 있습니다.  

### 백문이 불여일견!  

일단 이 Personal Access Token을 만들어보죠!  
<br/>
GitHub의 계정 설정(Settings)에 들어가 보면 좌측 메뉴의 제일 아래에 `Developer settings`라는 부분이 있습니다.  
여기에 `Personal Access Token` 메뉴를 통해 새로운 Token을 만들 수 있습니다.  
<br/>
![GitHub Settings의 Personal Access Token 페이지](/asserts/2017-03-21-github-2fa-git-cli/02.jpg)  
<br/>
우측 상단의 `Generate new token` 버튼을 이용해 새로운 Token을 생성할 수 있습니다.  
버튼을 클릭하면 아래와 같이 새로운 Token 생성 페이지로 이동합니다.  
<br/>
![New personal access token 페이지](/asserts/2017-03-21-github-2fa-git-cli/03.jpg)  

- Token description : 간단히 해당 토큰에 대한 이름 혹은 설명을 기입합니다.
- Select scopes : 이 토큰에 부여할 권한을 선택합니다.

사실 이 토큰은 GitHub의 개발자 API를 위하여 사용할 수 있는 토큰입니다.  
그래서 git Repository에 대한 권한 뿐만 아니라 사용자에 대한 Social 권한, 계정 권한 등도 포함하고 있죠.  
지금처럼 단순히 git client에서 사용하고자 할 경우 repo만 scope로 선택해도 충분합니다.  
<br/>
페이지 제일 하단의 `Generate token` 버튼을 선택하면 새로운 토큰이 발급됩니다.  
<br/>
![새로 발급된 token](/asserts/2017-03-21-github-2fa-git-cli/04.jpg)  
<br/>
위 그림처럼 화면에 현재 생성된 토큰이 노출됩니다.  
재빨리 토큰을 복사합니다. 왜냐하면 이 토큰은 딱 1번만 화면에 노출되기 때문입니다..  
화면을 리프레쉬하거나 다른 메뉴로 이동 후 다시 해당 페이지로 오면 아래와 같이 발급된 토큰 대신에 Token description이 노출됩니다.  
<br/>
![새로 발급된 token은 이제 안보여요.](/asserts/2017-03-21-github-2fa-git-cli/05.jpg)  
<br/>
만약 토큰이 다시 필요하다면 `Edit` 버튼을 누른 후 아래의 그림과 같이 편집 페이지에서 `Regenerate Token`으로 새로운 토큰을 발급받아야 합니다.  
당연히 새로운 토큰이 발급되면 기존 토큰은 사용할 수 없습니다. 보통 Git Client들은 Repository에 한번 계정 인증을 받으면 인증 정보를 별도로 저장하는데, 토큰을 재발급 받는 경우 이전에 저장된 토큰은 더 이상 유효하지 않으므로 다시 인증을 받아야 합니다.  
<br/>
![새로운 token을 발급받자.](/asserts/2017-03-21-github-2fa-git-cli/06.jpg)  
<br/>
이 토큰이라고 하는 녀석은 사실 오래오래 사용하면 안되는 녀석이긴 합니다.  
OAuth 인증을 공부해보셨거나 개발해 보셨다면 아시겠지만, Authorization Token은 인증 체계를 대신하는 특별한 값으로 짧게 사용하는 것이 좋습니다.  
사실 GitHub의 이 Personal Access Token이라는 것도 원래의 목적은 GitHub의 API에 접근하도록 허용하는데 OAuth용 값입니다.  
가능하면 각 클라이언트(혹은 서비스) 별로 별도의 토큰을 발급하고, 불필요해진 토큰은 바로 바로 파기해야 하는 것은 따로 언급하지 않아도 되겠죠?  
추가로 일정한 기간 후에는 토큰을 재발급 받아 기존 토큰이 너무 오래 사용되는 것을 방지하는 것도 보안에 좋은 방법입니다.  
<br/>
ps. 
위의 임시로 생성된 토큰은 이미 삭제되었으니 혹시라도 제 계정에 대해 인증 시도는 자제해주세요.  
GitHub Security 페이지에 보면 IP를 비롯해서 계정 접근 시도가 다 보여요~;;;;
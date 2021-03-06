---
layout: post
title:  "깃허브에 블로그를 만들면서..."
date:   2016-06-07 17:00:00 +0900
categories: devops-diary
tags: ['github', 'blog']
---

* content
{:toc}

아주 오래전(아마도 1997년...)부터 홈페이지라는 것을 운영하고 있었습니다.

몇번의 사이트 리뉴얼을 거쳐 지금은 티스토리 기반의 블로그가 되어 있는데요. [Digital Blue Eye (http://blog.sz21c.com)](http://blog.sz21c.com){:target="_blank"}라는 이름도 가지고 있는 한 때 정말 열심히 포스팅을 올리던 곳이었죠.(결혼하고 나니 좀 뜸해지긴 했네요. @.@)

블로그에는 소소한 생활 이야기, 취미 이야기를 쓰다가 개발자의 길을 걸으면서 개발에 대한 이야기도 조금씩 풀어가고 있었는데, 이런저런 잡탕 블로그보다는 체계적으로 무언가 쌓아볼 수 있는 블로그의 필요성을 느끼게 되었습니다.

올리려는 주제는 주로 개발, 개발자의 생활에 관련된 내용들이 될 것인데, 기술적인 이야기와 함께 일을 하면서 마주치는 여러가지 이야기도 풀어놓으면 나중에 세월이 흐르고나서 일종의 지식 저장소도 될 것 같고 개인적인 history도 될 듯 싶었습니다.

어떤 블로그 툴을 사용할까 여러가지 둘러보고 고민했었습니다.
후보가 되었던 것들은...

- 티스토리 이용 (기존 블로그는 티스토리에 둥지를 틀고 있습니다.)
- 워드프레스 서비스 이용
- 워드프레스 설치 이용
- 자체 개발(!)
- 깃허브 페이지 이용

등등이 후보로 올랐었는데, 최종적으로는 깃허브에 [jekyll](http://jekyllrb.com/){:target="_blank"}을 이용해서 블로그를 열게 되었습니다.

원했던 블로그 서비스는 아래와 같은 기능을 가지고 있어야 했습니다.

- 오프라인에서 글을 작성하고 쉽게 배포할 수 있어야 한다. (이미지 포함)
- Markdown으로 글을 작성할 수 있어야 한다.
- 여러가지 모험적 시도도 해보고 싶으니 어느정도 손을 댈 수 있는 포맷이어야 한다.
- 가능하면 빠른 시간에(가까운 시일 내에) 설치하고 운영을 시작할 수 있어야 한다.

사실 가장 적합했던 것은 워드프레스를 설치해서 사용하는 것이었습니다.
실제로 개인 서버에 워드프레스를 설치하고 테마 및 기본적인 플러그인 셋팅까지 진행했었지만 최종적으로는 깃허브에 둥지를 트는 것으로 방향을 바꾸었네요.

깃허브를 이용해 블로그를 운영하게 되면...

- 오프라인에서 Markdown 페이지를 작성한 후 즉시 등록이 가능하다.
- 이미지도 오프라인에서 참조하는 방식 그대로 사용할 수 있다. (온라인 블로그 서비스들은 이미지를 서버에 올리고 http로 참조해야 하죠. 어렵진 않지만 꽤 번거롭긴 합니다.)
- 개발자이니 깃허브를 여러가지로 이용해 봄으로써 좀 더 깃허브와 친해질 수 있다.
- 맥북에 붙어 있는 스티커가 부끄럽지 않아진다. (이건 순전히 겉멋만 들었네요...ㅜㅜ)

이런 장점들이 있습니다.

어쨋든 가능하면 한 주에 하나라도 포스팅을 올려보려 합니다.

이 블로그가 세월이 흘러 뒤를 돌아볼 수 있는 일기장과 기술적 지식을 쌓아놓은 지식 창고가 될 수 있었으면 좋겠네요.

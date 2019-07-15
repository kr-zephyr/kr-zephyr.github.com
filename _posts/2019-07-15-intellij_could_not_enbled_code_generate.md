---
layout: post
title:  "IntelliJ IDEA에서 어느날 code generate가 안된다면..."
date:   2019-07-15 21:24:00 +0900
categories: tools
tags: ['intellij', 'ide bug', 'code generate']
---

* content
{:toc}

### IntelliJ IDEA에서 code generate가 없어졌다.

어느날인가부터 IntelliJ IDEA(이하 IntelliJ)에서 code generate가 없어져 버렸습니다.

![Command + N을 누르면 나오는 Context Menu 라던가...](/asserts/2019-07-15-intellij_could_not_enbled_code_generate/004.jpg)
*(Command + N을 누르면 나오는 Context Menu 라던가...)*

![마우스 오른쪽 버튼을 누르면 나오는 Context Menu 라던가...](/asserts/2019-07-15-intellij_could_not_enbled_code_generate/002.jpg)
*(마우스 오른쪽 버튼을 누르면 나오는 Context Menu 라던가...)*

![상단 메뉴에서 Code를 누르면 나오는 하위 메뉴라던가...](/asserts/2019-07-15-intellij_could_not_enbled_code_generate/003.jpg)
*(상단 메뉴에서 Code를 누르면 나오는 하위 메뉴라던가...)*

Generate라는 기능은 소스의 일부를 자동 생성해주는 유용한 기능입니다.

특히 getter/setter 등의 귀찮은 단순 작업을 자동으로 해주는 꼭 필요한 기능이죠.

그.런.데. 어느날 이 Generate 기능이 사라졌습니다.

### Groovy 플러그인이 문제

알고보니. 이거 오래된 문제더군요.

꽤 오래전부터 있던 문제인데 Groovy Plugin을 해제하면 발생하는 문제라고 합니다. (근데 왜 아직도 안고치고 있는거지?)

![Preference > Plugins에서 Groovy 플러그인을 활성화!](/asserts/2019-07-15-intellij_could_not_enbled_code_generate/001.jpg)
*(Preference > Plugins에서 Groovy 플러그인을 활성화!)*

Groovy 플러그인을 활성화하고 IntelliJ를 재기동하면 깜쪽같이 기능이 돌아옵니다.

(이걸로 몇일을 끙끙... 플러그인 하나하나 다 해제해보고... 포럼을 일찍 뒤져볼껄... 근데 Groovy 플러그인은 언제 비활성화시킨거지? 기억이 없...)
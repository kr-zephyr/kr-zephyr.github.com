---
layout: post
title:  "[이슈대응] myBatis에서 Mapped Statements collection does not contain value for... Exception이 발생하는 경우 체크할 부분들"
date:   2016-08-11 15:14:00 +0900
categories: java mybatis resolve-issue
---
제가 종종 겪는 Exception 입니다.

보통은 프로젝트 초기 개발에 사용할 프레임워크를 처음 정의하는 단계에서 많이 마주쳤던 Exception으로 기억하네요.

{% highlight text %}
Caused by: java.lang.IllegalArgumentException: Mapped Statements collection does not contain value for xxx.xxx.xxx.TestDevDao.selectUserInfos
	at org.apache.ibatis.session.Configuration$StrictMap.get(Configuration.java:853)
	at org.apache.ibatis.session.Configuration.getMappedStatement(Configuration.java:686)
	at org.apache.ibatis.session.Configuration.getMappedStatement(Configuration.java:679)
	at org.apache.ibatis.session.defaults.DefaultSqlSession.selectList(DefaultSqlSession.java:147)
	... 43 more
{% endhighlight %}

이런 류의 Exception 발생하는 현상입니다.

일단 위의 Exception은 Mapper XML에서 해당 쿼리를 찾지 못하는 현상입니다. (좀 더 정확히는 Mapper XML을 찾지 못하는 문제입니다.)  
이 Exception이 발생했을 때 Configuration(Java Config 혹은 XML), Mapper XML, Dao, Spring DI 등의 여러가지 요소가 조합되다 보니 원인을 찾는게 까다로운 경우가 있습니다.

myBatis(혹은 iBatis)는 구성하는 방법이 여러가지가 있습니다.  
하지만 체크해야 할 부분이 특별히 많지는 않습니다. 다만, 개발자의 직감(혹은 '여기는 잘 해놨을거니까 안봐도 되'같은 나쁜 자신감 혹은 소홀함)으로 인해 세세히 확인하지 않고 멘붕에 빠져 원인을 못 찾는 경우가 많습니다. (제가 그렇...ㅜㅜ)  
결국 인터넷 검색(구글신께 물어봄)으로 넘어가게 되는데, 인터넷 검색으로 나오는 검색 결과를 무작정 믿으실 것은 아닌 것 같습니다. (대부분 작성하신 분들의 개발 환경, 소스 구성에 치우쳐 해결 방안을 이야기 하는 경우가 많으며, 일부 잘못된 내용이 전파되기도 합니다.)

위의 문제가 발생했을 때 체크해야 할 부분은 아래와 같습니다.  
다만, 사용 방법에 따라 다소 확인해야할 부분이 다른 곳이 있습니다.

### 1. Dao를 인터페이스로 구현하고 Mapper에서 쿼리 호출을 myBatis에 맡기는 경우  
Dao를 인터페이스로 구현하고 쿼리의 탐색 및 매핑을 myBatis에 맡기는 경우(즉, 자동 매핑)에는 MapperScan을 사용하게 됩니다.  
Java Config를 사용하는 경우 @MapperScan 어노테이션을 사용하게 되는데요, Mapper의 위치가 정확히 정의되었는지 살펴봐야 합니다.

@MapperScan을 사용하는 경우 Mapper XML을 직접 지정하는 것이 아닌 XML 파일의 위치까지만 지정합니다.

>예시1) @MapperScan({"**/dao"})   
>- 클래스 패스의 하위에서 모든 dao라는 패키지 안의 Mapper를 검색
>
>예시2) @MapperScan({com.sz21c.test.mybatis.dao})   
>- com.sz21c.test.mybatis.dao 패키지 하위를 검색.   
>- Maven/Gradle과 같이 빌드 플랫폼을 이용해 빌드할 때에는 resource로 정의된 위치 하위의 폴더는 패키지 구조 형태로 빌드되어 들어가므로 소스(src/main/java)의 하위 패키지 안에 XML 파일을 둔 것이 아닌 resource(src/main/resource)의 하위에 폴더로 구성한 경우 @MapperScan으로 정의된 패키지와 동일한 폴더 구조가 되어야 합니다.
    
### 2. Dao를 클래스로 구현하고 sqlSession을 이용해 직접 mapper의 쿼리를 호출하는 경우
이 경우 sqlSessionFactory에 MapperLocation을 주입하게 되는데, 이 때는 확장자까지 정의해야 합니다.

>예시) sqlSessionFactoryBean.setMapperLocations(new PathMatchingResourcePatternResolver().getResources("classpath*:**/dao/*.xml"));

만약 확장자를 제외하고 정의하는 경우 상황에 따라 전혀 엉뚱한 Exception 메시지를 받을 수 있습니다.
제가 테스트한 소스에서는 아래와 같은 메시지가 반환되었습니다.

{% highlight text %}
Caused by: com.sun.org.apache.xerces.internal.impl.io.MalformedByteSequenceException: 2은(는) 2바이트 UTF-8 시퀀스에 대해 부적합한 바이트입니다.
{% endhighlight %}

### 3. Dao의 패키지 위치
제가 종종 실수하는 부분입니다.

MapperScan 혹은 MapperLocation 주입 시 위와 같이 패키지 경로 상의 dao 패키지를 검색하도록 설정한 후 실제 Dao는 엉뚱한 곳에 생성하는 경우 입니다.

제 코딩 스타일로는 Dao를 구현한 후 package 정의를 복사하여 Mapper XML의 namespace에 붙여넣는데, 이 경우 Dao와 Mapper XML의 패키지는 동일하게 정의되지만, 생성된 패키지 위치가 엉뚱한 경우 Mapper XML을 찾지 못하게 됩니다.

지금까지의 제 경험 상으로는 위의 3가지만 체크하면 대부분 오류를 바로 잡을 수 있었습니다.

동일한 문제로 고생 중이신 개발자 분이 계시다면 도움되셨길 바랍니다.

## 참고. myBatis 셋팅 및 동작 시 조건
위와 같이 Dao를 인터페이스로 구현하는 방법, 클래스로 구현하는 방법과 같이 구현 방법이 차이, Dao와 Mapper의 매핑 등으로 myBatis를 이용할 경우 종종 실수를 하거나, 셋팅 조건을 혼동할 수 있습니다.

일부 인터넷 검색 시 결과에서는 Dao의 클래스 이름과 Mapper XML의 파일 이름을 맞춰야 한다거나, Dao에 구현된 method의 이름과 Mapper XML의 쿼리 id를 맞춰야 한다는 등의 설명이 있는데 모두 잘 못된 내용입니다.

Dao 클래스와 Mapper XML의 정확한 위치와 Dao의 패키지 네임, Mapper XML의 namespace만 맞추면 됩니다.

아래에 Dao를 인터페이스로 혹은 클래스로 구현 시  셋팅 및 동작 조건을 정리해 봤습니다.

### Dao를 인터페이스로 구현할 때
- Dao를 인터페이스로 정의하는 경우 MapperScan을 설정해야 한다. (Java Config에서는 @MapperScan 어노테이션 사용)
- Dao를 인터페이스로 정의하는 경우 Dao의 클래스 이름과 Mapper XML의 파일 이름이 달라도 상관없다.
- Dao를 인터페이스로 정의하는 경우 Dao의 method 이름과 mapper의 id는 반드시 같아야 한다.

### Dao를 클래스로 구현할 때
- Dao를 클래스로 정의하고 sqlSession을 사용하는 경우 SqlSessionFactory에 setMapperLocations을 반드시 설정해야 한다. (MapperScan을 사용하지 않음)
- setMapperLocations에 PathMatchingResourcePatternResolver로 Mapper의 위치를 주입하는 경우 반드시 Mapper의 namespace와 Dao의 Package name이 일치해야 한다.
    - 이 경우 Wrong namespace. Expected 'xxx.xxx.xxx.dao.TestDevMapper' but found 'TestDevDao'.로 메시지가 반환되므로 설정 중에 오류를 미리 알 수 있다.
- Dao를 클래스로 정의하고 sqlSession을 사용하는 경우 Dao의 클래스 이름과 Mapper XML의 파일 이름이 달라도 상관없다.
- Dao를 클래스로 정의하고 sqlSession을 사용하는 경우 Dao의 method 이름과 mapper의 id가 달라도 상관없다.

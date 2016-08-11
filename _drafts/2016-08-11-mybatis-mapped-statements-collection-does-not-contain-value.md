---
layout: post
title:  "[이슈대응] myBatis에서 Mapped Statements collection does not contain value for... Exception이 발생하는 경우 체크할 부분들"
date:   2016-08-11 15:14:00 +0900
categories: java mybatis
---
제가 종종 겪는 Exception 입니다.

보통은 프로젝트 초기 개발에 사용할 프레임워크를 처음 정의하는 단계에서 많이 마주쳤던 Exception으로 기억하네요.

###### 코드 부분
Caused by: java.lang.IllegalArgumentException: Mapped Statements collection does not contain value for xxx.xxx.xxx.TestDevDao.selectUserInfos
	at org.apache.ibatis.session.Configuration$StrictMap.get(Configuration.java:853)
	at org.apache.ibatis.session.Configuration.getMappedStatement(Configuration.java:686)
	at org.apache.ibatis.session.Configuration.getMappedStatement(Configuration.java:679)
	at org.apache.ibatis.session.defaults.DefaultSqlSession.selectList(DefaultSqlSession.java:147)
	... 43 more

이런 류의 Exception 발생하는 현상입니다.

일단 위의 Exception은 Mapper XML에서 해당 쿼리를 찾지 못하는 현상입니다.
여러가지 설정 방법들로 인해 종종 위 Exception이 발생하면 원인을 찾는게 까다로운 경우가 있는데요.
사실 까다롭기보다는 직감에 의해 철저히 하나하나 확인하지 않다보니 원인이 보이지 않는 경우가 많습니다.

myBatis(혹은 iBatis)를 구성하는 방법은 여러가지가 있는데요.
체크해야 할 부분이 특별히 많지는 않습니다. 다만, 개발자의 직감(혹은 '여기는 잘 해놨을거니까 안봐도 되'같은 나쁜 자신감 혹은 소홀함)으로 인해 세세히 확인하지 않고 멘붕에 빠지는 경우가 있습니다.
결국 인터넷 검색(구글신께 물어봄)으로 넘어가게 되는데, 인터넷 검색으로 나오는 검색 결과를 무작정 믿으실 것은 아닌 것 같습니다. (대부분 작성하신 분들의 개발 환경, 소스 구성에 치우쳐 해결 방안을 이야기 하는 경우가 많으며, 일부 잘못된 내용이 전파되기도 합니다.)

위의 문제가 발생했을 때 체크해야 할 부분은 아래와 같습니다.
다만, 사용 방법에 따라 다소 확인해야할 부분이 다른 곳이 있습니다.

1. Dao를 인터페이스로 구현하고 Mapper에서 쿼리 호출을 myBatis에 맡기는 경우
    이 경우 Configuration에서 MapperScan을 정의해야 합니다. Java Config를 사용하는 경우 @MapperScan 어노테이션으로 Mapper의 위치가 정확히 정의되었는지 살펴봐야 합니다.
    @MapperScan을 사용하는 경우 Mapper XML을 직접 지정하는 것이 아닌 XML 파일의 위치까지만 지정합니다.
    예시1) @MapperScan({"**/dao"}) --> 클래스 패스의 하위에서 dao라는 패키지 안의 Mapper를 검색
    예시2) @MapperScan({com.sz21c.test.mybatis.dao}) --> com.sz21c.test.mybatis.dao 패키지 하위를 검색 --> Maven/Gradle 빌드 시 resource로 정의된 위치 하위의 폴더는 패키지 구조 형태로 빌드되어 들어가므로 소스(src/main/java)의 하위 패키지 안에 XML 파일을 둔 것이 아닌 resource(src/main/resource)의 하위에 폴더로 구성한 경우 @MapperScan으로 정의된 패키지와 동일한 폴더 구조가 되어야 한다.
2. Dao를 Class로 구현하고 sqlSession을 이용해 직접 mapper의 쿼리를 호출하는 경우
    이 경우 sqlSessionFactory에 MapperLocation을 주입하게 되는데, 이 때는 확장자까지 정의해야 합니다.
    예시) sqlSessionFactoryBean.setMapperLocations(new PathMatchingResourcePatternResolver().getResources("classpath*:**/dao/*.xml"));
    만약 확장자를 제외하고 정의하는 경우 상황에 따라 전혀 엉뚱한 Exception 메시지를 받을 수 있습니다.
    (제가 테스트한 소스에서는 Caused by: com.sun.org.apache.xerces.internal.impl.io.MalformedByteSequenceException: 2은(는) 2바이트 UTF-8 시퀀스에 대해 부적합한 바이트입니다.라는 메시지가 반환되었습니다.)

#### 작성 시 참고사항
- Dao를 class로 정의하고 sqlSession을 사용하는 경우 SqlSessionFactory에 setMapperLocations을 설정해야 한다.
- setMapperLocations에 PathMatchingResourcePatternResolver로 Mapper의 위치를 주입하는 경우 반드시 Mapper의 namespace와 Dao의 Package name이 일치해야 한다.
    - 이 경우 Wrong namespace. Expected 'com.unitrontech.edms.admin.common.dev.dao.TestDevMapper' but found 'TestDevDao'.로 메시지가 반환되므로 알 수 있다.
- Dao를 class로 정의하고 sqlSession을 사용하는 경우 Dao와 Mapper XML의 이름이 달라도 상관없다.
- Dao를 class로 정의하고 sqlSession을 사용하는 경우 Dao의 method와 mapper의 id가 달라도 상관없다.
- Dao를 interface로 정의하는 경우 Config에 @MapperScan으로 설정해야 한다.
- Dao를 interface로 정의하는 경우 Dao와 Mapper XML의 이름이 달라도 상관없다.

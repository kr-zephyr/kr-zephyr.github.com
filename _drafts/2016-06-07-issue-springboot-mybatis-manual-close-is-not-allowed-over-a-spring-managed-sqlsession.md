---
layout: post
title:  "[이슈대응] Spring Boot에서 MyBatis 사용 시 Test에서 DB를 사용한 후 Test를 종료하거나, App을 종료할 때 java.lang.UnsupportedOperationException: Manual close is not allowed over a Spring managed SqlSession이 발생하는 경우"
date:   2016-06-12 10:30:00 +0900
categories: resolve-issue
---
얼마 전 Github에 공개해 둔 [SpringBootWebAppSample](https://github.com/kr-zephyr/SpringBootWebAppSample) 프로젝트를 손보면서 Test를 추가하던 중 아래와 같은 Exception을 받게 되었습니다.

{% highlight shell linenos %}
2016-06-07 14:23:04,260  WARN | o.s.beans.factory.support.DisposableBeanAdapter         | Invocation of destroy method 'close' failed on bean with name 'sqlSessionForMyBatis'
java.lang.UnsupportedOperationException: Manual close is not allowed over a Spring managed SqlSession
	at org.mybatis.spring.SqlSessionTemplate.close(SqlSessionTemplate.java:310)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:497)
	at org.springframework.beans.factory.support.DisposableBeanAdapter.invokeCustomDestroyMethod(DisposableBeanAdapter.java:354)
	at org.springframework.beans.factory.support.DisposableBeanAdapter.destroy(DisposableBeanAdapter.java:277)
	at org.springframework.beans.factory.support.DefaultSingletonBeanRegistry.destroyBean(DefaultSingletonBeanRegistry.java:578)
	at org.springframework.beans.factory.support.DefaultSingletonBeanRegistry.destroySingleton(DefaultSingletonBeanRegistry.java:554)
	at org.springframework.beans.factory.support.DefaultListableBeanFactory.destroySingleton(DefaultListableBeanFactory.java:972)
	at org.springframework.beans.factory.support.DefaultSingletonBeanRegistry.destroySingletons(DefaultSingletonBeanRegistry.java:523)
	at org.springframework.beans.factory.support.DefaultListableBeanFactory.destroySingletons(DefaultListableBeanFactory.java:979)
	at org.springframework.context.support.AbstractApplicationContext.destroyBeans(AbstractApplicationContext.java:1006)
	at org.springframework.context.support.AbstractApplicationContext.doClose(AbstractApplicationContext.java:982)
	at org.springframework.context.support.AbstractApplicationContext$1.run(AbstractApplicationContext.java:901)
{% endhighlight %}

문제 자체는 MyBatis에서 DB 접근을 위해 SqlSession을 생성한 후 App이 종료되면서 생성되었던 SqlSession을 해제하려고 하면서 발생되는 Exception입니다.

메시지 자체는 Warning으로 프로그램이 동작하는데에는 직접적 영향을 주지 않지만 Warning이라고 그냥 둘 수는 없는 일.

여기저기 확인을 해봤는데... SpringBoot에서의 사례는 그리 눈에 보이지 않습니다.

그러던 중 StackOverFlow의 어느 글을 통해 해당 부분은 MyBatis의 버그이고 1.2.4 버전에서 수정되었다는 글을 보게 되었습니다.

[mybatis-spring을 1.2.4로 업데이트 후(기존에는 1.2.2를 사용)](https://github.com/kr-zephyr/SpringBootWebAppSample/commit/57f427e00274fb78b01313faa34c2a07506f582c) 위의 메시지는 더 이상 출력되지 않습니다.

혹시 같은 문제로 고민 중이신 분들이 계시다면 본 포스트와 같이 라이브러리 업데이트를 해보세요.

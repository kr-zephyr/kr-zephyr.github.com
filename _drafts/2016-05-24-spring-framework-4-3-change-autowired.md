---
layout: post
title:  "Spring Framework 4.3 변경 사항 - 단일 Constructor인 경우 @Autowired 생략 가능"
date:   2016-05-24 17:38:00 +0900
categories: SpringFramework
---
Spring Framework의 Annotation 중 `@Autowired`는 상당히 많이 사용하는 Annotation이다.

`@Autowired`는 Spring Framework에서 관리하는 Bean을 주입해 주는 역할을 한다. (자세한 내용은 공부하도록...)

우선 기존의 코드부터 보면...

{% highlight java %}
@RestController
public class RestTestController {

    private TestService testService;

    @Autowired
    public RestTestController (TestService testService) {
        this.testService = testService;
    }

    @RequestMapping("/api/{id}")
    public @ResponseBody RestModel getId(@PathVariable String id) throws Exception {
        return testService.getModel(id);
    }
}
{% endhighlight %}

위와 같이 Constructor를 이용해 Denpendency를 주입하는 경우 Spring Framework 4.2에서는 반드시 `@Autowired`를 명시해야 한다. Spring Framework 4.3에서는 만약 Constructor가 1개라면 `@Autowired`를 생략할 수 있다.

아래의 소스 참고.

{% highlight java %}
@RestController
public class RestTestController {

    private TestService testService;

    public RestTestController (TestService testService) {
        this.testService = testService;
    }

    @RequestMapping("/api/{id}")
    public @ResponseBody RestModel getId(@PathVariable String id) throws Exception {
        return testService.getModel(id);
    }
}
{% endhighlight %}

다만, Constructor를 사용하지 않고 변수에 직접 `@Autowired`를 명시하는 경우에는 기존과 동일하게 사용해야 한다. (아래 소스 참고)

{% highlight java %}
@RestController
public class RestTestController {

    @Autowired
    private TestService testService;

    @RequestMapping("/api/{id}")
    public @ResponseBody RestModel getId(@PathVariable String id) throws Exception {
        return testService.getModel(id);
    }
}
{% endhighlight %}

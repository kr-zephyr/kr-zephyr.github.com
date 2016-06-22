## 6. Spring Framework 4.3의 새로운 기능 및 개선점

### 6.1 Core Container 개선점
- 만약 목표로하는 bean이 오직 하나의 constructor를 가지고 있다면 `@Autowired`는 더 이상 기술할 필요가 없다.
- `@Configuration` 클래스들은 생성자 주입을 지원한다.
- 모든 SpEL 표현식은 bean들을 참조할 수 있는 `@EventListener`의 상태를 기술하는 것에 사용할 수 있다. (즉, `@beanName.method()`)
- 구성된 annotation들은 array의 component type의 단일 요소와 함께 meta-annotation들 중 array attribute를 이제 override할 수 있다. 예들 들면, `@RequestMapping`의 String[] path attribute는 구성된 annotation 중 String path와 함께 override될 수 있다.
- `@Scheduled`와 `@Schedules`는 attribute override와 함께 커스텀화로 구성된 annotaion들을 생성하는데 meta-annotation들처럼 이제 사용될 수 있다.

### 6.2 Data Access 개선점
- `jdbc:initialize-database`와 `jdbc:embedded-database`는 각각의 script에 적용된 설정할 수 있는 구분자를 지원한다.

### 6.3 Caching 개선점
Spring 4.3은 단 한번만 계산되도록 주어진 key에 대한 동시 호출을 동기화할 수 있다. 이것은 선택적 기능으로 @Cacheable의 새로운 sync attribute를 통해 활성화해야 한다. 이 기능의 추가된 get(Object key, Callable<T> valueLoader) 메소드같은 Cache 인터페이스에 대한 주요 변경을 소개한다.

Spring 4.3은 아래와 같은 캐싱 개념(caching abstraction) 또한 개선했다.

- cache들의 SpEL 표현식-관계된 annotation들은 bean들을 참조할 수 있다. (즉, @beanName.method())
- ConcurrentMapCacheManger와 ConcurrentMapCache는 새로운 storeByValue attribute를 통해 cache 구성원들의 serialization(병렬)을 이제 지원한다.
- @Cacheable, @CacheEvict, @CachePut과 @Caching은 이제 attribute 대체와 함께 커스텀 구성된 annotation들을 생성하는 meta-annotation으로 사용될 수 있다.

### 6.4 JMS 개선점
- @SendTO는 이제 공유된 공통 응답 목적지를 클래스 레벨에서 지정 될 수있다.
- @JmsListener와 @JmsListeners는 이제 attribute 대체와 함께 커스텀 구성된 annotation들을 생성하는 meta-annotation으로 사용될 수 있다.

### 6.5 Web 개선점
- HTTP HEAD와 HTTP OPTIONS의 내장 기능으로의 지원
- @RequestMapping의 새로운 @GetMapping, @PostMapping, @PutMapping, @DeleteMapping 그리고 @PatchMapping

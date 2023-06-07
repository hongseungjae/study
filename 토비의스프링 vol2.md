1장
***

* 스프링은 오브젝트의 생성과 관계설정, 사용, 제거 등의 작업을 코드가 아닌 독립된 컨테이너가 담당 -> 컨테이너가 오브젝트의 대한 제어권을 갖고있음 -> IoC 컨테이너
* 오브젝트의 생성과 오브젝트 사이의 런타임 관계를 설정하는 DI 관점 -> 빈 팩토리
* 빈 팩토리에 여러 가지 컨테이너 기능을 추가한 것 -> 애플리케이션 컨텍스트
* 애플리케이션 컨텍스는 BeanDefintion으로 만들어진 메타정보를 담은 오브젝트를 사용해 IoC와 DI작업을 수행 -> 메타정보는 특정한 파일 포맷이나 형식에 제한되거나 종속되지않음
* IoC컨테이너는 POJO 클래스와 설정 메타정보를 결햅해서 하나의 애플리케이션을 만듬
 
* IoC 컨테이너의 역할은 초기에 빈 오브젝트를 생성하고 DI 한 후에 최초 애플리케이션을 기동할 빈 하나를 제공해주는 것
  - 자바 프로그램은 main() 메소드를 가진 클래스 시작시켜달라고 요청
  - 하지만 웹에서는 main() 메소드를 호출할 방법이 없으며, 사용자도 여럿이고 동시에 웹 애플리케이션을 사용
  - 서블릿이 일종의 main() 역할을 실행
  - 요청이 서블릿으로 들어올 때마다 getBean()으로 필요한 빈을 가져와 정해진 메소드 실

* 스프링은 프론트 컨트롤러 패턴을 사용 : 몇 개의 서블릿이 중앙집중식으로 모든 요청을 다 받아서 처리하는 방식

* 서블릿 한개당 애플리케이션 컨텍스트가 구성되고, 웹 애플리케이션에 루트 애플리케이션 컨텍스트를 부모를 두고있음 -> 계층 구조 유지이유는 웹 기술에 의존적인 부분과 그렇지 않은 부분을 구분하기 위해

* 스프링의 웹 기능을 지원하는 프론트 컨트롤러 서블릿은 DispatcherServlet, 서블릿이 초기화 될 때 자신만의 컨텍스트 생성하고 초기화, 루트 애플리케이션 컨텍스를 찾아서 자신의 부모 컨텍스트로 사용

* @Componet 지정하면 빈 등록이 가능, @Component를 포함해 디폴트 피털에 적용되는 애노테이션을 스테레오타입 애노테이션이라고함

* 빈 스캐너 단점 : 애플리케이션에서 등록될 빈이 어떤 것들이 있고, 어떻게 정의되는지 한눈에 파악 할 수 없음, XML처럼 상세한 메타정보 항목을 지정 안됨, 클래스당 한 개 이상의 빈을 등록못함

* 디폴트로 정의돈 빈은 싱글톤임, 따라서 return new annotatedHello()를 실행해도 새 객체가 아닌 빈 오브젝트가 반복적으로 리턴, @Bean이 붙은 메소드를 조작

* XML보다 자바코드 이점
  1. 컴파일러나 IDE를 통한 타입 검증 가능, XML은 텍스트문서
  2. 자동완성 기능 최대한 이용
  3. 이해하기 쉬움
  4. 복잡한 빈 설정이나 초기화 작업을 손쉽게 적용

* 멀티 컨텍스트에서 중복 빈 스캐닝으로 문제가 발생할 수 있음(서블릿 컨텍스트와 루트 컨텍스트에 두 개 다 빈이 등록되어 서블릿 컨텍스트에 트랜잭션 aop가 적용이 안된문제)

* 자동와이어링, byName, byType, 타입에 의한 방식은 빈의 이름이나 프로퍼티 이름에 신경을쓰지 않아도 돼서 편리함, 대신 타입이 같은 빈이 두 개 이상 존재하는 경우 적용안됨

* 필드 주입은 테스트 코드 작성하기가 불편함, 왜냐하면 컨테이너가 주입해줘야하기 때문, 그러나 dao처럼 컨테이너 통합테스트일 경우는 고려해볼만함
* 수정자 주입은 외부에서 주입이 가능하다, 그러나 초기화 중 잊어버릴 수 있음, 또 수정자 메소드가 많아질 수 있음
* 생성자 주입은 null이 들어갈 위험이 없다. final을 이용해서, 그러나 모든 프로퍼티를 다 di하게 강제함, 유연성이 떨어질 수 있음

* @Resource 자동 주입 방법은 xml 자동주입과 다르게 빈을 못찾으면 예외 발생, 디폴트 이름으로 참조할 빈을 찾음 -> 타입을 이용해 한 번 더, 이름을 이용한 프로퍼티 설정
  - 수정자, 필드 주입

* @Autowired 스프링 전용 애테이션, @Injext는 JavaEE 6의 표준 스펙에 정의되어있는 것
  - 생성자, 필드, 수정자, 일반 메소드로 네 가지로 확장
  - @Resource와 다르게 이름 대신 필드나 프로퍼티 타입을 이용해 후보 빈을 찾음
  - @Autowired는 타입이 같은 여러빈을 컬렉션이나 배열로 선언하여 다 받을 수 있음
  - @Autowired에서 타입 외의 정보를 추가해서 세밀하게 도움 주는 보조 방법은 @Qualifier를 사용하는것
  - 이름을 매핑할때 -> @Resource,  타입과 한정자 매칭할 때 -> @Autowired, @Qualifier

* @Autowired와 같은 애노테이션을 통한 의존관계 설정은 빈 오브젝트 등록을 마친 후에 후처기에 의해 별도의 작업으로 진행됨

* @Value에 직접 값을 지정하는 방법은 잘사용하지 않음
 - 대신 자바 코드 외부의 리소스나 환경정보에 담긴 값을 사용하도록 지정해줌, @Value("#systemProperties['os.name']}"), @Value("${database.username}")

* 빈 후처리기는 매 빈 오브젝트가 만들어진 직후에 오브젝트의 내용이나 오브젝트 자체를 변경할 때 사용
* 빈 팩토리 후처리기는 빈 설정 메타정보가 모두 준비됐을 때 빈 메타정보 자체를 조작하기 위해 사용(PropertyPlaceHolderconfigurer), 치환자를 찾지 못해도 예외가 발생하지않음

* 값주입에 SpEL을 이용하여 능동적으로, 오타와 같은 실수가 있을 때 에러 검증 가능, 프로퍼티를 빈으로 만들고, 그 빈의 이름으로 값을 주입

* 컨테이너가 자동등록하는 빈
  - ApplicationContext, BeanFactory
    - @Autowired로 자동주입, 그게 안되면 ApplicationContextAware 인터페이스를 구현
  - ResourceLoader, ApplicationEventPublisher
  - systemProperties, systemEnvironment

* 기본적으로 스프링의 빈은 싱글톤
  - 매 요청마다 애플리케이션 로직을 담은 오브젝트를 만드는 건 비효율적
  - 하나의 빈에 동시에 여러 스레드가 접근하기때문에, 상태 값을 갖는 인스턴스 변수를 저장해두고 사용할 수 없음 -> 필드에는 빈에 대한 레퍼런스나 읽기전용 값만
  - DTO 등은 파라미터나 리턴 값을 전달하면 싱글톤에서 사용해도 아무런 문제 없음

* 싱글톤이 아닌 빈은 프로토타입과 스코프 빈(웹어플리케이션)
  - 프로토타입 빈은 컨테이너에게 빈을 요청할 때마다 매번 새로운 오브젝트를 반환해줌
  - 프로토타입 빈은 반환하는 순간 컨테이너에게 관리가 안되고 주입받은 오브젝트에게 관리됨, 그 오브젝트 가 싱글톤이면 프로토타입 빈도 생명주기가 싱글톤으로 유지
  - 매번 새로운 오브젝트가 필요한데 DI가  필요한 오브젝트일 때 사용

* request를 컨트롤러와 서비스계층에서 모두 사용할 경우 163p
  - request 안에서 dao에 접근해서 member를 세팅해놓기
  - 이때 request는 di를 받아야됨 -> 빈으로 만들기 -> 프로토타입으로, @Componet @Scope("prototype")
  - 빈 가져오기 this.conext.getBean(ServiceRequest.classs);, @Autowired로 가져오면 새로 생성되지않음 주의하기 -> DL (getBean하거나 Provider로 타입으로 주입 받아서 get하기)

* DL 전략
  1. ApplcationContext, BeanFactory
     - ApplicationConext를 DI를 가져오면 부담이됨, 스프링 api가 직접 코드에 등장함, 테스트 시 거대한 저 객체를 모킹해야됨
  2. ObjectFactory, ObjectFactoryCreatingFactoryBean
     - 중간에 ApplicationConext를 요청해서 ServiceReqeust빈을 찾아오는 팩토리 빈 만들기
  3. ServiceLocatorFactoryBean
     - @Autowired ServiceRequestFactory serviceRequestFactory;로 사용가능
  4. 메소드 주입
     - abstract public ServiceRequest getServiceRequest();로 사용가능, \<lookup-method\> 사용
  5. Provider\<T\>
     - @Inject Provider\<ServiceRequest\> serviceRequestProvider로 사용가능, 따로 빈 등록 X


* 스코프의 종류
  - 싱글톤, 프로토타입 외 요청, 세션, 글로벌세션, 애플리케이션 네 가지 스코프 
  - 스코프는 프로토타입과 다르게 컨테이너가 전 과정을 관리 

* 스코프 빈은 DL 대신 스코프 프록시를 이용하여 DI를 해줄 수 있음
  - @Scope(value="session", proxyMode-ScopedProxyMode.TARGET_CLASS)

* @Configuration/@Bean, @Autowred 같은 애노테이션을 이용한 빈 의존 관계 설정 방식, @PostConstruct를 통한 빈 초기화 메소드 기능 모드 스프링 컨테이너가 기본적으로 제공하는 기능이 아님
  - 스프링 컨테이너의 기능을 확장할 수 있는 컨테이너 인프라 빈이 제공하는 기능임
  - context:annotation-config 태그를 등록하면 됨 -> 이 태그는 context 네임스페이스의 태그를 처리하는 핸들러를 통해 특정 빈이 등록되게함 -> 그 특정빈이 빈의 등록과 관계 설정 등 새로운 기능을 부여하는 컨테이너 인프라빈
  - 선언하면 여러빈이 등록되며, 그 빈들이 @Configuration 처리하고, @Autowired를 처리함, 각각 역할에 맞춰서
  - component-scan은 @Configuration처리, @Atuwired도 처리, annotation-config는 빈 스캐너기능은 안됨

* 빈 등록정보 조회 유틸리티 클래스 197p
* 빈 등록관련 200p
* 스프링 1.x -> xml을 통한 빈 등록 bean 태그
* 스프링 2.0 -> aop:config, tx:advice namespace 태그로 좀 더 깔끔하게 xml 정리
* 스프링 2.5 -> @Component처럼 애노테이션만으로도 빈 등록 가능, 그러나 외부라이브러리에 @Component를 사용불가
* 스프링 3.0 -> 자바 코드를 이용해 빈설정코드를 만들수있음
* 스프링 3.1 -> 인프라빈도 자바코드로

* AnnotationConfigWebApplicationContext는 context:annotation-config이 등록해주는 빈을 기본적으로 추가해줌

* 런타임추상화 -> 프로파일
* getEnvironment() 현재 애플리케이션 컨텍스트에 적용된 활성 프로파일이 무엇인지 확인
* getActiveProfiles() 활성 프로파일 목록
* @Autowired Environment로 init()할때 값 주입, 혹은 @Value로 바로 주입(PropertysourcePlaceholderConfigurer 빈은 static 메소드로 등록)

2장
***

* DAO패턴은 데이터 액세스 기술을 외부에 공개해서는 안되는 것 -> 코드에 영향을 주지않고 데이터 액세스 기술을 변경하거나 하나 이상의 데이터 액세스 기술을 혼합해서 사용할 수 있게 해줌
* DAO 예외도 메소드 선언부에 throws SQLException과 같은 내부 기술을 드러내는 예외를 직접 노출시키면 안됨
  - 데이터 액세스 기술에서 던져주는 예외에 일관성이 없음 -> 스프링이 데이터 예외 추상화를 제공(JdbcTemplate과 같은)

* 템플릿/콜백 패턴으로 , try/catch/finally 중복되는 코드 제거
* DB 연결 풀 기능 -> DataSource
* JDBC는 자바의 데이터 액세스 기술의 기본이 되는 로우레벨의 API
  - JDBC는 표준 인터페이스를 제공하고 각 DB벤더는 이 인터페이스를 구현한 드라이버를 제공 -> SQL의 호환성만 유지한다면 DB가 변경되어도 코드 그대로 재사용
  - 그러나 반복 코드, 체크 예외를 처리해야함, close 안할 시 등 문제 -> 스프링 JDBC로 극복

* 스프링 JDBC가 해주는 작업
  - Connection 열기와 닫기
  - Statement 준비와 닫기, 실행
  - ResultSet 루프
  - 예외처리와 변환(SQLException을 런타임 예외인 DataAccessException 타입으로 변환)
  - 트랜잭션 처리

* 스프링 JDBC에서 가장 많이 이용 -> SimpleJdbcTemplate, SimpleJdbcInsert -> 3.1에서 @Deprecated, 대신 JsbcTemplate과 NamedParameterJdbcTemplate 이용
* ibatis 사용법 270p
* 바이트코드 향상 기법 : 이미 컴파일된 클래스 바이트 코드를 조작해서 새로운 기능을 추가하는 것
* 런타임 시에 클래스를 로딩하면서 기능을 추가하는 것 : 로드타임 위빙 -> 스프링 JPA에서 사용

* 선언적 트랜잭션 경계설정 기능을 이용하면 코드 내에서 직접 트랜잭션을 관리하고 트랜잭션 정보를 파라미터로 넘겨서 사용하지 않아도됨 <-> 트랜잭션 스크립트 방식
  - 비즈니스로직과 데이터액세스 로직을 분리

* PlatformTansactionManager를 DI 받아서 getTransaction() 해보면 현재 진행중인 트랜잭션 확인 가능

* 인터페이스 없이 직접 dao클래스를 사용하는 경우 불필요한 메서드에도 트랜잭션 동작, final 사용불가
* 셀프이보케이션 문제
   - 프록시를 가져와서 그 프록시로 호출
   - AspectJ AOP 이용

* 트랜잭션 전파 : 트랜잭션을 시작하거나 기존 트랜잭션에 참여하는 방법을 결정하는 속
* 트랜잭션 격리수준 : 동시에 여러 트랜잭션이 진행될 때에 트랜잭션의 작업 결과를 여타 트랜잭션에게 어떻게 노출할 것인지를 결정하는 기준


3장
***

* 스프링의 HTTP 처리
  1. 서블릿컨테이너는 HTTP 프로토콜을 통해 들어오는 요청이 스프링의 DisPatcherServlet에 할당된 것이라면 HTTP 요청 정보를 전달함
  2. DiPatcherServlet은 공통적으로 진행해야 하는 전처리 작업 등을 함(보안, 파라미터 조작, 한글 디코딩 등)
  3. URL이나 파라미터 정보, HTTP 명령 등으 참고해 어떤 컨트롤러에게 작업을 위임할지 결정 -> 핸들러 매핑 전략, 컨트롤러를 핸들러라고도함(웹의 요청을 다루는 오브젝트라는 의미)
     - 이 핸들러 매핑 전략은 전략패턴임, 맞는 핸들러를 그냥 DI해주면 됨
  4. 컨트롤러를 위임이 결정됐으면 그 컨트롤러의 메소드를 호출해야됨 -> 어떻게 제각각 다른 메소드와 포맷으 가진 오브젝트를 컨트롤러를 만들어놓고 DispatcherServlet이 알아서 호출하게 할 수 있을까?
  5. 어댑터 패턴 이용 -> 컨트롤러가 어떤 메소드를 가졌고, 어떤 인터페이스를 구현했는지 전혀 알지못함, 각 어댑터가 컨트롤러에게 맞는 호출 방법을 이용해서 작업 요청을 하고 결과를 받아서 DispatcherServlet에게 넘겨줌
  6. 모델과 뷰를 리턴
  7. HTTP 응답 돌려주기

* DisPatcherServlete의 DI 가능한 전략
  1. HandlerMapping
  2. HandlerAdapter
  3. HandlerExceptionResolver
  4. ViewResolver
  5. LocaleResolver
  6. ThemeResolver
  7. RequestToViewNameTranslator


* 간단하게 만들어보기
  1. SimpleControllerHandlerAdapter를 이용하여 커스텀 컨트롤러 처리하기 -> Controller 인터페이스를 구현한 핸들러를 처리함, 즉 어댑터에서 처리할수 있는 인터페이스를 컨트롤러에서 구현
  2. Controller 인터페이스는 ModevlAndView handleRequest(HttpServletRequest request, HttpServletResponse response) 가진 메서드
  3. 해당 인터페이스를 구현한 HelloController를 만들자
  4. 이제 이 HelloController의 handleRequest가 SimpleControllerHandlerAdapter를 통해 DispatcherServlet으로부터 호출될 것
  5. 이제 DispatcherServlet이 핸들러 매핑을 해야되는데 BeanNameUrlHanlderMapping임 -> <bean name="/hello" class="springbook.temp.HelloController" /> name에 경로를 줌
  6. 그러면 요청 경로를 이용해서 HelloController를 찾고, 그 handler를 처리해줄 adpater를 찾는구나 나이스
  7. 그리고 InternalResourceViewResolver 뷰리졸버를 이용해서 컨트롤러가 리턴한 뷰 이름에 해당하는 뷰 오브젝트를 가져오고 HTTP 응답결과를만들어냄
  8. 정리 -> 요청이 들어오면 DispatcherServlet이 요청정보를 분석해 핸들러를 찾음, 그 핸들러는 특정 인터페이스를 구현하고있는데, 그 인터페이스를 처리해줄수있는 어댑터를 for문을 돌면서 찾음, 찾으면 어댑터에게 처리요청을함(만약 어댑터를 안쓰면, 새로운 컨트롤러를 추가할때마다 소스 수정되야됨)

* MockHttpServletRequest, MockHttpServletResponse로 테스트 가능
* DispatcherServlet 테스트 시 ConfigurableDispatcherServlet 활용, AbstractDispatcherServletTest 활용
* 서블릿처럼 동작하는 컨트롤러를 만들기위해, 서블릿은 모델과뷰 리턴이 없으므로 HttpRequestHandler의 void handleRequest()메소드를 구현하고, 디폴트 어댑터 전략인 HttpRequestHandlerAdapter를 이용하면됨

* 커스텀 컨트롤러를 만들기위해 Controller인터페이스를 직접 구현하는건 권장되지 않음, 적어도 필수 기능이 구현되어 있는 AbstractController를 상속해서 컨트롤러를 만드는게 편하기 때문
  - 예를 들어 Method를 제한하려면 직접코드를 짜는게 아닌 구현되어있는 쓸수있음
  
* 간단히 Controller는 인터페이스를 구현한 abstract 기반 클래스를 두고 이를 구현하게 사용
  - HttpServletRequest rowlevel 코드를 감추고, 뷰를 세팅하거나, 필요한 request 파라미터를 세팅해두고 이를 호출하는 메서드를 abstract로 (템플릿메서드)

* AnnotationMehtodHandlerAdapter(스프링 3.2에서 deprecated RequestMappingHandlerAdapter변경) : 여타 핸들러 어댑터는 지원하는 컨트롤러의 타입이 정해져있지않음
  - 애노테이션의 정보와 메소드 이름, 파라미터, 리턴 타입에 대한 규칙 등을 이용하고 컨트롤러 선별
  - 컨트롤러 하나가 하나 이상의 URL에 매핑될 수 있음
  - URL을 매핑을 컨트롤러단위가 아닌 메소드 단위로

* 핸들러 매핑 기본 전략
  - BeanNameUrlHandlerMapping
    - 빈의 이름에 들어 있는 URL과 HTTP 요청의 URL 비교해서 일치하는 빈
    - /root/**/sub 일경우 **는 하나 이상의 경로를 포함
  - 특정 전략을 빈으로 등록하면 디폴트 핸들러 매핑은 등록하지않음을 주의
  - RequestMappingHandlerMapping
    - @RequestMapping이라는 애노테이션을 컨트롤러 클래스나 메소드에 직접 부여함
    - 컨트롤러의 개수를 줄일 수 있는 장점

* 핸들러 인터셉터
  - 핸들러 매핑의 역할은 컨트롤러 빈을 찾아주는 것, 그리고 핸들러 인터셉터를 적용해주는 것
  - 컨트롤러를 호출하기 전과 후에 요청과 응답을 참조하거나 가공할 수 있는 일종의 필터
  - 핸들러 매핑은 DispatcherServlet으로부터 매핑 작업을 요청받으면 그 결과로 핸들러 실행 체인(HandlerExcutionChain)을 돌려줌
  - 서블릿 필터와 그 쓰임새가 유사한데 HttpServletRequest, HttpServletResponse뿐 아니라, 실행될 컨트롤러 빈 오브젝트, 돌려줄 ModelAndView, 발생한 예외 등을 제공받을 수 있음, 또한 자체가 빈이기때문에 DI를 통해 다른 빈을 활용
  - 서블릿은 모든 요청에 적용, 핸들러는 특정 핸들러 매핑으로 제한
  - 인터셉터 대신 컨트롤러에 aop 적용은? -> 메소드마다 파라미터 리턴 제각각이므로 쉽지 않음

* 확장컨트롤러
  - 컨트롤러 인터페이스를 정의하고, 애노테이션을 이용하여 엘리먼트 값을 이용해 정보를 넣어줌
  - 어댑터에서 이 인터페이스 타입 support 해놓고, 애노테이션에서 정보 뽑아서 활용하기

* 핸들러 예외 리졸버
  - HandlerExceptionResolver는 컨트롤러의 작업 중에 발생한 예외를 어떻게 처리할지 결정하는 전략

* HandlerExceptionResolver 인터페이스 구현 전략
  1. AnnotationMehtodHandlerExceptionResolver
     - 예외가 발생한 컨트롤러 내의 메소드 중에서 @ExceptionHandler 애노테이션이 붙은 메소드를 찾아 예외처리를 맡겨주는 핸들러 예외 리졸버
  2. ResponseStatusExceptionResolver
     - 예외 클래스에 @ResponseStatus를 부팅고, 단순한 HTTP 500 에러 대신 의미 있는 응답상태 제공
  3. DefaultHandlerExceptionResolver
     - 위의 두 가지 예외 리졸버에서 처리하지 못한 예외를 다룸, 표준 예외처리 로직 가지고 있음
  4. SimpleMappingExceptionResolver
     - 예외와 그에 대응되는 뷰 이름을 매핑

* 플래시 맵 : 플래시 애트리뷰트를 저장하는 맵
  - 하나의 요청에서 생성되어 다음 요청으로 전달되는 정보 -> Post/Redirect/Get 패턴을 적용한 경우 POST단계의 작업 결과 메시지를 리다이렉트된 페이지로 전달할 때 주로 사용


* WebApplicationInitializer 통해 web.xml 등 설정 작업을 모두 자바 코드로 가능하게함

4장
***

* 제네릭스와 매피정보 상속을 이용해 컨트롤러 작성 480p
  - 도메인별로 CRUD와 검색 기능을 가진 메소드가 중복돼서 등장
  - abstract GenericController<T, K, S>를 구성해 컨트롤러에서 상속받게 만듬
  - 컨트롤러 코드가 매우 간결해지고 개발 생산성을 높여줌
 
 * @Controller를 담당하는 어댑터 핸들러는 상당히 복잡함
   - 사용할 수 있는 파라미터나 리턴 값의 종류 등 다양하게 처리할수 있게만들어야 돼서

* 컨트롤러 메서드 파라미터
  - @ReqestParm은 String, int , 복잡한오브젝트 @ModelAttribute 
  - @ModelAttribute는 검증 작업이 추가적으로 진
  - @ModelAttribute 는 예외 발생 시 BindException 타입의 오브젝트에 담겨서 컨트롤러로 전달, 수정할 기회를 주기위해 파라미터로 BindingResult 타입의 파라미터를 같이 사용
  - @RequestBody는 HTTP 요청의 본문 부분이 그대로 전달
    - HttpMessageConverter 타입의 메시지 변환기가 여러개 등록
    - HTTP 요청의 미디어 타입과 파라미터 타입을 확인해서 처리할 수 있는 처리기 있으면 처리해서 파라미터로 전달
    - Json일 경우 MappingJacksonHttpMessageConverter를 사용
  - 수정폼관련한 문제를 해결하기위해 @SessionAttributes 활용 - 수정폼을먼저 저장, 나중에 변경폼이 오면 세션에 저장해놓은것을 꺼내고 변경폼에서 전송해준 파라미터만 바인딩
  - 세션에 저장된 폼을 제거하기위해 SessionStatus 사용

* 스프링 파라미터 변환은 프로퍼티에디터를 사용함
  - 커스텀 프로퍼티 에디터 만들려면 PropertyEditorSupport 확장한 클래스 만들기
  - @InitBinder를 컨트롤러에 등록해서 WebDataBinder에 추가하기
  - 많은 곳에서 사용된다면 WebBindingInitializer를 이용하기 ( 디폴트핸들러어댑터도 추가해줘야댐)
  - 프로퍼티 에디터는 공유되면 안됨, new 로 새로만듬 -> 만약 DI가 필요하다면? -> 프로토타입 빈
  - 변환되어야할게 객체 안의 객체라면? -> 그 객체의 키값만 따로 DB조회해서 넣어주기, 커스텀 프로퍼티에디터 사용해서 페이크 객체 만들기(id값만 이용해서 가짜 객체 만들어서 세팅) 546p, 아니면 실제 객체 만들기, 3가지 방법
  - 그냥 dto를 만들면? -> 데이터 중심 아키텍처, 화면 단위로 코드를 만들어야됨
  - 548p


* 프로퍼티에디터는 매번 객체 생성, 쓰레드 세이프 하지 않아서 싱글톤으로 사용불가 -> 스프링 3.0에서 Converter로 변경 , 멀티스레드 환경에서 안전함, 싱글톤 가능
  - 프로퍼티데이터는 문자열과 오브젝트 사이의 양방향 변환 기능, Converter는 소스타입에서 타깃 타입으로 단방향만 변환 가능 -> 양쪽 두개 만들어야 양방향

* Converter 타입은 ConversionService 타입의 오브젝트를 통해 WebDataBinder에 설정
  - @InitBinder를 통한 수동 등록
  - ConfigurableWebBindingInitializer를 이용한 일괄 등록

* GenericConversionService에 여러가지 디폴트 컨버터가 있음

* Formatter는 Locale 타입의 현재 지역 정보도 함께 제공됨, FormattingConversionServce의 메소드를 이용하여 등록
  - @NumberFormat
  - @DataTimeFormat

* 바인딩 기술 선택하기
  - 사용자 정의 타입의 바인딩을 위한 일괄 적용 : Converter
  - 필드와 메소드 파라미터, 애노테이션 등의 메타정보를 활용하는 조건부 변환 기능: ConditionalGenericConverter
  - 필드에 부여하는 애노테이션 정보를 이용해 변환 긴능 지원하려면 AnnotationFormatterFactory와 Formatter
  - 특정 필드에만 적용되는 변환 기능 : PropertyEditor

* 바인딩 적용 우선 순위
  1. 커스텀 프로퍼티
  2. 컨버전 서비스의 컨버터
  3. 디폴트 프로퍼티 에디터

* WebDataBinder는 HTTP 요청정보를 컨트롤러 메소드의 파라미터나 모델에 바인딩할때 사용되는 바인딩오브젝트
  - allowedFields, disallowedFields
  - requiredFields
  - fieldMarkerPrefix
  - fieldDefaultPrefix

* 검증 과정에서 사용할 수 있는 Validator 표준 인터페이스 제공
  - 검증 결과는 BindingResult에 저장
  - supports, validate 구현

* 검증 방법
  1. 컨트롤러 메소드 내의 코드
  2. @Valid
  3. 서비스 계층 오브젝트에서의 검증
  4. 서비스 계층을 활용하는 Validator
  5. 빈 검증 기능 @NotNull, @Min

* 커스텀 검증 빈 만들기 576p
  - ConstraintValidator를 구현한 MembeerNoValidator 만듥
  - @MemberNo에 @Constraint(validatedBy=MemberNoValidator.class) 등록

* 에러 코드를 통해 MessageCodeResolver는 좀 더 상세한 메시지 키 값으로 확장됨
  - MesaageSource를 통해 messages.properties에 내용을 가져옴
  - 규모가 커지면 메시지를 수정하는 일이 힘들 테니 에러 코드와 메시지  프로퍼티 파일을 활용이 좋음

* 메시지 컨버터는 AnnotationMethodHandlerAdapter를 통해 등록
  - @RequestBody와 @ResponseBody를 이용해 사용
  - ByteArrayHttpMessageConverter
  - StringHttpMessageConverter
  - FormHttpMessageConverter
  - SourceHttpMessageConverter
  - 그 외에 디폴트는 아니지만 자주 쓰이는 MappingJacksonHttpzmessageConverter
 
* AnnotationMethodHandlerAdapter 확장 포인트 -> deprecated로 아래의 RequestMappingHandler참고하기
  - SessionAttributeStore
    - 다른 방식으로 세션 정보를 저장할 때, SessionAttributeStore 인터페이스를 구현함
  - WebArgumentResolver
    - 컨트롤러의 메소드 파라미터를 확장할 수 있음
  - ModelAndViewResolver

* RequestMappingHandlerMapping : @RequestMapping이 붙은 메소드로 매핑해줌
  - 기존의 핸들러 매핑전략은 핸들러를 돌려주면 그 특정 메소드를 실행시키는 것
  - 그러나 @RequestMapping으로 인해 핸들러가 오브젝트 단위에서 메서드 단위로 바뀜
  - HandlerMethod를 넘겨줌 -> 메소드르 실행하는데 필요한 관한 참조정보를 담고 있는 오브젝트
    - 빈 오브젝트, 메소드 메타정보, 메소드 파라미터 메타정보, 메소드 애노테이션 메타정보, 메소드 리턴 값 메타정보
  - RequestMappingHandlerMapping은 DispatherServlet이 시작될 때 모든 컨트롤러 빈의 메소드를 살펴서 매핑 후보가 될 메소드를 추출한 뒤 이를 HandlerMethod형태로 저장해두고, 실제 요청이 들어오면 저장해둔 목록에서 요청 조건에 맞는 HandlerMethod 오브젝트를 돌려줌

* 핸들러 메소드의 매핑 기준이 되는 정보 : request condition(요청 조건)
  - URL 패턴 : PatternsRequestCondition
  - HTTP 요청방법 : RequestMethodsRequestCondition
  - 파라미터 : ParamsRequestCondition
  - 헤더 : HeadersRequestCondition
  - Content-Type 헤더 : ConsumesRequestCondition
  - Accept헤더 : ProducesRequestCondition

* RequestMappingHandlerAdapter : HandlerMethod 타입의 핸들러를 담당하는 핸들러 어댑터
  - @Validated(그룹 검증), @Valid 지원
  - @Valid와 @RequestBody
  - URI를 생성하거나 가공할 때 UriComponentsBuilder 이용
  - RedirectAttributes와 리다이렉트 뷰

* RequestMappingHandlerAdapter 확장 포인트
  - 파라미터 : HandlerMethodArgumentResolver -> 새로운 파라미터타입 추가시 해당 인터페이스를 구현 후 추가
  - 리턴 값 : HanderMethodReturnValueHandler

* @EnableWebMvc와 WebMvcConfigurationSupport 659p

5장
***

* aop를 만드는 방법은 인터페이스 구현과 애노테이션방식 혹은 aop:aspect 네임스페이스방식
  - 인터페이스는 어드바이저 개념, 후자는 AspectJ의 애스펙트 
* @AspectJ는 이름 그대로 AspectJ AOP 프레임워크에서 정의된 애노테이션을 이용해 애스펙트를 만들 수 있게 해줌, 하지만 문법과 애스펙트 정의 방법을 차용했을 뿐, AspectJ AOP를 사용하는 것은 아님, 스프링의 프록시 기반 AOP를 만들 때 사용

* 직접 프록시를 생성
  - AOP 실행 과정 client -> proxy -> target
  - client에서 Interface에 @Autowired 주입되게 사용불가 -> 왜? proxy 빈과 target 빈 둘 중 무엇을 주입해줘야될지 구분이 안됨, 같은 인터페이스를 구현하였기때문

* 자동 프록시 생성
  - @Autowired의 타입에 의한 의존관계 설정에 문제가 없음 -> 타깃빈을 대체해서 자기가 빈으로 등록됨
  - AOP 적용은 다른 빈들이 Target 오브젝트에 직접 의존하지 못하게함, 직접 의존하게되면 AOP적용시 Target 오브젝트가 Proxy 빈 안에 숨어버리면서 DI 대상을 차지못함, 인터페이스를 통한 의존관계를 따르면 발생할일 없음

* 인터페이스는 단지 DI만을 위해 좋은 것이 아님 -> 다른 오브젝트가 자신에게 접근 할 때 특정 메소드만 사용하도록 할 수 있음, 심지어 public이라도 할지라도 자유롭게 바꿀 수 있음 -> 불필요한 결합도를 낮춤, AOP를 포함해서 DI의 활용 방법을 손쉽게 적용

* 인터페이스 없이 프록시 만드는 방법 -> 상속
  - final 클래스와 final 메소드에는 적용이 안됨
  - 생성자 두 번 호출, 같은 타깃 클래스 타입의 빈이  두 개 만들어지기 때문
  - CGLib이라는 바이트 코드 생성 외부라이브러리 필요
  - 인터페이스처럼 프록시로 노출할 메소드를 선별할 수 없음
  - 레거시 코드나 외부에서 개발한 라이브러리의 클래스 등에도 AOP를 적용할 수 있게 해주려는 것

* @AspectJ AOP
  - 객체지향 언어의 클래스와 비슷한 개념
  - 부가기능을 추상화 해놓은 것
  - 하나 이상의 포인트컷과 어드바이스로 구성
  - 어드바이저는 하나의 포인트컷과 하나의 어드바이스로 정의된 가장 단순한 형태의 애스펙트
  - 애스펙트는 다양한 조합을 갖는 포인트컷과 어드바이스를 하나의 모듈로 정의
  - @EnableAspectJAutoProxy, @Aspect, @Pointcut, @Before, @After를 이용
  - 일반 메소드 필드, 상속, 인터페이스 구현 등 평범한 POJO 클래스처럼 , @AspectJ방식 AOP 개발의 장점
  - 포인트컷에서 조인포인트는 메서드 실행 지점

* 스프링 AOP는 메서드 호출지점에 적용가능, 객체 생성 지점은안됨 -> AspectJ기술로 만ㄷ르어진 DependencyInjectionAspect 애스펙트를 이용, @Configurable, 로드타임 위버(클래스 로딩 시점에 바이트 코드조작)

* 스프링은 다양한 서버환경에서 사용 가능한 편리한 로드타임 위버를 제공해줌, @EnableLoadTimeWeaving

6장
***











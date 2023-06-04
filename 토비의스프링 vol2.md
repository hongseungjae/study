============================== 1장
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
  - 빈 가져오기 this.conext.getBean(ServiceRequest.classs);, @Autowired로 가져오면 새로 생성되지않음 주의하기

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
  - 스코프는 프로토타입과 다르게 컨테이너가 전 과정을 관

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

======================= 2장

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


========================== 3장


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










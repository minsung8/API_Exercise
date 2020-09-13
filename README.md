# API_Exercise

Rest API 구성
- 자원 : Data, Meta Data, HATEOAS
- 행위 : HTTP Method로 표현
- 표현 


REST의 특징

- Uniform Interface(유니폼 인터페이스)
  구성 요소(클라이언트, 서버 등) 사이의 인터페이스는 균일(uniform)해야합니다.
  인터페이스를 일반화함으로써, 전체 시스템 아키텍처가 단순해지고, 상호 작용의 가시성이 개선되며, 
  구현과 서비스가 분리되므로 독립적인 진화가 가능해질 수 있습니다.

- Stateless (무상태성)

  클라이언트와 서버의 통신에는 상태가 없어야합니다. 모든 요청은 필요한 모든 정보를 담고 있어야합니다.
  요청 하나만 봐도 바로 뭔지 알 수 있으므로 가시성이 개선되고, task 실패시 복원이 쉬우므로 신뢰성이 개선되며,
  상태를 저장할 필요가 없으므로 규모 확장성이 개선될 수 있습니다.

- Cacheable (캐시 가능)

  캐시가 가능해야합니다. 즉, 모든 서버 응답은 캐시가 가능한지 그렇지 아닌지 알 수 있어야합니다. 
  효율, 규모 확장성, 사용자 입장에서의  성능이 개선됩니다.
  
- Self-descriptiveness (자체 표현 구조)

  REST의 또 다른 큰 특징 중 하나는 REST API 메시지만 보고도 이를 쉽게 이해 할 수 있는 
  자체 표현 구조로 되어 있다는 것입니다.

- Client - Server 구조

  클라이언트-서버 스타일은 사용자 인터페이스에 대한 관심(concern)을 데이터 저장에 대한 관심으로부터 분리함으로써
  클라이언트의 이식성과 서버의 규모확장성을 개선할 수 있습니다.

- Layered System(계층형 구조)

  REST 서버는 다중 계층으로 구성될 수 있으며 보안, 로드 밸런싱, 암호화 계층을 추가해 구조상의 유연성을 둘 수 있고
  PROXY, 게이트웨이 같은 네트워크 기반의 중간매체를 사용할 수 있게 합니다.
  
 
REST API 설계 가이드
- URI는 자원의 정보를 표현해야 함
- 자원에 대한 행위는 HTTP Method (GET, POST, PUT, DELETE)로 표현
- URI에 HTTP Method가 들어가면 안됨
- URI의 행위에 대한 동사가 들어가면 안됨
- 경로 부분 중 변하는 부분은 유일한 값으로 대체 
- 슬래쉬 구분자(/)는 계층 관계를 표현
- 마지막에 슬래쉬 구분자 사용 안됨
- 하이픈(-) 사용 가능
- 밑줄(_) 사용 불가
- 파일 확장자는 URI에 포함하지 않습니다. Accept header를 사용하도록 합니다.
예) http://edwith.org/files/java.jpg (X)
예) GET /files/jdk18.exe HTTP/1.1 Host: edwith.org Accept: image/jpg (O)
- 리소스 간에 연관 관계가 있는 경우 다음과 같은 방법으로 표현합니다.
/리소스명/리소스 ID/관계가 있는 다른 리소스명
예) GET : /books/{bookid}/viewers (일반적으로 소유 ‘has’의 관계를 표현할 때)
- 자원을 표현하는 컬렉션(Collection)과 도큐먼트(Document)
컬렉션은 객체의 집합, 도큐먼트는 객체라고 생각하면 됩니다. 컬렉션과 도큐먼트 모두 리소스로 표현할 수 있으며 URI로 표현할 수 있습니다.
예) http://edwith.org/courses/1 
courses는 컬렉션을 나타냅니다. 복수로 표현해야 합니다. courses/1 은 courses중에서 id가 1인 도큐먼트를 의미합니다.

HATEOAS
- 결과에 관련된 REST API에 대한 정보

MessageConvertor
- 자바 객체와 HTTP 요청 / 응답 바디를 변환하는 역할
- @ResponseBody, @RequestBody
- @EnableWebMvc 로 인한 기본 설정
- WebMvcConfigurationSupport 를 사용하여 Spring MVC 구현
- Default MessageConvertor 를 제공

Json 응답하기
- 컨트롤러의 메소드에서는 Json으로 변환될 객체를 반환
- jackson라이브러리를 추가할 경우 객체를 JSON으로 변환하는 메시지 컨버터가 사용되도록 @EnableWebMvc에서 기본으로 설정됨
- jackson라이브러리를 추가하지 않으면 JSON메시지로 변환할 수 없어 500오류가 발생
- 사용자가 임의의 메시지 컨버터(MessageConverter)를 사용하도록 하려면 WebMvcConfigurerAdapter의 configureMessageConverters메소드를 오버라이딩





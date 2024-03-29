 
# Spring 소개
 * Spring 1.0 버전은 2004년 3월 출시
   * 20년 가까이 자바 엔터프라이즈 어플리케이션 개발의 최고의 자리를 차지했다.
    * 엔터프라이즈 어플리케이션이란??
* 스프링 프레임 워크의 구성은 20여가지로 구성되었고 (https://spring.io/projects/spring-framework), 스프링의 핵심 기능(DI, AOP, etc)를 제공하며 필요한 모듈만 선택 가능하다.
* 현재 단일 아키텍처(Monolith) 에서 마이크로서비스 아키텍처로 넘어가는 추세에 따라 스프링도 진화하는 추세이다.
* 여러가지 모듈이 있지만, 단연 스프링부트, 스프링 클라우드, 스프링 데이터, 스프링 배치, 스프링 시큐리티 등에 중점을 둔다.

# Spring 소개 (좀 더 기술적인 관점에서)
* Spring의 과제는 **테스트의 용이성** 과 **느슨한 결합** 에 중점을 둔다.
* 작성/테스트가 어려웠던 자바EE 어플리케이션
   * 데이터베이스와 같이 외부에 의존성을 두는 경우 단위테스트가 불가능했다.
   * 느슨한 결합이 된 어플리케이션 개발이 힘들었다.
* IOC의 등장: 다른 프레임워크와 가장 큰 차이점을 보여주는 부분이다. 차후 깊게 설명할 것.
* AOP: AOP를 사용하여 로깅, 트랜잭션 관리, 시큐리티에서의 적용 등 AspectJ와 같이 와녑ㄱ하게 구현된 AOP와 통합하여 사용가능하다. 역시 차후 깊게 설명할 것.

# Spring을 도식으로 보여준다면?
POJO라는 삼각형의 각 변에 
* IOC/DI(의존 관계 주입)
* AOP 관점 중심 프로그램
* PSA 이식 가능한 추상화

# JAVA Design Pattern

## 디자인 패턴 Overview

> 01.아키텍처와 패턴 - The History of IT System

> 01.아키텍처와 패턴 - Cloud Native Architecture

- 확장 가능한 아키텍처

  - 시스템의 수평적 확장에 유연
  - 확장된 서버로 시스템의 부하분산, 가용성 보장
  - 시스템 또는 서비스 애플리케이션 단위의 패키지(컨테이너 기반 패키지)
  - 모니터링

- 탄력적 아키텍처

  - 서비스 생성, 통합, 배포, 비즈니스 환경 변화에 대응 시간 단축
  - 분할된 서비스 구조
  - 무상태 통신 프로토콜
  - 서비스의 추가와 삭제 자동 감지
  - 변경된 서비스 요청에 따라 사용자 요청 처리

- 장애 격리(Fault isolation)
  - 특정 서비스에 오류가 발생해도 다른 서비스에 영향을 주지 않음

> 01.아키텍처와 패턴 - Architecture Pattern ?

- 아키텍처 패턴이란?

  - 소프트웨어 아키텍처의 공통적인 발생 문제에 대한 일반적인, 재사용 가능한 해결책
  - 디자인 패턴과 비슷하지만 더 넓은 범위
  - 컴퓨터 하드웨어 성능 제한, 비즈니스 위험의 최소화와 고가용성(HA), 모니터링 등 소프트웨어 공학의 다양한 문제 해결
  - 일부 아키텍처 패턴은 소프트웨어 프레임워크 안에 구현

- Architecture Pattern
  - Action Domain Responsor(Model-View-ViewModel, Model-View-Controller 등)
  - Layers
  - EDA(Event-driven-architecture)
  - Hexagonal architecture
  - MicroService architecture
  - Entity-control-boundary
  - Service-oriented architecture

> 01.아키텍처와 패턴 -JavaEE Architecture

> 01.아키텍처와 패턴 - Layer Pattern

- Client Layer → Presentation Layer
- Presentation Layer → Service Layer
- Service Layer → Data Access Layer
- Data Access Layer → Resource Layer

> 01.아키텍처와 패턴 - MVC Pattern

- Model
  - 애플리케이션 상태의 캡슐화
  - 상태 쿼리에 대한 응답
  - 애플리케이션의 기능 표현
  - 변경을 View에 통지
- View
  - 모델을 화면에 시각적으로 표현
  - 모델에게 업데이트 요청
  - 사용자의 입력을 컨트롤러에 전달
  - 컨트롤러가 View를 선택하도록 허용
- Controller
  - 요청 입력 값 체크
  - 사용자 액션을 모델 업데이트와 Mapping
  - 일정 범위에 모델 데이터 저장
  - 응답에 대한 View 선택

> 01.아키텍처와 패턴 - MSA Pattern

> 02.방법론과 패턴

> 03.객체지향설계 SOLID - 객체지향 특징

- Abstraction
  - 복잡한 현실세계를 사용자 요구에 맞게 단순화
- Encapsulation
  - 구현은 감추고 사용법 제공
- Inheritance
  - 부모 클래스의 멤버 변수와 멤버 메소드 자식 인스턴스 통해 사용
- Polymorphism
  - 객체의 다형성 : 상속을 전제로 부모타입의 자식 생성자로 다양한 객체 생성
  - 메소드의 다형성 : 부모타입의 메소드를 상속 받은 자식 클래스에서 재정의, 부모타입의 객체 사용 메소드 호출 시 재정의된 메소드 응답
- 클래스의 종류
  - Concrete Class
  - Abstract Class
  - Interface
- Cohesion(응집도)와 Coupling(결합도)
  - High Cohesion : 한 모듈 내부의 처리 요소들은 서로 관련도가 높게
  - Loosely Coupling : 서로 다른 모듈 간에 상호 의존 느슨하게

> 03.객체지향설계 SOLID - SOLID

- Single Responsibility Principle(단일책임의 원칙)
  - 객체는 단 하나의 책임만을 가져야 한다.
- Open Closed Principle(개방폐쇄원칙)
  - 소프트웨어 요소는 확장에는 열려 있으나 변경에는 닫혀 있어야 한다.
  - 기존의 코드를 변경하지 않으면서 기능을 추가할 수 있도록 설계
- Liskov Substitution Principle(리스코프 치환 원칙)
  - 특정 클라이언트를 위한 인터페이스 여러 개가 범용 인터페이스 하나보다 낫다.
  - 클라이언트가 자신이 이용하지 않는 메서드에 의존하지 않아야 한다.
- Dependency Inversion Principle(의존관계 역전 원칙)
  - 추상화에 의존 해야지, 구체화에 의존하면 안된다.
  - 소프트웨어 모듈들을 분리하는 특정 형식을 지칭한다. 이 원칙을 따르면, 상위 게층(정책 결정)이 하위 계층(세부 사항)에 의존하는 전통적인 의존관계를 반전(역전)시킴으로써 상위 계층이 구현으로부터 독립

> 04.디자인 패턴 개요 - 의미와 역사

- 디자인 패턴?

  - 소프트웨어 공학의 소프트웨어 디자인에서 특정 문맥에 공통적으로 발생하는 문제에 대해 재사용 가능한 해결책

- 역사
  - 건축적 개념으로서의 패턴은 크리스토퍼 알렉산더(1977/79)가 창안
  - 1987년,, 켄트 벡과 워드 커닝햄은 프로그래밍, 구체적으로는 패턴 언어에 패턴을 적용하는 개념에 관한 실험을 시작
    - OOPSLA 컨퍼런스에서 자신들의 결과를 제시
  - 1994년 Erich Gamma, Richard Helm, Ralph Johnson, John Vlissides 등 4인(GoF, Gang of Four) - "디자인 패턴(Design Patterns: Elements of Reusable Object-Oriented Software)" 출간
    - 다양한 패턴을 정리하고 일반화하여 일반적인 객체지향 소프트웨어 설계 문제에 집중
  - J2EE, .NET 등의 아키텍처 구성을 위한 패턴들도 발표

> 04.디자인 패턴 개요 - 구성과 분류

## 생성 패턴 Creational Pattern

> Singleton Pattern

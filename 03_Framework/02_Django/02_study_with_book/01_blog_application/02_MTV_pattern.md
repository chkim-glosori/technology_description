# MTV Pattern

## 1. MTV 패턴이란?
MTV 패턴은 Django에서 사용하는 아키텍처 패턴으로, "Model-Template-View"의 약자이다. 이 패턴은 웹 애플리케이션의 구조를 정의하며, 각 구성 요소가 어떤 역할을 하는지 설명한다.

> 디자인 패턴과 아키텍처 패턴은 다른 것

### 1-1. 디자인 패턴
디자인 패턴은 소프트웨어 개발 중에 자주 발생하는 특정 문제를 해결하기 위한 일반적인 해결책을 제시하는 패턴이다. 주로 객체지향 프로그래밍에서 사용된다. 싱글톤, 팩토리, 옵저버, 전략 패턴 등이 있다. 특정 상황에서의 구현 방법과 절차를 제시하는 것이 디자인 패턴의 특징이다.

### 1-2. 아키텍처 패턴
아키텍처 패턴은 소프트웨어 시스템의 구조를 정의하는 고수준의 패턴으로, 시스템의 구성 요소 간의 관계와 상호작용을 설명한다. MVC, MTV, 레이어드 아키텍처, 이벤트 기반 아키텍처 등이 있다.

### 1-3. 디자인 패턴과 아키텍처 패턴의 차이
디자인 패턴은 특정 문제를 해결하기 위한 일반적인 방법론을 제공하는 것이며, 개별 클래스나 모듈의 설계를 중점으로 한다. 그러나, 아키텍처 패턴은 시스템의 전체 구조와 설계를 다루며, 구성 요소 간의 관계를 정의한다. 간단히 정의하면, 아키텍처 패턴의 범위가 시스템 전역으로 더 넓다고 얘기할 수 있다.

* 파이썬에서, 하나의 모듈 == 하나의 파일 != 하나의 클래스

## 2. MTV 패턴의 각 요소

### 2-1. Model
데이터베이스와의 상호작용을 담당한다. Spring 에서의 JPA (ORM) 격이라고 할 수 있다. 데이터베이스의 구조와 비즈니스 로직을 정의한다.

각 모델은 클래스 형태로 정의되며, 각 클래스는 데이터베이스의 테이블에 매핑된다. Spring 처럼, 데이터의 유효성 검사 및 제약 조건을 정의할 수 있다.

### 2-2. Template
사용자에게 보여 줄 HTML 을 생성한다. FE 부분을 담당하며, UI 를 구성한다.

Spring 에서 Thymeleaf 와 같은 Template Engine 을 사용하여 동적인 HTML 을 생성하는 방식과 유사하다.

Template 를 사용하면 서버 사이드 렌더링을 하지만, Template 를 사용하지 않고 클라이언트 사이드 렌더링을 하는 방법도 있다.

클라이언트 사이드 렌더링은 주로 React 와 같은 JavaScript 프레임워크를 사용하여 클라이언트에서 HTML을 생성하는 방식으로, 서버는 RESTful API를 통해 데이터를 제공한다.

> 서버 사이드 렌더링 vs 클라이언트 사이드 렌더링

서버 사이드 렌더링 방식은 서버에서 완전한 HTML 페이지를 생성하여 사용자에게 페이지를 건네는 방식이다. 이런 경우 서버에서 완전한 HTML 페이지를 생성하기 때문에 검색 엔진이 페이지 내용을 쉽게 인식할 수 있어 검색 엔진 최적화(SEO) 에 유리하다는 장점이 있다. 또한, 사용자가 페이지를 요청하면 서버에서 미리 렌더링된 HTML 을 제공하기 때문에 초기 속도가 빠르다.

다만, 모든 요청에 대해 서버가 HTML 을 렌더링해야 하므로 서버의 부하가 증가할 수 있고, 페이지를 전환할 때 전체 페이지를 새로 로드해야 하기 때문에 사용자 경험이 저하된다.

클라이언트 사이드 렌더링을 하면 JS 서버를 통해 서버의 부하를 분산시킬 수 있고, 전체 페이지를 새로 로드하지 않아도 된다.

또한, API 로 데이터를 받아온 후, 이 데이터를 상태로 저장하고 UI 를 업데이트하는 과정에서 클라이언트 애플리케이션의 메모리에 저장되고, 렌더링 과정에서 필요에 따라(상태 관리 같은 코드) 사용된다.

결론적으로, API 요청을 통해 데이터를 받아오는 과정에서 메모리 소비는 주로 브라우저와 클라이언트 애플리케이션에서 발생한다. 사용자의 브라우저가 웹 페이지를 렌더링하고 JS 를 실행하는 동안, 클라이언트 애플리케이션의 상태와 데이터도 메모리를 차지하기 때문에 두 주체가 모두 메모리를 소비한다.

### 2-3. View
View 는 사용자의 요청을 처리하고 적절한 모델과 템플릿을 연결하여 응답을 생성한다. Thymeleaf 와 같은 템플릿 엔진을 사용하는 Spring 서버에서 @Controller 애너테이션이 붙을 수 있는 클래스와 비슷한 역할을 한다고 생각하면 되겠다. 예를 들면, URL 과 View 를 연결하는 역할 또한 수행한다.

View 는 주로 Python 함수와 클래스 형태로 정의된다. 사용자의 요청에 따라 필요한 데이터를 모델에서 가져오고, 이를 템플릿에 전달하여 최종 응답을 생성한다. @Service 애너테이션이 붙을 수 있는 비즈니스 로직이 포함된 코드 또한 포함된다고 생각해도 되겠다.

> 비즈니스 로직이란?

애플리케이션의 핵심 기능과 규칙을 정의하는 부분으로, 특정 도메인이나 비즈니스에 관련된 규칙과 요구 사항을 구현한 코드를 말한다. 데이터 처리를 포함하며, 사용자 입력을 검증하고, 데이터베이스와 상호작용하며, 결과적으로 애플리케이션의 목표를 달성하는 데에 필요한 모든 계산과 결정을 포함한다.

## 3. MTV 패턴의 흐름
- 사용자가 웹 브라우저에서 URL을 요청.
- Django의 URL 디스패처가 요청된 URL을 분석하여 View 를 Mapping.
- 뷰가 호출되어 필요한 데이터를 Model 에서 가져옴.
- 뷰는 가져온 데이터를 Template 에 전달.
- 템플릿은 데이터를 기반으로 HTML을 생성하여 사용자에게 응답.

## 4. MTV와 MVC의 차이
MTV 패턴은 MVC(Model-View-Controller) 패턴과 유사하지만, Django에서는 "뷰"가 "컨트롤러"의 역할을 하며, "템플릿"이 "뷰"의 역할을 하는 차이점이 있다. 즉, Django에서 뷰는 요청을 처리하고 템플릿을 렌더링하는 역할을 수행한다.
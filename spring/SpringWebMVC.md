# [Spring Web MVC] 동작 원리

## 구조

<br>

![WebApplicationServer](/image/web_application_server.png)

<br>

## Filter

> Web Application의 전역적인 로직 담당으로 Dispatcher Servlet으로 들어가기 전인 Web Application 단에서 실행한다.

## Dispatcher Servlet

> Servlet Container에서 Http 프로토콜을 통해 들어오는 모든 요청을<br>
> 프레젠테이션 계층의 제일 앞에 둬서 중앙 집중식으로 처리해주는 프론트 컨트롤러

- Spring MVC 패턴에서 기본적으로 사용하는 Servlet<br>
- 클라이언트의 요청이 있을 시 가장 앞단에서 요청을 가로채어 (Front Controller)<br>
- 요청에 매핑되는 Controller에 작업을 전달하고<br>
- 비즈니스 로직 처리 후 해당 결과 View를 클라이언트에 전달하는 역할을 담당한다.

## Handler Mapping

> 사용자가 요청한 URL을 분석하여 이것을 처리할 Handler를 찾아주는 인터페이스(Interface)

- Dispatcher Servlet 으로부터 검색을 요청받은 Controller를 찾아 Dispatcher Servlet으로 정보를 리턴해준다.
- Dispatcher Servlet에서는 Controller 정보를 받아 해당 Controller와 매핑시킨다.

## Handler Adapter

> Handler Mapping이 찾아낸 Handler를 호출하고 처리하는 인터페이스(Interface)

- Hander Mapping을 통해 찾은 컨트롤러를 직접 실행하는 기능을 수행한다.

## Handler Interceptor

> Dispatcher Servlet이 컨트롤러를 호출하기 전과 후에 요청, 응답을 가공할 수 있는 일종의 필터(Filter)

- Request가 Controller에 매핑되기전 앞단에서 부가적인 로직을 끼워넣는다.
- 주로 세션, 쿠키, 권한 인증 로직에 많이 사용된다.

## Controller

- Request와 매핑되는 곳
- Request에 대해 어떤 로직(Service)으로 처리할 것인지를 결정하고, 그에 맞는 Service를 호출
- Service Bean을 스프링 컨테이너로부터 주입받아야 한다. Service Bean의 메소드를 호출해야 하기 때문.

## Service

- 데이터 처리 및 가공을 위한 비즈니스 로직을 수행한다.
- Request에 대한 실질적인 로직을 수행하기 때문에, Spring MVC Request Lifecycle의 중심으로 볼 수 있다. Service가 없다면 서버 애플리케이션의 존재 이유도 없다.
- Repository를 통해 DB에 접근하여 데이터의 CRUD(Create, Read, Update, Delete)를 처리한다.

## Repository

- DB에 접근하는 객체이다. DAO(Data Access Object) 라고 부른다.
- Service에서 DB에 접근할 수 있게 하여 데이터의 CRUD를 가능하게 한다.

## View Resolver

> Handler에서 반환하는 View 이름에 해당하는 View를 찾아내는 인터페이스

- Controller에서 리턴한 View의 이름을 Dispatcher Servlet으로부터 넘겨받고, 해당 View를 렌더링한다.
- 렌더링한 View는 Dispatcher Servlet으로 리턴하고, Dispatcher Servlet에서는 해당 View 화면을 Response 한다.
- View 이름으로부터 사용될 View 객체를 매핑하는 역할

<br>

---

<br>

## 참고

[스프링 동작 원리 이해](https://ee-22-joo.tistory.com/20)<br>
[DispatcherServlet 동작원리](https://jckim-dev.tistory.com/12)<br>
[Spring MVC Life Cycle](https://velog.io/@damiano1027/Spring-Spring-MVC-Request-Lifecycle)

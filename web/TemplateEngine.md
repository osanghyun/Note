# Template Engine

템플릿 양식과 특정 데이터 모델에 따른 입력 자료를 합성하여 결과 문서를 출력하는 소프트웨어를 말한다.

- 그 중 웹 템플릿 엔진이란 웹 문서가 출력되는 템플릿 엔진을 말한다.
  - 즉, 웹 템플릿 엔진은 웹 템플릿들과 웹 컨텐츠 정보를 처리하기 위해 설계된 소프트웨어이다.
  - 웹 템플릿 엔진은 view code(HTML)와 data logic code(DB Connection)를 분리해주는 기능을 한다.

## Template Engine 의 종류

- Thymeleaf
- Django
- JSP
- PHP
- ...

## Layout Template Engine VS Text Template Engine

- `Layout` Template Engine
  - 중복되는 include 코드를 사용하지 않고도 지정된 페이지 레이아웃에 따라 페이지 타일을 조합하여 완전한 페이지로 만들어준다.
  - Apache Tiles, Sitemesh 등
- `Text` Template Engine
  - 템플릿 양식에 적절한 특정 데이터를 넣어 결과 문서를 출력한다.
  - Freemarker, Thymeleaf, JSP 등
- 둘은 역할이 다르며 섞어서 사용하는 것이지 서로 배타적인 것이 아니다.

## Server Side Template Engine VS Client Side Template Engine

- `Server` Side Template Engine

  - 서버에서 DB 혹은 API에서 가져온 데이터를 미리 정의된 Template에 넣어 html을 그려서 클라이언트에 전달해주는 역할을 한다.
  - 즉, HTML 코드에서 고정적으로 사용되는 부분은 템플릿으로 만들어두고 동적으로 생성되는 부분만 템플릿 특정 장소에 끼워넣는 방식으로 동작할 수 있도록 해준다.
  - 과정<br>
    1. 클라이언트에게 요청을 받음
    2. 필요한 데이터를 DB or API 에서 가져온다
    3. 미리 정의된 Template에 해당 데이터를 적절하게 넣는다.
    4. 서버에서 HTML을 생성한다.
    5. 해당 HTML을 클라이언트에게 전달한다.
  - Thymeleaf, JSP 등

- `Client` Side Template Engine
  - html 형태로 코드를 작성할 수 있으며, 동적으로 DOM을 그리게 해주는 역할을 한다.
  - 즉, 데이터를 받아서 DOM 객체에 동적으로 그려주는 프로세스를 담당한다.
  - 예를 들어 웹 페이지에서 여러 카테고리 중 탭을 선택할 때마다 같은 형식의 프레임에 내용만 바뀌어 변경되는 것을 볼 수 있다. 이런 공통적인 프레임을 미리 제작한 template이라고 부른다. 클라이언트에서는 이런 template을 매번 입력하거나 바꿀 수 없으므로 script 타입을 template으로 미리 만들어 사용한다.
  - 과정<br>
    1. 클라이언트에서 공통적인 프레임을 미리 template으로 만든다.
    2. 서버에서 필요한 데이터를 받는다.
    3. 데이터를 template을 적절한 위치에 replace하고 DOM 객체에 동적으로 그려준다.
  - 클라이언트 사이드 템플릿 엔진의 필요성
    - Javascript 라이브러리로 랜더링이 끝난뒤 (HTML DOM이 다 그려진 뒤)에 서버 통신 없이 화면 변경이 필요할 경우
    - 계속해서 페이지를 이동하여 서버 쪽으로 호출이 발생한다면 서버 사이드 템플릿 엔진을 이용하면 되는데, 단일 화면에서 특정 이벤트에 따라 화면이 계속 변경되어야 하는 경우는 javascript로 html을 렌더링하는 경우가 많다.
    - 단일 화면에서의 화면 병경에서는 서버 쪽을 사용하지 않고 화면을 그리기위해 javscript 내부에 html 코드를 작성해야 하는데, 이때 클라이언트 사이드 템플릿 엔진을 사용하지 않고 아래와 같이 javascript로 html을 렌더링하는 경우에는 여러 문제가 있다.
    - js
      1. html 코드의 오타를 찾기 어렵다.
      2. 렌더링 해야 할 코드가 늘어나면 늘어날수록 수정하기 어려워진다.

## Template Engine의 필요성

1. 많은 코드를 줄일 수 있다.
   - 대부분의 Template Engine은 기존의 HTML에 비해서 간단한 문법을 사용한다.
2. 재사용성이 높다.
   - 웹페이지 혹은 웹앱을 만들 때 똑같은 디자인의 페이지에 보이는 데이터만 변경되는 경우가 많다.
3. 유지보수에 용이하다.
   - 하나의 Template을 만들어 여러 페이지를 렌더링하는 작업에는 또 다른 이점이 있다.

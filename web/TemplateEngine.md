# Template Engine

## Template System

- 템플릿 프로세서를 사용하여 웹 템플릿과결합하여 완성된 웹 페이지를 만들어내는 시스템.
- Data를 결합하여 페이지를 만들어 내기도 하고 많은 양의 Content를 표현하는 것을 도와준다.

## Template System의 구성요소

- 템플릿 엔진 (Template Engine)
- 템플릿 자료 (Template Resource) : 템플릿 언어로 작성된 웹 템플릿
- Content Resource : XML, 다양한 종류의 데이터 스트림

## Template System의 종류

> Template와 결합되는 위치에 따라 종류를 나눌 수 있다.
> <br>

- Server Side : Web Server
- Client Side : Web Browser
- Edge-Side : Proxy Server
- 분산(Distributed) : Multiple Server
- 서버 밖(OutSider Server) : 정적 웹 페이지(Static Web Page)는 Offline에서 제작되고 웹 서버에 업로드 된다.

## Static Site Generators

- Static Web Page만을 생성한다.
- OutSider Server의 대표적인 예시이다.

## Server-side Systems

- Server-side dynamic pages가 미리 존재하는 템플릿에 맞게 생성된다.
- 대표적인 예시로 Thymeleaf, Django 등이 있다.

## Client-side Systems

- Browser에서 XSLT 스타일시트를 적용하여 XML의 데이터를 XHTML로 변경 가능하다.
- Javascript를 이용하여 템플릿을 구성하기도 한다.

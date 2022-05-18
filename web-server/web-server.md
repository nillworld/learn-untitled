# Web Server and WAS

## Web Server

- 어떠한 하드웨어로 하여금 서버 역할을 하도록 해주는 소프트웨어도 서버라고 부른다. ex) Apache server, NginX server
- 웹서버(Apache server, NginX server)는 보통 하드웨어를 웹서비스 할 수 있도록 해주는 소프트웨어를 일컫는다.
- 웹서버는 html, css, js, 이미지파일을 외부에서 접근 가능하도록 개방하여 이들을 받아갈 수 있도록 함.
- IIS는 윈도우에서 쓸 수 있는 웹서버
- 기본적으로는 정적인 페이지만 운영할 수 있지만, 모듈등을 이용해서 apache, php, MySQL(줄여서 APM)와 같이 서로 연결하여 동적인 웹을 만들 수 있음.
- Reverse proxy 기능 - 사용자로 부터 서버 내부의 구조를 감춤
- 로드밸런싱 역할
- (사용자가 서버로 부터 자주 찾는 데이터)서버단 캐싱 역할

## Web Application Server(WAS)

- 보통 자바 스프링에서 쓰이는 용어.
- 단순히 서버역할(서빙) 하는게 아닌, 프로그래밍적으로 어떠한 작업을 하는 것으로, 동적페이지를 전문적으로 처리함.
- 단순 php와 같은 소스가 아닌 스프링과 같은 고차원언어일 경우 WAS 이용.
- 자바 바이트 코드로 컴파일 되는 언어들에 쓰이는 WAS는 tomcat, Jetty, Undertow 등이 있다.
- 스프링으로 코딩한 웹앱 - war파일로 빌드(.class, html, js 등이 압축되어 있음) - 톰캣의 특정 폴더에 war 파일을 넣고 명령어 실행하면 스프링 서비스가 톰캣을 사용하여 동작.
- 요즘은 war파일로 빌드하는게 아닌 tomcat이 내장되어있는 jar파일로 빌드해서 배포.
- 자바의 스프링이 아닌 파이썬의 Django나 C#의 닷넷과 같이 다른 프레임워크에서 딱히 WAS 역할을 하는게 나누어져 있지 않다.
- DJANGO에 있는 runserver는 개발용 서버일 뿐 보안이슈에 대해 체크하지 않아서 배포용으로 사용하지 않고 , gunicorn이나 uwsgi와 같은 Gateway Interface(WSGI)를 통해서 다른 웹서버 프로그램과 통신하여 배포 함. (Client - Webserver(nginx) - WSGI(gunicorn) - Application Server(django))
- Node.js는 application이 WAS 역할을 하는 것처럼 보이게 처리된다.
- 톰캣이 아파치와 같은 web server 역할을 할 수 있지만, Reverse proxy역할을 못함.

## Apache와 NginX의 차이

- apache는 다중프로세스, NginX는 이벤트로 작업 처리.
- apache는 멀티 프로세스 모듈(MPM) 방식으로, 사용자가 올 때마다 프로세스를 새로 생성 하거나 한 프로세스 안에서 스레드를 새로 생성.
- apache는 오랫동안 써 왔기에 다양한 검증된 기능 성능을 위해 apache도 이벤트 방식 추가.
- NginX의 event driven 방식은 순서대로 이벤트 처리(성능이 좋고 가벼움).

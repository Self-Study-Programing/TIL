# viewport

브라우저 에서 Viewport 는 화면 크기를 이야기하며, 메뉴바, 탭영역 등을 제외한 순수 화면 영역이다.
Viewport 의 영역은 디바이스 크기와, 각각의 브라우저 마다 계산되는 영역이 달라 같은 웹페이지라도 환경에 따라, 매우 다양해진다.

Viewport 는 화면이 크기이기 때문에, viewport 보다 웹 문서가 클 경우 스크롤이 생성되며, 이를 가지고 viewport 를 이동시킬 수 있다.

## 브라우저 Viewport 구하기

브라우저의 Viewport 를 구하기 위해서 아래 값들로 확인할 수 있다.

- document.documentElement.clientWidth / clientHeight 문서의 viewport 크기
- window.innerWidth / innerHeight 브라우저 viewport 의 스크롤 포함 크기
- window.outerWidth / outerHeight 브라우저 창 크기

뷰포트 뿐만 아니라 screen이라는 객체도 있다

## screen

screen 객체는 viewport 와 관계없이 화면의 전체 크기와 픽셀값들을 가지고 있다.

- screen.width
- screen.height

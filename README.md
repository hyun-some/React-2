# React-2
react2

202030328 정현철

9/11
2.1 서버 사이드 렌더링(SSR)
- 생소할 수도 있지만 웹 페이지를 제공하는 가장 흔한 방법입니다.

- APM 을 이용하는 일반적인 웹 페이지 생성이라고 보면 도비니다.

- 여기에 자바스크립트 코드가 적재되면 동적으로 페이지 내용을 렌더링 합니다.


- Next.js도 이와 같이 동적으로 페이지를 렌더링할 수 있습니다.

- 그리고 여기에 스크립트 코드를 집어 넣어서 나중에 웹 페이지를 동적으로 처리할 수도 있는데 이를 하이드레이션이라고 합니다.

- 예를 들면 어떤 사람이 작성한 블로그 글을 한 페이지에 모아서 작성해야한다면 ssr을 이용하는 것이 적당합니다.

- 서버 사이드 렌더링 -> 자바스크립트가 하이드레이션된 페이지를 전송 -> 클라이언트에서 DOM 위에 각 스크립트 코드를 하이드레이션 : 페이지 새로 고침 없이 사용자와 웹 페이지간 상호 작용을 가능하게 합니다.


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

- 리액트 하이드레이션 덕분에 이 상태에서 웹 앱은 싱글 페이지 애플리케이션 (spa) 처럼 작동할 수 있습니다.

- csr과 ssr의 장점을 모두 가지는 것입니다.

- 특정 렌더링 전략만 사용한다고 가정하면 ssr이 csr에 비해 여러 가지 장점이 있습니다.

[ssr의 장점]

- 더 안전한 웹 애플리케이션 : 쿠키 관리, 주요 api, 데이터 검증 등과 같은 작업을 서버에서 처리하기 때문에 중요한 데이터를 클라이언트에 노출할 필요가 없기 때문입니다.

- 더 뛰어난 웹 사이트 호환성 : 클라이언트 환경이 자바스크립트를 사용하지 못하거나 오래된 브라우저를 사용하더라도 서비스를 제공할 수 있습니다.

- 더 뛰어난 seo: 서버가 렌더링한 html 을 받기 때문에 봇이나 웹 크롤러가 페이지를 렌더링 할 필요가 없기 때문입니다.

SSR이 최적의 렌더링 전략이 아닌 경우

- 클라이언트가 페이지를 요청할 때마다 페이지를 다시 렌더링 할 수 있는 서버가 필요합니다.

- 다른 방식에 비해 SSR이 더 많은 자원을 소모하고, 더 많은 부하를 보이며 유지 보수 비용도 증가합니다.

- 페이지에 대한 요청을 처리하는 시간이 길어집니다.

- 페이지가 외부 API 또는 데이터 소스에 접근해야 한다면, 해당 페이지를 렌더링 할 때마다 이를 다시 요청해야합니다.

- 페이지 간의 이동은 CSR에 비해 느립니다.

- 중요한 것은 NEST.JS가 기본적으로 빌드 시점에 정적으로 페이지를 만든다는 것입니다.

- 페이지에서 외부 API를 호출하거나 데이터베이스에 접근하는 등 동적 작업을 해야 한다면 해당하는 함수르 페이지에 EXPXORT를 해야합니다.

코드 설명(36P)

- 이 페이지는 DIV 요소 안에 문자열만 표시합니다.

- 외부 API를 호출 하지 않으며 항상 같은 문자열만 표시 됩니다.

//function IndexPage() {
    return <div>This is the index page.</div>;
}

export default IndexPage;

- 다음 코드는 페이지를 요청할 때마다
사용자 환영 문구를 표시합니다.

- 특정 사용자 정보를 가져온 다음 클라이언트에 전달해서 사용할 수 있도록 하고 있습니다.

- 이 경우 미리 예약된 getServerSideProps()함수를 사용합니다.

export async function getServerSideProps() {
    const userRequst = await fetch('https://example.com/api/user');
    const userData = await userRequest.json();

    return {
        props: {
            user: userData,
        },
    };
}

function IndexPage(props) {
    return <div>Welcome, {props.user.name}!</div>;
}

export default IndexPage;

- 페이지에 대한 요청이 들어오면 서버가 REST API를 호출해서 필요한 사용자 정보를 가져옵니다.

- 이 과정은 다음과 같은 세부 단계로 나눌 수 있습니다.

1. getServerSideProps라는 비동기 함수를 exprot합니다. 빌드 과정에서 Next.js는 이 함수를 export하는 모든 페이지를 찾아서 서버가 페이지 요청을 처리할때 getServerSideProps 함수를 호출하도록 만듭니다.

2. getServerSideProps 함수는 props라는 속성값을 갖는 객체를 반환합니다. 이 props는 컴포넌트로 전달되 서버와 클라이언트 모두가 props 에 접근할 수 있게 됩니다. fetch API는 서버에서 실행되기 때문에 별도의 폴리필을 끼워 넣을 필요는 없습니다.

3. IndexPage 함수를 수정해서 props를 인자로 받습니다. 이 props는 getServerSideProps 함수에서 반환한 props의 모든 내용을 갖고 있습니다.

#Next.js14부터는 하나의 API만 사용합니다.

2.2 클라이언트 사이더 렌더링(CSR)

- React 앱을 실행하면 렌더링 시작전에 빈 화면이 한동안 유지되는 것이 보입니다.

- 이는 서버에서 스크립트와 스타일만 포함된 HTML을 전송하기 때문입니다.

- 실제 렌더링은 클라이언트에서 이루어 집니다.

- CSR로 생성한 앱의 HTML을 보면 div태그 하나 밖에 없습니다. 그래서 빈 화면만 보였던 겁니다.

- 빌드 과정에서 js와 css파일을 HTML페잊이에 불러오도록 만들고 root div에 렌더링 합니다.

// <body>
        <noscript>
        You need to enable JavaScript to run this app.
        </noscript>
        <div id="root"></div>
    </body>


    CSR을 사용할 때의 주요 이점

    - 네이티브 앱처럼 느껴지는 웹 앱

    - 전체 자바스크립트 번들을 다운로드 한다는 것은 렌더링 할 모든 페이지가 이미 브라우저에 다운로드 되어 있다는 뜻입니다.

    - 다른 페이지로 이동해도 서버에 요청할 필요 없이, 바로 페이지를 이동할 수 있습니다.

    - 페이지를 바꾸기 위해 새로 고칠 필요가 없습니다.

    - 쉬운 페이지 전환

    - 클라이언트에서의 내비게이션은 브라우저 화면을 새로 고칠 필요 없이 다른 페이지로의 이동을 가능하게 만듭니다.

    - 페이지 간 전환에 멋진 효과를 넣을 수도 있습니다. 애니메이션을 방해할 요소가 없기 때문입니다.

    - 지연된 로딩과 성능

    - 웹 앱은 최소로 필요한 HTML만 렌더링합니다.

    - 버튼을 누르면 나오는 모달도 실제 버튼이 눌렀을 때 동적으로 생성하게 됩니다.

    - 서버 부하 감소 - 서버리스 환경에서 웹 앱을 제공할 수도 있습니다.

    장점은 단점이 될수도 있다.

    - 네트워크 속도가 느린 환경에서는 번들이 모두 다운로드 될때까지 계속 빈 페이지를 보아야 합니다.

    - 검색 로봇에게도 그 내용은 빈 것으로 보입니다.

    - 번들을 모두 받을 때까지 검색 로봇이 기다리기는 하지만 성능 점수는 낮을 것입니다.

    - React useEffect Hook

    - 최근 리액트는 하뭇형 컴포넌트 사용을 강조하면서 life cycle함수 대신 Hook 을 사용합니다.

    - 함수형 컴포넌트 내에서 DOM 조작이나 데이터 불러오기 같은 사이드 이펙트 기능을 구현할 때, useEffect 함수를 사용해서 컴포넌트가 마운트된 후 해당 기능을 실행하도록 만들 수 있습니다.

코드 설명(40~41p)

CSR인 React에서는 다음 코드가 문제없이 작동하지만 Next.js의 빌드 과정에서는 문제가 생깁니다.

- Highlight.js 라이브러리가 document라는 전역 변수를 사용하는데, 이 변수는 Node.js에서 제공하지 않으며 오직 브라우저에서만 접근할 수 있긴 때문입니다.

- 이 문제는 hljs 호출을 useEffect 훅으로 감싸서 해결할 수 있습니다.

import Head from 'next/head';
import hljs from 'highlight.js';
import javascript from 'highlight.js/lib/languages/javascript';

function Highlight({ code }) {
    hljs.registerLanguage('javascript', javascript);
    hljs.initHlightLighting();

    return (
        <>
        <Head>
        <link rel = 'stylesheet' href='/highlight.css' />
        </Head>
        <pre>
            <code className='js'> {code}</code>
            </pre>
            </>
    );
}

export default Highlight;
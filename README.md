# React-2
react2

### 202030328 정현철


### 10/30
4.2 데이터 불러오기
Next는 클라이언트와 서버 모두에서 데이터를 불러올 수 있습니다.
서버는 다음 두 가지 상황에서 데이터를 불러올 수 있습니다.
1) 정적 페이지를 만들 때 getStaticProps함수를 사용해서, 빌드 시점에 데이터를 불러올 수 있습니다.
2) 서버가 페이지를 레넏링할 때 getServerSideProps를 통해, 실행 도중 데이터를 불러올 수도 있습니다.

데이터 베이스에서 데이터를 가져올 수도 있지만 안전하지 않기 때문에 권장하지 않습니다. 데이터베이스의 접근은 백엔드에서 처리하는것이 좋습니다.
Next는 프런트엔드만 담당하는것이 좋습니다.

서버가 데이터 불러오기
- 서버에서는 두 가지 방법으로 HTTP 요청을 만들고 처리할 수 있습니다.
  1)Node의 내장 HTTP라이브러리를 사용할 수 있ㅅ브니다.
  다만 서드파티 HTTP클라이언트와 비교했을 때 설정하고 처리해야 할 작업이 더 많은 편입니다.
  2)HTTP 클라이언트 라이브러리를 사용할 수 있습니다. 가장 유명한 것이 Axios입니다.

- Axios를 사용하는 이유는
  1) 클라이언트와 서버 모두에서 동일하게 사용할 수 있고,
  2) npm을 통한 다운로드가 일주일에 약 1,700만 회에 달할 정도로 많이 사용되기 때문입니다.
 
  서버에서 REST API 사용하기
  - REST APIㄹ르 호출할 땐느 public API를 호출할 것인지, private API를 호출할 것인지를 먼저 확인해야 합니다.
  - Public API는 어떤 인증이나 권한도 필요 없으며 누구나 호출할 수 있습니다.
  - Private API는 호출 전 반드시 인증과 권한 검사 과정을 거쳐야 합니다...

GraphQL API
- 2012년에 메타에서 개발했습니다.
- 새로운 관점으로 api 데이터를 불러옵니다.


1. REST API - 개요
   - REST(Representational State Transfer)란 자원을 이름으로 구분하여 그 자원의 상태를 통신을 통해 주고 받는 것을 의미합니다.
     1. HTTP URL(Uniform Resource Identifier: 통일된 자원 식별자)를 이용해서 자원(Resource)을 명시합니다.
     2. HTTP Method(POST, GET, PUT, DELETE, PATCH 등)를 통해 자원에 CRUD를 적용합니다.
    
   - CRUD란 데이터 처리의 기본적인 기능을 나타냅니다.
     1. Create: 데이터 생성(POST)
     2. Read: 데이터 조화(GET)
     3. Update: 데이터 수정(PUT, PATCH)
     4. Delete: 데이터 삭제(DELETE)


     -REST API란 REST의 규칙을 적용한 API를 의미합니다.

1. REST API - 기본 설계 규칙
   - URL는 동사보다는 명사를, 대문자보다는 소문자를 사용하여야 합니다.
   - 주소의 마지막에 슬러시/를 포함하지 않습니다.
   - 단어를 연결할 땐느 하이픈을 사용합니다.
   - 파일확장자는 URI에 포함하지 않습니다.
   - URI에 메소드를 포함하지 않습니다.
     
  Json Server
   - Backend가 개발되기 전이나, 아직 외부 API가 결정되지 않았다면 local에 Json server를 구축하고 Frontend 개발을 하기에 적합한 node 패키지입니다.
   - 다음 명령으로 json-server를 설치해 줍니다.
   - $npm i -g json-server
     
   - 설치가 잘되었는지 version 을 확인해 봅니다.
     - $json-server --version
### 10/23
1. Static Resource
   - 정적 자원 중 이미지 파일은 SEO에 많은 영향을 미칩니다.
   - 다운로드 시간이 많이 걸리고, 렌더링 후에 레이아웃이 변경되는 등 UX에 영향을 미칩니다.
   - 이것을 누적 레이아웃 이동(CLS: Cumulative Layout Shift)이라고 합니다.
   - Image 컴포넌트를 사용하면 CLS문제를 해결합니다.
   - lazy loading: 이미지 로드 시점을 필요할때까지 지연시키는 기술입니다.
   - 이미지 사이즈 최적화로 사이즈를 1/10 이하로 줄여 줍니다
   - Placeholder를 제공합니다
1. Image component - local
   - WebP와 같은 최신 이미지 포맷 및 최신 포맷을 지원하지 않는 브라우저를 위해 PNG나 JPGE와 같은 예전 이미지 포맷도 제공합니다.
   - Pixabay나 Unsplash 와 같은 외부 이미지 서비스로 이미지를 제공할 수 있습니다.
   - Image 컴포넌트를 사용하면 다양한 props를 전달할 수 있습니다.
     [주요 props]
     src=""
     width= {500}
     height= {500}
     alt=""
     Placeholder = "blue"
     //외부 이미지는 blurDataURL=''로 처리
     loading="lazy"

   - 정적 자원은 기본적으로 public 디렉토리에 저장합니다.
   - 정적 자원은 번들링 이후에도 변하지 않기 때문입니다.
   - 여러 종류의 정적 자원을 사용할 경우 public의 root에 각각 디렉토리를 만들어 사용합니다.
   - Image도 마찬가지로 /public/images 디렉토리를 만들고 사용합니다.
   - 이미지를 불러오는 방법은 직접 불러오는 방법과 import하는 방법 2가지가 있습니다.
   - 이미지의 경로/images/[이미지 이름.확장자]로 합니다. 이 때 public은 생략합니다


1. Image component - Remote
 - Pixabay와 같은 외부 이미지를 사용하려면 next.config.mjs에 URL을 추가해 줘야합니다.
 - 만일 파일이 없다면 Project root에 추가해 주면 됩니다.
 - 파일의 초기 상태는 다음과 같습니다.
 - nextConfig에 images를 추가합니다.
 - 간단하게 domains만 등록해 줘도 되지만, 공식 사이트의 추천은 두번째 코드와 같습니다.

- 이미지를 출력하는 코드입니다.
- 서비스에 따라서 도메인은 차이가 날 수 있습니다.
- Pixabay의 경우 원하는 이미지를 우클릭하고, '이미지 주소 복사'로 주소를 복사합니다.
- 나머지는 local image 사용법과 같습니다.
- 이미지가 정상저긍로 출력되면 다운로드 받아 이미지의 상태를 확인합니다.
- 이 방법은 외부 서비스가 아니라 자체 이미지 서버를 갖고 있을 때도 유용합니다.

04. 코드 구성과 데이터 불러오기
   - 4장에서는 애플리케이션의 디렉터리 구조를 어떻게 구성하는지 알아봅니다.
   - 클라이언트와 서버에서 외부 REST-API 및 GraphQL API를 사용한느 방법도 알아봅니다.
   - 프로젝트를 시작할 때 애플리케이션의 확장과 복잡도 증가에 대비해야 합니다.
   - 4-1절에서는 애플리케이션 상태를 빠르고 간결하게 관리할 수 있는 코드 구성 방법을 알아봅니다.
   - 알아볼 내용은 다음과 같습니다.
      - 아토믹 디자인 원칙(Atomic Design Principles/Atomic Design Pattern)에 따른 컴포넌트 구성
      - 유틸리티 구성
      - 정적 자원 구성
      - 스타일 파일 구성
      - lib 파일 구성
      - 서버에서 REST API를 사용하는 방법
      - 클라이어늩에서 REST API 를 사용하는 방법
      - 클라이언트 및 서버에서 Apollo를 이용하여 GraphQL API를 사용하는 방법
    
4.1 디렉토리 구조 구성
- NeXT.js에서는 특정 파일과 디렉토리가 지정된 위치에 있어야 합니다.
  _app.js나 _documnt.js파일.pages/와 public/

- Node_modules/: Next.js프로젝트의 의존성 패키지를 설치하는 디렉토리
- pages/: 애플리케이션의 페이지 파일을 저장하고 라우팅 시스템 관리
- public/: 컴파일된 CSS 및 자바스크립트 파일, 이미지, 아이콘 등의 정적 자원 관리
- styles/: 스타일링 포맷(CSS, SASS, LESS 등) 과 관계없이 스타일링 모듈 관리

- pages/ 디렉토리를 src/디렉토리 안으로 옮길 수 있습니다.
- public/과 node_modules/를 제외한 다른 디렉토리는 모두 src/로 옮길 수 있습니다.
  next-js-app
  - node_modules/
  - package.json
  - pages/
  - public/
  - styles/
 
  컴포넌트 구성
  - 컴포넌트는 세가지로 분류하고 각 컴포넌트와 관련된 스타일 및 테스트 파일을 같은 곳에 두어야합니다.
  - 코드를 더 효율적으로 구성하기 위해 아토믹 디자인 원칙에 따라 디렉토리를 구성합니다.
  - atoms: 가장 기본적인 컴포넌트 관리.예)button,input,p와 같은 표준 HTML요소를 감싸는 용도로 사용되는 컴포넌트
  - molecules : atom에 속한 컴포넌트 여러 개를 조합하여 복잡한 구조로 만든 컴포넌트 관리 . 예)input과 label을 합쳐서 만든 새로운 컴포넌트.
  - organisms: molecules와 atoms를 섞어서 더 복잡하게 만든 컴포넌트 관리 예)footer나 carousel컴포넌트
  - templates:위의 모든 컴포넌트를 어떻게 배치할지 결정해서 사용자가 접근할 수 있는 페이지
 
  - Button 컴포넌트를 예를 들면 다음과 같이 최소한 세 개의 파일을 만들어야 합니다.
  - 컴포넌트 파일, 스타일 파일, 테스트 파일입니다.
  - 이렇게 컴포넌트를 구성하면 필요할 때 컴포넌트를 찾고 수정하기 쉽습니다.
 
  정적 자원의 구성
  - 정적 자원은 public/디렉토리에서 관리합니다.
  - 일반적인 웹 애플리케이션에서는 다음과 같은 정적 자원을 사용합니다.
       - 이미지
       - 컴파일한 자바스크립트 파일
       - 컴파일한 CSS 파일
       - 아이콘(favicon 및 웹 앱 아이콘)
       - manifest.json.robot.txt 등의 정적 파일
  - 먼저 public/assets/디렉토리를 만들고 파일 유형별로 다시 디렉토리를 추가합니다.
  - 그리고 이곳에 저장도니 파일에 접근하고자 하면 예와 같이 public을 제외한 주소를 써주면 됩니다.
 
  -  icons/디렉토리는 주로 웹 앱 매니페스트에 제공할 아이콘을 관리합니다.
  -  manifest.json파일은 public/디렉토리 root에 만들어서 사용합니다.
  -  HTML 메타 태그를 사용해서 manifest 파일을 불러옵니다.
  -  다음은 manifest.json의 예시입니다.
 
  스타일 파일 구성
  - 스타일 파일은 앱에서 어떤 스타일 관련 기술을 사용하는가에 따라 구성 달라집니다.
  - Emotion,styled-components,JSS와 같은 CSS-in-JS 프레임워크의 경우 컴포넌트별로 스타일 파일을 만듭니다.
  - 이렇게 하면 스타일 변경도 쉽습니다.
  - 만일 컬러 팔레트, 테마, 미디어 쿼리와 같은 공통 스타일의 경우는 styles/ 디렉토리를 사용합니다.

   lib 파일 수성
  - lib 파일은 서드파티 라이브러리를 감싸는 스크립트를 말합니다.
  - lib 파일은 특정 라이브러리에 특화된 것입니다. 예)GraphQL
  - 만일 GraphQL을 사용한다면, 클라이언트를 초기화하고, 질의문과 뮤테이션을 저장하는 등의 작업이 필요합니다.
  - 먼저 이런 스크립트를 좀 더 모듈화하기 위해 프로젝트 root에 lib/graphql/디렉토리를 만듭니다.
  - 그리고 다음과 같이 구성하여 관리합니다.
 
    4.2 데이터 불러오기
  - Next는 클라이언트와 서버 모두에서 데이터를 불러올 수 있습니다.
  - 서버는 다음 두가지 상황아ㅔ서 데이터를 불러올 수 있습니다.
    1) 정적 페이지를 만들 때 getStaticProps함수를 사용해서, 빌드 시점에 데이터를 불러올 수 있습니다.
    2) 서버가 페이지를 렌더링할 때 getServerSideProps를 통해, 실행 도중 데이터를 불러올 수도 있습니다.
   
   - 데이터 베이스에서 데이터를 가져올 수도 있지만 안전하지 않기 때문에 권장하지 않습니다. 데이터베이스의 접근은 백엔드에서 처리하는것이 좋습니다.
   - Next는 프런트엔드만 담당하는 것이 좋습니다.
  

### 10/11
1. Page Project Laout - app
    - _app.jsx는 서버에 요청할 때 가장 먼저 실행되는 컴포넌트입니다.
    - 페이지에 적용할 공통 레이아웃을 선언하는 곳입니다.
    - 기본 코드는 다음과 같습니다.
      import "@/styles/globals.css";

      export default function App({ Component, pageProps}) {
      return <Componenet {...pageProps} />;
      }
    - Global CSS는 이곳에 추가됩니다.
    - props 중 Component는 서버에 요청한 페이지입니다.
    - pageProps는 App.genInitialProps를 이용하여 prefetching 된 데이터를 반환합니다.
    - 데이터가 없다면 빈 객체({})를 반환합니다.
    - 단, getStaticProps, getServerSideProps와 같은 Data Fetching methods는 동작하지 않습니다.
  
1. Page Project Layout - _document
    - _document.jsx는 _app.jsx 다음에 실행됩니다.
    - 각 페이지에서 공통적으로 사용될 html, head, body 안에 들어갈 내용을 선언합니다.
    - onClick 같은 이벤트나 CSS는  이 곳에 선언하지 않습니다.
    - 만일 로직이나 스타일이 필요하다면 _app.jsx에 선언해야 합니다.
    - 기본 코드는 다음과 같습니다.

  import {HTML, Head, Main, NextScript } from 'next/document'

  export default function Document() {
  return (
  <Html lang="ko">
  <Head>
      {/*사용자 정의 메타 태그 */}
      <meta name="description" content = "커스텀 설명입니다."/>
      {/*외부 스크립트 추가 */}
      <script src="..."></script>
  
  </Head>
  <body>
      <Main/>
          <NextScript/>
  </body>
          </Html>
          )
          }

2. App Project Layout - layout.jsx
 - layout.jsx는 app 디렉토리 아래에 위치합니다.
 - layout.jsx는 Page Project에서 사용하던 _app.jsx와 _document.jsx를 대체합니다.
 - 이 파일은 삭제해도 프로젝트를 실행하면 자동으로 다시 생겨납니다.
 - 프로젝트를 생성할 때 생성된 기본 코드는 다음과 같습니다.

   export const metadat = {
   title: 'Next.js',
   description: 'Gnerated by Next.js',
   }

   export default function RootLayout({ children }) {
   return (
   <html lang="en">
   <body>{children}</body>
   </html>
   )
   }

   2. App Project Layout - meta data
   - metadata에서 모든 페이지에 적용할 meta data를 선언할 수 있습니다.
   - title의 경우에는 각 페이지에 맞게 작성한느 것이 SEO에 좋습니다.
   - 이럴 때는 각각의 page.jsx에 다음 코드를 추가해 주면 됩니다.
   - 추가하지 않은 페이지는 layout.jsx에서 정의한 title이 적용됩니다.
  
     export const metadata = {
     title: 'Hello, Next.js!',
     }

     - 만일 공통되는 title과 함께 각 페이지의 title을 추가하고 싶은 경우에는 layout.jsx의 title을 다음과 같이 추가해 줍니다.
       export const metadata = {
       title: {
       default : 'Next.js',
       template: '%s |Next.js',
       },
       description: 'Generated by Next.js',
       }

    2. App Project Layout - RootLayout
   - Children prop은 각각의 page.jsx를 받아 옵니다.
   - html 태그에 옵션을 추가하거나 수정할 수 있습니다. lang="ko"
   - 공통 레이아웃은 body 태그에 추가해 주면 됩니다.
   - 이때 children prop을 삭제하지 않도록 주의합니다.
  
   - Body에 header와 footer를 추가한 코드입니다.
  
   - 만일 특정 페이지나, 페이지 그룹에 레이아웃을 추가하고 싶다면 해당 디렉토리에 layout.jsx파일을 만들어 주면 됩니다.
   - 다음은 추가한 코드와 출력 화면의 예입니다.
  
     export default function Help

    - Link component를 이요해서 Navibar component를 만들어봅니다.
    - /components/Navibar.jsx 파일을 만든 다음 코드를 추가 합니다.
    - RootLayout에 Navibar component를 추가 합니다.

     3. Link vs. a vs. router.push
     - Link component를 이용해서 Navibar componenet를 만들어봅니다.
     - <a> tag는 html 동기식으로 전체가 reload되기 때문에, 외부 링크를 할 때 사용합니다.
     - 일반적으로 내부 링크 이동시에는 사용하지 않는 것이 좋습니다.
    
     - router.push 는 빌드 후, 이동할 주소가 html 상에 노출되지 않기 때문에 SEO에 취약합니다.
    
     - Link 컴포넌트는 빌드 후, a tag 로 자동 변환됩니다.
     - a tag의 장점인 SEO 최적화, prefetch 가능, 우 클릭 기능 등을 갖습니다.
     - 내부 페이지로의 이동할 때 이 방식을 사용해야 SPA 방식으로 전체 html 중 필요한 부분만 비동기식으로 리렌더링 된다.
     - 따라서 특별한 경우가 아니면 Link 컴포넌트 사용을 권장합니다.

    1. Image component - local
   - 정적 자원 중 이미지 파일은 SEO에 많은 영향을 미칩니다.
   - 다운로드 시간이 많이 걸리고, 렌더링 후에 레이아웃이 변경되는 등 UX에 영향을 미칩니다.
   - 이것을 누적 레이아웃 이동(CLS: Cumulative Layout Shift)이라고 합니다.
   - Image 컴포넌트를 사용하면 CLS 문제를 해결합니다.
   - lazy loading: 이미지 로드 시점을 필요할 때까지 지연시키는 기술입니다.
   - 이미지 사이즈 최적화로 사이즈를 1/10이하로 줄여 줍니다.
   - Placeholder를 제공합니다.
  
     1. Image component - local
     - WebP와 같은 최신 이미지 포맷 및 최신 포맷을 지원하지 않는 브라우저를 위해 Png나 Jpge와 같은 예전 이밎 포맷도 제공합니다.
     - Pixabay 나 Unplash와 같은 외부 이미지 서비스로 이미지를 제공할 수 있습니다.
      

1. Image component - local
- Image 컴포넌트를 사용하면 다양한 props를 전달 할 수 있습니다.
- 주요 props
- src =""
- width={500}
- height={500}
- alt=""
- Placeholder = "blue"
//외부 이미지는 blurDataURL=''로 처리
- loading = "lazy"
- Props 참고

1. Image component - local
- 정적 자원은 기본적으로 public 디렉토리에 저장합니다.
- 정적 자원은 번들링 이후에도 변하지 않기 때문입니다.
- 여러종류의 정적 자원을 사용할 경우 public의 root에 각각 디렉토리를 만들어 사용합니다.
- 이미지를 불러오는 방법은 직접 불러오는 방법가 import 하는 방법 2가지가 있습니다.
- 직접 불러올 때 경로는 /images/[이미지 이름.확장자]로 하면됩니다.

- import 하는 방법은 다음 소스처럼 이미지를 import 한 후에 이름만 사용하면 됩니다.
- import 경로에는 /public 을 반드시 넣어줘야 합니다.
- 같은 이미지를 같은 페이지에서 여러 번 사용할 때 편합니다.


### 9/25
<div>

페이지에서 경로 매개변수 사용하기(page53)
- 경로 매개변수를 사용해서 동적 페이지를 쉽게 만들 수 있습니다.

- page/greet/[name].js 파일을 만들어 보겠습니다.

- 내장 getServerSideProps 함수를 통해 URL에서 동적으로 [name] 변수 값을 가져오는 것입니다.

- greet/Mitch 주소로 가면'Hello, Mitch!'라는 문구가 렌더링 됩니다.

3. Next.js 기초와 내장 컴포넌트

- Next는 서버사이드 렌더링 외에도 많은 내장 컴포넌트와 함수를 제공합니다.
[3장학습내용]
- 클라이언트와 서버에서의 라우팅 시스템 작동 방식

- 페이지 간 이동 최적화

- Next.js가 정적 자원을 제공하는 방법

- 자동 이미지 최적화와 새로운 Image 컴포넌트를 사용한 이미지 제공 최적화 기법

- 컴포너트에서 HTML메타데이터를 처리하는 방법

- _app.js와 document.js파일 내용 및 커스터마이징 방법

3-1. 라우팅 시스템

- React의 React Router, Reach Router 등은 클라이언트 라우팅만 구현할 수 있습니다.

- Next는 파일시스템 기반 페이지와 라우팅을 합니다.

- 페이지는 /pages 디렉토리 안의 *.js, *.jsx, *.ts, *.tsx 파일에서 export한 React 컴포넌트입니다.

- 만일 블로그와 같이 컨텐츠를 분리해야 한다면 어떻게 해야 할까요?

- /pages 아래 디렉토리를 만들고 라우팅 규칙을 만들면 됩니다.

- /pages 디렉토리 내부에는 계층적 구조로 라우팅 규칙을 만들고 있습니다.

- /pages/posts 안에 index.js와 [slug].js 를 만ㄷ르어 jsx를 반환합니다.

- /pages/posts/ 디렉토리 내에 index.js만 간단하게 만들면 localhost:3000/posts로 접속이 가능합니다.

- 다만 동적인 라우팅 규칙을 만들려면 [slug].js 파일이 필요합니다.

- [slug].js 는 매개 변수로 사용되며 주소창에서 입력하는 값을 모두 받을 수 있습니다.

- 동적 라우팅 규칙을 중첩할 수도 있습니다.

- 접근 경로를 ~/posts/[date]/[slug]와 같이 만들 수 있습니다.
- [date] 디렉토리를 만들고 그 안에 [slug].js 파일을 저장하면 됩니다.
- [date] 나 [slug]는 어떤 값이든 가질 수 있습니다.

- 실제 앱에서는 경로 매개변수에 따라 서로 다른 동적 페이지를 렌더링하게 됩니다.


### 9/11
<div>

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

- 다음과 같이 React.useEffect와 React.useState를 함께 써서 특정 컴포넌트를 정확히 클라이언트에서만 렌더링하도록 지정할 수 있습니다.

import {useEffect, useState} from 'react';
import Highlight from '../components/Highlight';

function UseEffectPage() {
    const [isClient, setIsClient] = useState(false);

    useEffect(() => {
        setIsClient(true);
    }, []);

    return (
        <div>
        {isClient &&
        (<Highlight
        code={"console.log('Hello, world!')"}
        language='js'
        />)
        }
        </div>
    );
}

export default UseEffectPage;

process.browser 변수

- 서버에서 렌더링할 때 브라우저 전용 API로 인한 문제를 다른 방법으로 해결할 수도 있습니다.

- PROCESS BROWSER 값에 따라서 스크립트와 컴포넌트로 조건별로 실행하는 것입니다.

- 이 변수는 Boolean 값으로, 코드를 클라이언트에서 실행하면 true, 서버에서 실행하면 false 값을 갖습니다.

- 다음 코들르 실행하면 처음에는 "~server-side"로 표시되고, 리액트 하이드레이션이 끝나면 바로 "~client-side"라는 문자열로 바뀝니다.

하지만 process.browser에 대한 지원은 곧 중단될 예정입니다.

function IndexPage() {
    const side = process.browser ? 'client' : 'server';

    return <div>You're currently on the {side}-side.</div>;
}

export default IndexPage;


대신 좀 더 정확한 의미를 갖는 typeof window를 사용할 수 있습니다.

- typeof window를 서버에서 실행하면 그 값은 문자열 "undefined"가 되며, 그렇지 않으면 클라이언트에서 실행하게 됩니다.

function IndexPage() {
    const side = typeof window === "usdefined" ? 'server' : 'client';

    return <div> You're currently on toeh {side}-side.</div>;
}

export default IndexPage;

동적 컴포넌트 로딩 - dynamic

- 앞서 React.useEffect 훅을 사용하여 브라우저에서 코드를 실행하는 경우에만 컴포넌트를 렌더링 해 보았습니다.

- dynamic 함수로도 똑같이 동작하게 할 수 있습니다.

- 다음 코드를 실행하면 Highlight 컴포넌트를 동적 임포트 (dynamic import)로 불러옵니다.

- 즉, ssr:flase 옵션으로 클라이언트에서만 코드를 실행한다고 명시하는 것입니다.

<!-- import dynamic from 'next/dynamic';

const Highlight = dynamic(
    () => import('../componenets/Highlight'),
    { ssr: false}

);

import styles from '../styles/Home.module.css';

function DynamicPage() {
    return (
        <div className={styles.main}>
        <Highlight code={`console.log('Hello, world! ')`}language="js" />
        </div>
    );
}

export default DynamicPage; -->

2.3 정적 사이트 생성(SSG: Static Site Generation)
- SSG는 일부 똔느 전체 페이지를 빌드 시점에 미리 렌더링 합니다.

- SSG는 SSR 및 CSR과 비교했을 때 다음과 같은 장점이 있습니다.

1. 쉬운 확장

 정적 페이지는 단순 HTML로파일이므로 CDN을 통해 파일을 제공하거나, 캐시에 저장하기 쉽습니다.

 2. 뛰어난 성능
 빌드 시점에 HTML페이지를 미리 렌더링하기 때문에 페이지를 요청해도 클라이언트나 서버가 무언가를 처리할 필요가 없습니다.

 3. 더 안전한 API요청

 외부 API를 호출하거나, 데이터베이스에 접근하거나, 보호해야 할 데이터에 접근할 일이 없습니다.

 필요한 모든 정보가 빌드 시점에 미리 페이지로 렌더링 되어 있기 때문입니다.

- SSG는 높은 확장성과 뛰어난 성능을 보이는 프런트엔드 애플리케이션을 만들고 싶을 때 가장 좋은 방법입니다.

- 한가지 문제점은 일단 웹페이지를 만들고 나면 다음 배포 전까지 내용이 변하지 않는다는 것입니다.

- 조금이라도 수정하려면 필요한 데이터를 가져와서 수정하고 다시 생성하는 과정ㅇ르 반복해야 합니다.

- 이런 문제 때문에 나온 방법이 바로 "증분 정적 재생성(ISR:Incremental Static Regeneration)"입니다.

- 예를 들어 동적 콘텐츠를 제공하지만 해당 콘텐츠 데이터를 로딩 하는데 시간이 오래 걸린다면, SSG와 ISR을 함께 사용하여 문제를 해결할 수 있습니다.

- 많은 양의 데이터를 필요로 하는 복잡한 대시보드를 만든다면, 데이터를 불러오기 위한 REST API 호출에 수 초가 소요됩니다.

- 만일 데이터가 자주 변하지 않는다면 SSG와 ISR을 사용해서 데이터를 10분동안 캐싱할 수 있습니다.

코드 설명(46~48P)

1. getStaticProps 함수를 사용합니다.

2. 빌드 과정에서 페이지를 렌더링할 때 이 함수를 호출해서 필요한 데이터 등을 가져오며, 다음 번 빌드 시점까지 더 이상 호출하지 않습니다.

3. 빌드 과정에서 페이지의 내용을 getStaticProps함수가 반환한 객체의 값으로 채웁니다. 그리고 이 페이지는 빌드를 거쳐 정적 페이지로 만들어집니다.

4. 처음 10분간 해당 페이지를 요청하는 모든 사용자는 동일한 정적 페이지를 제공받습니다.

5. 10분이 지나고 해당 페이지에 대한 새로운 요청이 들어오면 Next.js는 이 페이지를 서버에서 다시 렌더링하고 getStaticProps 함수를 다시 호출합니다. 다시 렌더링한 페이지는 이전 페이지를 덮어씁니다.

6. 이후 10분간 동일한 페이지에 대한 모든 요청에 대해 새로 만든 정적 페이지를 제공합니다.

7. 만일 10분이 지난 후에 페이지에 대한 새로운 요청이 없다면 새로 빌드하지 않습니다.

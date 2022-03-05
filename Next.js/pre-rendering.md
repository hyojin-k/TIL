# pre-rendering

## data-fetching 방식

### getStaticProps

- SSG(Static Site Generation 정적 페이지 생성) 시 사용
- **빌드 시**에 data-fetching이 이루어지고, 빌드 이후에는 변경 불가능
- 고정된 내용이 있는 페이지에 사용
- 호출 시마다 매번 data fetch를 하지 않아 성능면에서 좋음

### getStaticPaths

- 동적 라우팅(Dynamic Routes) + getStaticProps 를 위해 사용
- 빌드 시에 정적으로 렌더링할 경로를 설정 (설정하지 않은 경로는 404에러)

### getServerSideProps

- SSR(Server Side Rendering 서버 사이드 랜더링) 시 사용
- 빌드와 상관없이, 런타임 환경에서 **페이지가 요청 받을 때마다** 호출됨
- 성능 면에서는 getStaticProps보다 떨어지지만, 내용을 동적으로 수정 가능
- 서버사이드에서만 실행되고, 브라우저에서 실행되지 않음

## getServerSideProps
page에서 서버 측 랜더링 함수인 getServerSideProps함수를 export하는 경우 Next.js는 getServerSideProps에서 반환된 데이터를 사용하여 각 request에서 이 페이지를 pre-render합니다.   
getServerSideProps는 서버 측에서만 실행되며 브라우저에서는 실행되지 않습니다.   
https://nextjs.org/docs/basic-features/data-fetching/get-server-side-props

## getServerSideProps를 사용하여 request시 데이터 fetch하기
다음 예는 request 시 데이터를 fetch하고 결과를 pre-render하는 방법을 보여줍니다.
```
export default function Home({ data }) {
// 데이터 랜더링
}

// 매 request마다 실행됩니다.
export async function getServerSideProps() {
const res = await fetch(`https://.../data`);
const data = await res.json();

// props를 통해 page에 data전달
return { props: { data } }
}
```
https://nextjs.org/docs/basic-features/data-fetching/get-server-side-props#using-getserversideprops-to-fetch-data-at-request-time

## getServerSideProps (타입스크립트와 함께 사용하기)
https://nextjs.org/docs/api-reference/data-fetching/get-server-side-props#getserversideprops-with-typescript

## Pre-rendering with Default Data

페이지를 미리 렌더링해야 하는 경우 Next.js는 2가지 형태의 사전 렌더링을 지원합니다.   
Static Generation (SSG), Server-side Rendering (SSR).   
SWR를 사용하면서, SEO를 위해 페이지를 미리 렌더링할 수 있으며 클라이언트 측에서 caching, revalidation, focus tracking, refetching와 같은 기능도 사용할 수 있습니다.   
```
export default function Page({ fallback }) {
// SWRConfig안에 SWR훅은 SWRConfig의 value값을 사용합니다.
// fallback에는 key-value 객체를 통해 캐시의 초기값을 설정할 수 있습니다.
return (
< SWRConfig value={{ fallback }}>
< Article />
< /SWRConfig>
)
}
```
https://swr.vercel.app/docs/with-nextjs#pre-rendering-with-default-data

## withIronSessionSsr

```
export function withSessionSsr(handler) {
return withIronSessionSsr(handler, sessionOptions);
}
```
https://github.com/vvo/iron-session#nextjs-withironsessionssrhandler-ironoptions--req-incomingmessage-res-serverresponse--ironoptions--promiseironoptions

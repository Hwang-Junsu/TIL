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

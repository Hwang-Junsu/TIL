# getStaticPaths

동적인 라우트(동적인 URL)을 갖는 페이지에서 getStaticProps를 사용할 때 필요합니다. (예: [id].tsx)   
동적 경로를 사용하는 페이지에서 getStaticPaths(정적 사이트 생성)라는 함수를 export할 때 Next.js는 getStaticPaths에 의해 지정된 모든 경로를 정적으로 미리 렌더링합니다.   
getStaticPaths는 getStaticProps와 함께 사용해야 합니다. getServerSideProps와 함께 사용할 수 없습니다.   
또한 getStaticPaths는 getStaticProps도 사용하는 동적 경로에서만 export할 수 있습니다.   
```
ex) [slug].tsx
export async function getStaticPaths() {
return {
paths: [
{ params: { slug: "pizza" } }
],
fallback: true // false or 'blocking'
};
}
```
https://nextjs.org/docs/basic-features/data-fetching/get-static-paths

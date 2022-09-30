# Apollo Server소개
Apollo 서버는 Apollo 클라이언트를 포함한 모든 GraphQL 클라이언트와 호환되는 사양 준수(spec-compliant)의 오픈 소스 GraphQL 서버입니다.   
모든 소스의 데이터를 사용할 수 있는 자체 문서화 가능한 production-ready GraphQL API를 구축하는 가장 좋은 방법입니다.   
https://www.apollographql.com/docs/apollo-server/

# Apollo Server시작하기
```
npm install apollo-server graphql
npm install nodemon -D
```
```
const server = new ApolloServer({
typeDefs,
resolvers,
csrfPrevention: true,
});

server.listen().then(({ url }) => {
console.log(`🚀 Server ready at ${url}`);
});
```
https://www.apollographql.com/docs/apollo-server/getting-started/

# GraphQL이 해결하는 문제점

1. Overfetching
필요한 데이터보다 더 많은 데이터를 fetch하는 것을 말합니다.     
GraphQL을 사용하면 API에 GraphQL 쿼리를 보내고 필요한 것만 정확히 얻을 수 있습니다.     
GraphQL 쿼리는 항상 예측 가능한 결과를 반환합니다.   

2. Underfetching
필요한 데이터보다 적은 데이터를 fetch하는 것을 말합니다.   
일반적인 REST API는 여러 URL에서 로딩해야 하지만 GraphQL API는 앱에 필요한 모든 데이터를 단일 request로 가져옵니다. 
GraphQL을 사용하는 앱은 느린 모바일 네트워크 연결에서도 빠를 수 있습니다.   

## Get Now Playing
https://developers.themoviedb.org/3/movies/get-now-playing

# Define your GraphQL schema (GraphQL 스키마 정의)

모든 GraphQL 서버(Apollo Server 포함)는 스키마를 사용하여 클라이언트가 쿼리할 수 있는 데이터 구조를 정의합니다.   
(스키마는 type definitions의 모음입니다.)   
```
// 예시
const typeDefs = gql`
type Book {
title: String
author: String
}

type Query {
books: [Book]
}
`;
```
https://www.apollographql.com/docs/apollo-server/getting-started/#step-3-define-your-graphql-schema

## Scalar types
GraphQL 객체 타입에는 이름과 필드가 있지만 이 필드는 더욱 구체적인 데이터로 해석되어야 합니다. 그 때 스칼라 타입을 사용할 수 있습니다.

GraphQL은 기본 스칼라 타입 세트와 함께 제공됩니다.   
ID: ID 스칼라 타입은 객체를 다시 가져오거나 캐시의 키로 자주 사용되는 고유 식별자를 나타냅니다.   
https://graphql.org/learn/schema/#scalar-types

## Mutations

GraphQL에 대한 대부분은 데이터 fetching이지만, 서버 측 데이터를 수정할 수 있는 방법이 필요합니다.    
서버 측 데이터를 수정하는 모든 작업은 mutation을 통해 보내야 한다는 규칙을 설정하는 것이 유용합니다.   
```
mutation CreateReview($ep: Episode!, $review: ReviewInput!) {
createReview(episode: $ep, review: $review) {
stars
commentary
}
}
```
https://graphql.org/learn/queries/#mutations

## Lists and Non-Null

아래 Character에 name에 String 타입을 사용하고 느낌표 !를 추가하여 Non-Null로 표시합니다.   
Non-Null로 표시하게 되면 서버가 항상 이 필드에 대해 null이 아닌 값을 반환할 것으로 예상합니다. 그래서 null 값을 얻게 되면 클라이언트에게 문제가 있음을 알립니다.   
```
type Character {
name: String!
appearsIn: [Episode]!
}
```
https://graphql.org/learn/schema/#lists-and-non-null

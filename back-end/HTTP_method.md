# HTTP 요청 메서드
HTTP는 요청 메서드를 정의하여, 주어진 리소스에 수행하길 원하는 행동을 나타냅니다. 간혹 요청 메서드를 "HTTP 동사"라고 부르기도 합니다.
https://developer.mozilla.org/ko/docs/Web/HTTP/Methods

## 자주 사용하는 HTTP 요청 메서드들
- GET: GET 메서드는 오직 데이터를 받기만 합니다. (읽기전용)
- POST: POST 메서드는 리소스를 생성할 때 쓰입니다.
- PUT: PUT 메서드는 리소스를 업데이트할 때 쓰입니다.
- DELETE: DELETE 메서드는 특정 리소스를 삭제합니다.
- PATCH: PATCH 메서드는 리소스의 부분만을 수정하는 데 쓰입니다.
등등..

## 5분만에 제대로 설계하는 ⭐️ REST API
https://youtu.be/4DxHX95Lq2U

## 5분만에 제대로 설계하는 ⭐️ REST API (요약)
1. URL에서는 가급적 동사를 사용하지 않는다.
(동사보다는 HTTP request method를 이용)
/seeMovies (GET) -> /movies (GET)
/createMovie (POST) -> /movies (POST)

2. 검색이나 필터를 처리할 때는 query parameter를 이용하는 것이 좋다.
/getTopRatedMovies -> /movies?min_rating=9
/findMoviesFromThisYear -> /movies?release_date=2022

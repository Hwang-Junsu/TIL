# 무한스크롤을 구현
- React.js에서 무한스크롤을 구현하기 위해서 react-Intersection-Observer 라이브러리를 이용하였다.
```
yarn add react-intersection-observer
```
- useInView 훅을 사용하여 ref와 inView를 가져온다. ref는 관찰할 대상을 설정하고, inView는 타겟에 보이지 않으면 false, 보이면 true를 갖습니다.
```javascript
const [ref, inView] = useInView();
```
- useEffect를 사용하여 지정한 타겟이 화면에 보일 때마다 서버에 요청을 보내서 포스트를 받아올 수 있도록 합니다.

# 구현한 코드
```javascript
  const page = React.useRef(1);
  const [hasNextPage, setHasNextPage] = React.useState(true);
  const [posts, setPosts] = React.useState([]);
  const [loading, setLoading] = React.useState(false);
  const [ref, inView] = useInView();
  const onDelete = (id) => {
    setPosts(posts.filter((post) => post.id !== id));
  };
  const fetch = useCallback(async () => {
    try {
      const {data} = await client.get(`/posts?_limit=2&_page=${page.current}`);
      setPosts((prevPosts) => [...prevPosts, ...data]);
      setHasNextPage(data.length === 2);
      if (data.length) {
        page.current += 1;
      }
      setLoading(false);
    } catch (err) {
      console.log(err);
    }
  });
  useEffect(() => {
    if (inView && hasNextPage && !loading) {
      fetch();
      setLoading(true);
    }
  }, [fetch, hasNextPage, inView]);

```
- page 변수를 만들어 api에서 페이지별로 데이터를 가져올 수 있도록 합니다.
- hasNextPage는 api에서 가져온 데이터가 설정한 값만큼 가져왔을 때는 true, 아니면 false
- post state를 임시로 만들어서 데이터를 담아줄 배열을 만들었습니다.
- loading 변수는 스크롤을 빠르게 계속 내릴 시 로딩 전에 데이터가 get되어서 중복되는 데이터가 없게 만들기 위해서 loading 변수를 설정하였음.
- url에서 page별로 나눌수 있는 방법은 `/post?_limit=(원하는 갯수)&_page=(원하는 페이지)` 

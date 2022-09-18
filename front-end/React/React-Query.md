# React-Query
React에서 서버 상태를 가져오고, 캐싱하고, 동기화하고, 업데이트할 수 있는 라이브러리. 비동기 로직을 쉽게 처리할 수 있다.

## 상태
Local State : React 컴포넌트 안에서 사용되는 state    
Global State (Client State) : Global Store에 정의되어 프로젝트 어디서나 접근할 수 있는 state    
Server State : 서버로부터 받아오는 state    
    
    
## 기존의 비동기 로직 처리 (ex. redux, redux-saga)
```
function* fetchUser(action) {
   try {
      const user = yield call(Api.fetchUser, action.payload.userId);
      yield put({type: "USER_FETCH_SUCCEEDED", user: user});
   } catch (e) {
      yield put({type: "USER_FETCH_FAILED", message: e.message});
   }
}
...
// redux
const initialState = {
	isLoading: false,
    user: ...
}
...
```
- 성공, 실패 액션 하나하나를 모두 선언, 이후 redux store에 저장하고 사용
- Global State와 Server State를 동시에 관리
### 단점
- 서버 데이터가 항상 최신 상태임이 보장되지 않는다. fetch를 수행해야만 최신 데이터가 됨.
- 여러 컴포넌트에서 최신 데이터를 받아오려면, fetch를 그 수 만큼 수행해야 한다.
- 매우 큰 보일러플레이트
    
    
---
## React-Query
### useQuery
```
const { isLoading, error, data } = useQuery('user', fetcher, options);
```
- Server State를 읽어오는 hook (read)
- useQuery의 반환 값을 활용하여 성공, 실패 처리 가능 ( isFetching, isLoading, error, state 등 )
- useQuery 첫 번째 인자인 QueryKey에 따라서 캐싱 처리. 캐싱된 쿼리의 QueryKey와 동일한 요청을 하는 쿼리는 같은 것으로 인식하여 fetch하지 않고 캐싱된 쿼리 그대로 사용.
  * 여기서 QueryKey는 user
  * string, array, object 등 유니크한 값이면 된다.
  * array일 경우 순서가 서로 바뀌어도 unique
  * object는 순서가 바뀌면 같은 값으로 인식
- 두 번째 인자 fetcher는 프로미스를 반환하는 함수여야 한다.
- 세 번째 인자 options에는 캐시 만료 시점, refetch 시점, 초기값 등을 설정할 수 있으며 생략 가능하다.
### 주요 option
- ### staleTime
   * fresh -> stale 까지의 시간
   * fresh : 데이터 fetch가 막 이루어진 상태
   * stale : not fresh. 오래된 데이터이므로 업데이트가 필요함.
   * fresh 상태에서 unmount 이후 다시 mount 되어도 fetch 하지 않고 fresh 데이터 사용
   * 기본 값은 0, 0 ~ Infinity까지 설정 가능
- ### cacheTime
   * stale 상태의 데이터가 unmount 된 이후 캐시 데이터가 메모리에 남아있는 시간
   * 시간이 지나면 캐시 데이터는 GC가 수집함
   * 그 전에 다시 mount 된다면 fetch 되는 동안에는 캐시된 데이터 사용
   * 기본 값은 5분, 0 ~ Infinity까지 설정 가능
- ### refetchOnMount ( boolean | "always" )
  * stale 일 때 마운트 시 refetch 실행 여부
  * 기본 값은 true.
  * always 일 경우 fresh 상태에서도 refetch 한다.
- ### retry (boolean | number )
  * 쿼리가 실패했을 때 재시도하는 옵션
  * true : 계속 재시도
  * false : 재시도 X
  * number : 그 수 만큼 재시도, 기본 값은 3
- ### enabled
  * true인 경우만 쿼리 실행
> https://react-query.tanstack.com/reference/useQuery

## queryClient
```
// src/app.tsx
const App = () => {
  const queryClient = new QueryClient({
    defaultOptions: {
      queries: {
        cacheTime: 1000 * 60 * 60 * 24,
        staleTime: 1000 * 60,
        refetchOnMount: false,
        refetchOnReconnect: false,
        refetchOnWindowFocus: false,
      },
    },
  });
  return (
    <QueryClientProvider client={queryClient}>
      {element}
    </QueryClientProvider>
  );
}

export default App;
```
- 캐시된 쿼리를 관리하는 QueryClient 객체.
- Provider안의 모든 컴포넌트에서 getClient() 를 호출함으로써 접근할 수 있다.
- useQuery와 useMutation의 기본 option을 설정할 수 있다.
### 주요 메소드
- ### getQueryData(queryKey)
  * 해당 key에 대해서 캐싱 처리된 쿼리의 데이터를 가져오는 메소드
  * 쿼리가 존재하지 않으면 undefined를 반환함
- ### setQueryData(queryKey, updater)
  * 해당 key에 대해서 캐싱 처리된 쿼리의 데이터를 updater로 직접 수정하는 메소드
  * 쿼리가 존재하지 않으면 새로 생성함
  * updater에는 객체나 함수가 올 수 있다.
  * optimistic update에 사용될 수 있다.
- ### invalidateQueries(queryKey)
  * 해당 key에 대해서 캐싱 처리된 쿼리를 유효하지 않은 것으로 수정하는 메소드
  * 더이상 유효하지 않으니, 새로 받아와서 캐싱 처리해라 라는 뜻. 자동으로 useQuery가 실행된다.
  * 아무 값도 넘겨주지 않으면 캐싱된 모든 쿼리들을 invalidate 함.
https://react-query.tanstack.com/reference/QueryClient#queryclientcancelqueries

## useMutation
```
const { mutate } = useMutation(mutationFn, { options ... })

mutate(variables, { onSuccess, onSettled, onError })
```
- Server State를 변경시키는 hook (create, update, delete)
- return 값 중 mutate는,mutationFn 을 trigger하는 함수이다.
- 객체로 받은 variables를 mutationFn에 넘겨준다.
### 주요 option
- ### onMutate
  * mutationFn이 실행되기 전에 먼저 실행할 함수.
  * mutationFn의 객체 인자와 동일한 값을 넘겨준다.
  * 여기서 반환된 값은 onError, onSettled 함수에 전달된다. (optimistic update에서 사용될 수 있다.)
- ### onSuccess
  * mutationFn이 성공했을 때 실행
  * Server State를 변경시키는 mutation이 성공했으니, 기존에 캐싱된 쿼리 데이터는 예전 데이터이므로 쓸모가 없음. 두 가지 해결 방법이 있다.
  * invalidationQueries(QueryKey)로 해당 쿼리를 invalidate 하고 refetch
  * setQueryData로 직접 캐싱된 쿼리 데이터를 수정. (Optimistic Update) refetch가 일어나지 않음.
- ### onError
  * mutationFn이 실패했을 때 실행
- ### onSettled
  * 두 경우 모두 실행
> https://react-query.tanstack.com/reference/useMutation

## Optimistic Update
- useMutation이 성공할 것이라 가정하고 미리 화면의 UI를 바꾸고 나서, 결과에 따라 확정 / 롤백하는 방식.
```
 const queryClient = useQueryClient()
 
 useMutation(updateTodo, {
   onMutate: async newTodo => {
     await queryClient.cancelQueries('todos')
     // 기존 데이터
     const previousTodos = queryClient.getQueryData('todos')
     // 캐싱 데이터 업데이트
     queryClient.setQueryData('todos', old => [...old, newTodo])

     return { previousTodos }
   },
   onError: (err, newTodo, context) => {
     // 에러 시 캐싱 데이터 롤백
     queryClient.setQueryData('todos', context.previousTodos)
   },
 })
 ```
- onMutate에서 return된 값은 onError와 onSettled의 context에 전달된다. 만약 함수가 return 된다면, 다음과 같이 사용할 수 있다.
```
onMutate: async newTodo => {
  ...
  return () => queryClient.setQueryData('todos', previousTodos)
}
onError: (err, newTodo, rollback) => {
  if (rollback) rollback();
}
```
onMutate에서 데이터 업데이트 후 에러 시 롤백하는 방식이 아니고, onSuccess에서 업데이트 해주는 것도 가능하다. (이러면 optimistic update가 아닌가..?)

> https://react-query.tanstack.com/guides/optimistic-updates#_top

# React-Query
- react-query는 기본적으로 fetcher함수를 return한다.
- isLoading과 data 변수를 활용하여 쉽게 data에 접근할 수 있고, Loading변수를 따로 만들지 않아도 됨.
- 강력한 캐싱기능이 있음. query의 고유한 key값을 넘겨주었다면, 캐시에 어떠한 데이터가 있다는 것을 알고 있기 때문에, 다시 로딩을 하지 않음.

# useQuery Hook
```typescript
// api.ts
const BASE_URL = `https://api.coinpaprika.com/v1`;

export function fetchCoins() {
  return fetch(`${BASE_URL}/coins`).then((response) => response.json());
}

export function fetchCoinInfo(coinId: string) {
  return fetch(`${BASE_URL}/coins/${coinId}`).then((response) =>
    response.json()
  );
}

// coins.tsx

const {isLoading, data} = useQuery<ICoin[]>("allCoins", fetchCoins);
```
- useQuery(uniquekey, fetcher function)을 불러 return한다.
- 첫번째 인자로는 고유한 값의 key를 주어야 한다.

# ReactQueryDevtools
- 캐시에 어떤 query가 있는지, 결과가 무엇인지, Data Explorer를 보여준다.

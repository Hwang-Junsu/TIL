# Dynamic import

Next.js는 JavaScript용 ES2020 Dynamic import()를 지원합니다. 이를 통해 JavaScript 모듈을 동적으로 가져와서 작업할 수 있습니다.   
또한 SSR과 함께 작동합니다. dynamic()은 React.lazy와 유사하게 사전 로드가 작동하도록 모듈의 최상위에 표시되어야 하므로 React 렌더링 내부에서 사용할 수 없습니다.   
ex) 사용자가 검색을 입력한 후에만 브라우저에서 모듈을 동적으로 로드합니다.   
```
import dynamic from 'next/dynamic'

const DynamicComponent = dynamic(() => import('../components/hello'))

< div>
< DynamicComponent />
< /div>
```
https://nextjs.org/docs/advanced-features/dynamic-import
   
## With custom loading component
Dynamic Component가 로드되는 동안 로드 상태를 렌더링하기 위해 선택적 로딩 컴포넌트를 추가할 수 있습니다.
https://nextjs.org/docs/advanced-features/dynamic-import#with-custom-loading-
```
const DynamicComponentWithCustomLoading = dynamic(
() => import('../components/hello'),
{ loading: () => Loading... }
)
```

## With no SSR
항상 server side에 모듈을 포함하고 싶지는 않을 수 있습니다. 예를 들어 모듈에 브라우저에서만 작동하는 라이브러리가 포함된 경우에는 ssr: false를 통해 CSR으로 실행합니다.   

## With suspense
suspense를 사용하면 React.lazy 및 React 18의 Suspense와 유사한 컴포넌트를 지연 로드(lazy-load)할 수 있습니다. fallback이 있는 클라이언트 측 또는 서버 측에서만 작동합니다.   
동시 모드에서 완전한 SSR 지원은 아직 진행 중입니다.   
```
const DynamicLazyComponent = dynamic(() => import('../components/hello4'), {
suspense: true,
})

< Suspense fallback={`loading`}>
< DynamicLazyComponent />
< /Suspense>
```
https://nextjs.org/docs/advanced-features/dynamic-import#with-custom-loading-component

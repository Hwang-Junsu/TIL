# Custom Document
Custom Document는 페이지를 랜더링하는 데 사용되는 html 및 body 태그를 업데이트할 수 있습니다.    
이 파일은 서버에서만 랜더링되므로 onClick과 같은 이벤트 핸들러는 \_document에서 사용할 수 없습니다.    
Html, Head, Main 및 NextScript는 페이지가 제대로 랜더링되는 데 필요합니다.
```
import { Html, Head, Main, NextScript } from 'next/document'

export default function Document() {
return (
< Html>
  < Head />
    < body>
      < Main />
      < NextScript />
    < /body>
< /Html>
)
}
```
https://nextjs.org/docs/advanced-features/custom-document

Custom Document (Typescript)
https://nextjs.org/docs/advanced-features/custom-document#typescript

Noto Sans Korean 폰트
< link href="https://fonts.googleapis.com/css2?family=Noto+Sans+KR&display=swap" rel="stylesheet" />

Open Sans 폰트
< link href="https://fonts.googleapis.com/css2?family=Open+Sans:ital@1&display=swap" rel="stylesheet" />

## Script Component

Next.js Script 컴포넌트인 next/script는 HTML script 태그의 확장입니다.    
이를 통해 개발자는 애플리케이션에서 써드 파티 스크립트의 로드되는 우선 순위를 설정할 수 있으므로 개발자 시간을 절약하면서 로드하는 성능을 향상시킬 수 있습니다.   

- beforeInteractive: 페이지가 interactive 되기 전에 로드   
- afterInteractive: (기본값) 페이지가 interactive 된 후에 로드   
- lazyOnload: 다른 모든 데이터나 소스를 불러온 후에 로드   
- worker: (실험적인) web worker에 로드   
``` 
import Script from 'next/script'

< Script src="https://connect.facebook.net/en_US/sdk.js" strategy="lazyOnload" / >
```
https://nextjs.org/docs/basic-features/script

Kakao SDK   
```
< script src="https://developers.kakao.com/sdk/js/kakao.js" / >
```

Facebook SDK   
```
< script src="https://connect.facebook.net/en_US/sdk.js" / >
```
```
onLoad={() => {
  window.fbAsyncInit = function () {
    FB.init({
    appId: "your-app-id",
    autoLogAppEvents: true,
    xfbml: true,
    version: "v13.0",
});
};
}}
```

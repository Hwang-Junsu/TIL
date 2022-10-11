## API Routes

API route는 Next.js로 API를 빌드하기 위한 솔루션을 제공합니다.    
pages/api 폴더 내의 모든 파일은 /api/ 에 매핑되며 API endpoint로 처리됩니다.    
server-side 전용 번들이며 client-side 번들 크기를 늘리지 않습니다.   
req: http.IncomingMessage의 인스턴스와 pre-built된 일부 미들웨어   
res: http.ServerResponse의 인스턴스와 일부 helper함수   

예를 들어 다음 API 경로 pages/api/user.js는 상태 코드가 200인 json 응답을 반환합니다.   
```
export default function handler(req, res) {
res.status(200).json({ name: 'John Doe' })
}
```
https://nextjs.org/docs/api-routes/introduction

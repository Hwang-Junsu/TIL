## Iron session
데이터를 저장하기 위해 서명되고 암호화된 쿠키를 사용하는 Node.js stateless session 유틸리티.   
Next.js, Express, Nest.js, Fastify 및 모든 Node.js HTTP 프레임워크와 함께 작동합니다.    
세션 데이터는 암호화된 쿠키("seals")에 저장됩니다. 그리고 당신의 서버만이 세션 데이터를 디코딩(decode)할 수 있습니다.    
세션 ID가 없으므로 서버 관점에서 iron session을 "stateless"로 만듭니다.   
npm i iron-session
```
import { withIronSessionApiRoute } from "iron-session/next";

export default withIronSessionApiRoute(NextApiHandler)
```
https://github.com/vvo/iron-session   

req.session.save()   
세션 데이터를 암호화하고 쿠키를 설정합니다.   

32자 랜덤 비밀번호 필요하신 분들은 아래 사이트에서 Length 32로 설정 후 복사해서 사용하시면 됩니다.   
https://1password.com/password-generator/   

## TypeScript로 세션 데이터 Tying (req.session에 데이터 입력)
req.session은 자동으로 올바른 유형으로 채워지므로 .save() 및 .destroy()를 호출할 수 있습니다.   
그러나 더 나아가 세션 데이터도 입력할 수 있습니다. 이 코드는 특정 시점에 필요한 파일에 있는 한 프로젝트의 아무 곳에나 넣을 수 있습니다.   
```
declare module "iron-session" {
interface IronSessionData {
user?: {
id: number;
admin?: boolean;
};
}
}
```
https://github.com/vvo/iron-session#typing-session-data-with-typescript

## Module Augmentation
(위와 같이 모듈을 가져와서 module augmentation을 사용해서 컴파일러에게 알려줄 수 있습니다.)   
JavaScript 모듈은 병합을 지원하지 않지만 기존 객체를 가져온 다음 업데이트하여 패치할 수 있습니다.   
```
import { Observable } from "./observable";

declare module "./observable" {
interface Observable< T> {
map< U>(f: (x: T) => U): Observable< U>;
}
}
```
https://www.typescriptlang.org/docs/handbook/declaration-merging.html#module-augmentation

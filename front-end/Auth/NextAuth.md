# NextAuth.js
Next.js에서 Authentication 구현을 도와주는 패키지이다.   
npm i next-auth   

## Getting Started
아래 예제 코드는 Next.js 앱에 인증을 추가하는 방법을 설명합니다.
```
// pages/api/auth/[...nextauth].js
import NextAuth from "next-auth"
import GithubProvider from "next-auth/providers/github"

export default NextAuth({
// Configure one or more authentication providers
providers: [
GithubProvider({
clientId: process.env.GITHUB_ID,
clientSecret: process.env.GITHUB_SECRET,
}),
// ...add more providers here
],
})
```
https://next-auth.js.org/getting-started/example

## Next.js에 대한 인증
NextAuth.js는 Next.js 애플리케이션을 위한 완전한 오픈 소스 인증 솔루션입니다. Next.js 및 Serverless를 지원하도록 처음부터 설계되었습니다.   
https://www.npmjs.com/package/next-auth 

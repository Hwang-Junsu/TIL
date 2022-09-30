# Typescript 설정

1. 기존 Create React App으로 만든 프로젝트에 타입스크립트 설치
npm install --save typescript @types/node @types/react @types/react-dom @types/jest
+tsconfig.json파일이 없다면 추가로 설정

2. Create React App을 타입스크립트로 시작하기

```
npx create-react-app [my-app] --template typescript
yarn create-react-app [my-app] --template typescript
```
또는   
You are running `create-react-app` 4.0.3, which is behind the latest release (5.0.0). 오류가 뜬다면 아래 명령어로 진행
```
npx create-react-app@5.0.0 my-app --template typescript
```

+ create-react-app의 글로벌 설치는 더 이상 지원되지 않습니다.
이전에 npm install -g create-react-app를 통해 전역적으로 create-react-app을 설치한 경우 npm uninstall -g create-react-app을 사용하여 패키지를 제거하는 것이 좋습니다.

https://create-react-app.dev/docs/adding-typescript

DefinitelyTyped
https://github.com/DefinitelyTyped/DefinitelyTyped

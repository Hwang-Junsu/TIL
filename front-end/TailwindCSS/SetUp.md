# Tailwind CSS설치 및 초기화
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p (-p를 붙이면 postcss.config.js파일까지 생성)
https://tailwindcss.com/docs/installation/using-postcss

# Prettier를 통한 TailwindCSS 클래스 자동 정렬 플러그인
(TailwindCSS 공식 Prettier플러그인)
blueschist님이 소개해주신 TailwindCSS 클래스 자동 정렬 플러그인입니다. 사용 방법은 아래와 같이 설치 후, 파일 저장시 클래스가 순서에 맞게 자동으로 정렬되도록 도와줍니다.
npm install -D prettier prettier-plugin-tailwindcss
```
// 클래스 정렬 전    
button class="text-white px-4 sm:px-8 py-2 sm:py-3 bg-sky-700 hover:bg-sky-800"    

// 클래스 정렬 후    
button class="bg-sky-700 px-4 py-2 text-white hover:bg-sky-800 sm:px-8 sm:py-3"    
```
https://tailwindcss.com/blog/automatic-class-sorting-with-prettier
https://github.com/tailwindlabs/prettier-plugin-tailwindcss

클래스 정렬 기준
https://tailwindcss.com/blog/automatic-class-sorting-with-prettier#how-classes-are-sorted

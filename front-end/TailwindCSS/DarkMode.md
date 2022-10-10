# Dark Mode
Tailwind에는 dark 모드가 활성화되어 있을 때 사이트 스타일을 다르게 지정할 수 있습니다.   
현재 사용 중인 컴퓨터에서 설정한 라이트 모드 또는 다크 모드에 따라 dark가 자동으로 적용됩니다.   
ex) dark:bg-slate-900   
https://tailwindcss.com/docs/dark-mode 

## 수동으로 다크 모드 전환   
운영 체제 기본 설정에 의존하는 대신 수동으로 다크 모드 전환을 지원하려면 media 대신 class을 사용하십시오.   
```
// tailwind.config.js
module.exports = {
// 클래스를 기준으로 다크모드 적용 (최상위 부모에 dark클래스 지정)
darkMode: 'class',

// @media(prefers-color-scheme)를 기준으로 다크모드 적용 (기본 값)
darkMode: "media",
}
```
https://tailwindcss.com/docs/dark-mode#toggling-dark-mode-manually

## prefers-color-scheme
prefers-color-scheme CSS 미디어 특성은 사용자의 시스템이 라이트 테마나 다크 테마를 사용하는지 탐지하는 데에 사용됩니다.   
```
@media (prefers-color-scheme: light) {
.themed {
background: white;
color: black;
}
}
```
https://developer.mozilla.org/ko/docs/Web/CSS/@media/prefers-color-scheme

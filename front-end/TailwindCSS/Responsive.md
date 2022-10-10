# Mobile First

기본적으로 Tailwind는 Bootstrap과 같은 다른 프레임워크에서 사용하는 것과 유사한 모바일 우선 breakpoint 시스템을 사용합니다.    
이것이 의미하는 바는 접두사가 붙지 않은 유틸리티(예: uppercase)는 모든 화면 크기에 적용되는 반면 접두사가 붙은 유틸리티(예: md:uppercase)는 지정된 breakpoint 이상에서만 적용됩니다.   

이 접근 방식이 사람들을 가장 자주 놀라게 하는 부분은 모바일용으로 스타일을 지정하려면 sm: 접두사가 붙은 버전이 아니라 접두사가 없는 버전의 유틸리티를 사용해야 한다는 것입니다.    
sm을 "작은 화면에서"를 의미하는 것으로 생각하지 마십시오. "작은 breakpoint"로 생각하십시오.   
div class="sm:text-center" => 작은 사이즈 (not 모바일)   

이러한 이유로 디자인을 위한 모바일 레이아웃을 먼저 구현한 다음 sm 화면에 적합한 변경 사항을 레이어링한 다음 md 화면 등을 적용하는 것이 좋습니다.   
```
sm 640px @media (min-width: 640px) { ... }
md 768px @media (min-width: 768px) { ... }
lg 1024px @media (min-width: 1024px) { ... }
xl 1280px @media (min-width: 1280px) { ... }
2xl 1536px @media (min-width: 1536px) { ... }
```
https://tailwindcss.com/docs/responsive-design#mobile-first

## Customizing breakpoints
https://tailwindcss.com/docs/responsive-design#customizing-breakpoints

## Viewport orientation

portrait 및 landscape 수정자를 사용하여 뷰포트가 특정 방향에 있을 때 조건부로 스타일을 추가합니다.   
```
div class="portrait:hidden"
div class="landscape:hidden"
```
https://tailwindcss.com/docs/hover-focus-and-other-states#viewport-orientation

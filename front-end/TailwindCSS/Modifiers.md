# TailwindCSS Modifier 리스트

기본적으로 Tailwind에 포함된 모든 단일 modifier들입니다.
(~일 때 실행하는 것들)
```
- Modifier(왼쪽), CSS(오른쪽)
- hover (&:hover)
- focus (&:focus)
- active (&:active)
- first (&:first-child)
- disabled (&:disabled)
- sm (@media (min-width: 640px))
- md ( @media (min-width: 768px))
- lg (@media (min-width: 1024px))
- dark (@media (prefers-color-scheme: dark))
등등
```
https://tailwindcss.com/docs/hover-focus-and-other-states#quick-reference

## Ring Width
상자 그림자가 있는 윤곽선을 만들기 위한 유틸리티입니다.    
ring-{width} 유틸리티를 사용하여 특정 두께의 solid box-shadow를 요소에 적용합니다. 링은 기본적으로 반투명한 파란색으로 많은 시스템의 기본 포커스 링 스타일과 유사합니다.    
ex) ring-2 ring-offset-2 focus:ring-2 ring-red-500
```
button class="ring-2 ring-offset-2 focus:ring-2"
div class="ring-2 hover:ring-4 md:ring-4"
```
https://tailwindcss.com/docs/ring-width

## Ring Color
외곽선 링의 색상을 설정하는 유틸리티입니다.    
ring-{color} 유틸리티를 사용하여 외곽선 링의 색상을 설정합니다.    
```
button class="... ring-2 ring-blue-500"
button class="... ring-2 ring-blue-500/50
```
https://tailwindcss.com/docs/ring-color

## :empty

empty modifier를 사용하여 콘텐츠가 없는 경우 스타일을 지정합니다.    
콘텐츠가 없는 경우=>빈 텍스트, undefined, null등과 같이 값이 없는 경우에 해당    
+ empty:hidden은 display: none과 같다.   
```
{[1, 2, ""].map((number) => (
< h3 className="bg-red-500 empty:hidden" key={number}>
{number}
< /h3>
))}
```
https://tailwindcss.com/docs/hover-focus-and-other-states#empty

짝수=> even:bg-blue-200   
홀수=> odd:bg-red-200   

+ first: 적용안 되시는 분들은 first-of-type:으로 해보세요.

## group
상위(부모) 상태를 기반으로 한 스타일 지정    
일부 부모 요소의 상태를 기반으로 요소의 스타일을 지정해야 하는 경우 부모를 group 클래스로 표시하고 group-hover와 같은 group-* 수정자를 사용하여 대상 요소의 스타일을 지정합니다.    
이 패턴은 group-focus, group-active 또는 group-odd와 같은 모든 유사 클래스 수정자와 함께 작동합니다.   
``` 
< a href="#" class="group">
< h3 class="group-hover:text-white">New project< /h3>
< /a>
```
https://tailwindcss.com/docs/hover-focus-and-other-states#styling-based-on-parent-state

## peer
형제 상태를 기반으로 한 스타일 지정    
형제 요소의 상태를 기반으로 요소의 스타일을 지정해야 하는 경우 형제를 peer 클래스로 표시하고 peer-invalid와 같은 peer-* 수정자를 사용하여 대상 요소의 스타일을 지정합니다.   
이 패턴은 모든 유사 클래스 수정자(예: peer-focus, peer-required 및 peer-disabled)와 함께 작동합니다.   
```
< input class="peer"/ >   
< p class="peer-invalid:visible"> Pizza< /p>   
```
https://tailwindcss.com/docs/hover-focus-and-other-states#styling-based-on-sibling-state

## details
HTML details 요소는 "열림" 상태일 때만 내부 정보를 보여주는 정보 공개 위젯을 생성합니다. 요약이나 레이블은 summary 요소를 통해 제공할 수 있습니다.   
정보 공개 위젯은 보통 레이블 옆의 작은 삼각형이 돌아가면서 열림/닫힘 상태를 나타냅니다. details 요소의 첫 번째 자식이 summary 요소라면, summary의 콘텐츠를 위젯의 레이블로 사용합니다.
```
< details>
< summary>Details
Something small enough to escape casual notice.
< /details>
```
https://developer.mozilla.org/ko/docs/Web/HTML/Element/details

## File input buttons
파일 수정자를 사용하여 파일 입력의 버튼 스타일 지정   
ex) file:mr-4 file:py-2 file:px-4   
https://tailwindcss.com/docs/hover-focus-and-other-states?email=george%40krugerindustrial&password=Bosco#file-input-buttons   

## ::file-selector-button
::file-selector-button CSS 의사 요소는 type="file"의 input 버튼을 나타냅니다.   
ex) input[type=file]::file-selector-button   
https://developer.mozilla.org/en-US/docs/Web/CSS/::file-selector-button

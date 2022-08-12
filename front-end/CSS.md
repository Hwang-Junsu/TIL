# Selector
- 꾸밀 요소를 선택하는 선택자. 무엇을 꾸밀 지 선택하고 속성을 넣어 예쁘게 꾸며주는 것.
```HTML
/* id selector */
#id{...}

/* class selector */
.class{...}

/* tag selector */
tagename{...}

/* 여러 요소 선택하기 */
#id, .class{...}

/* sudo selector */
/* 어떤 요소가 특정 상태(마우스 올림, 포커스 됨 등등)일 때만 선택하게 해주는 선택자 */
button:hover{...}

```


# Grid
- DOM 요소들은 기본적으로 박스 형태로 표시된다. (p, div할 것 없이 모두 네모난 영역)
1. Box Model   
![BoxModel](https://teamsparta.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F23346a1c-11eb-4da2-9055-27a1450a296a%2F%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2021-08-27_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_3.44.57.png?table=block&id=dba08a5d-dc6a-4988-9a2e-1c0aa57aebaf&spaceId=83c75a39-3aba-4ba4-a792-7aefe4b07895&width=1530&userId=&cache=v2)
- margin box : 가장 바깥 영역. 주로 다른 요소들과 간격을 줄 때.
- border box : 테두리 영역. border 속성으로 테두리를 주면 이 영역이 바뀜
- padding box : 테두리와 콘텐츠 사이의 영역.
- contents box : 실제 콘텐츠 영역. width, heigth 등으로 사이즈를 줄 수 있고, 따로 지정하지 않을 경우 콘텐츠 내용(글이나 이미지 등)에 따라 임의로 사이즈가 잡힘
2. Display
- flex :
- block :
- grid : 

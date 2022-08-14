# 긴 문자 처리 Tip
```javascript
{toDo.comment.length >= 38
  ? toDo.comment.slice(0, 38) + "..."
  : toDo.comment}
```
- 박스 내부에서 글자의 길이가 넘어갈 때, 적정 길이를 설정하고 삼항연산자를 통해 slice된 문자와 "..."을 조합해 render한다.

# React Hook Form
사용하기 쉬운 유효성 검사를 통해 성능이 뛰어나고 유연하며 확장 가능한 form입니다.   
npm install react-hook-form
```
const {
register,
handleSubmit,
formState: { errors },
} = useForm();

input {...register('lastName', { required: true })}
```
https://react-hook-form.com

## register: (name: string, RegisterOptions?) => ({ onChange, onBlur, name, ref })
이 메서드를 사용하면 input을 등록하거나 element를 선택하고 유효성 검사 규칙을 React Hook Form에 적용할 수 있습니다.   
유효성 검사 규칙은 모두 HTML 표준을 기반으로 하며 사용자 지정 유효성 검사 방법도 허용합니다.   

## watch: (names?: string | string[] | (data, options) => void) => unknown
input의 변화를 구독합니다. 이 메서드는 지정된 input을 감시하고 해당 값을 반환합니다. input 값을 렌더링하고 조건에 따라 무엇을 렌더링할지 결정하는 데 유용합니다.

## handleSubmit: ((data: Object, e?: Event) => void, (errors: Object, e?: Event) => void) => Function

이 함수는 form 유효성 검사가 성공하면 form 데이터를 받습니다.  
```
const { register, handleSubmit } = useForm();
const onSubmit: SubmitHandler = data => console.log(data);

form onSubmit={handleSubmit(onSubmit)}
```
https://react-hook-form.com/api/useform/handlesubmit

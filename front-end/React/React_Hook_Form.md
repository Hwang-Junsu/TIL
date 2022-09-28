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

## 정규표현식
- ^ 문장의 시작
- + 하나 또는 하나이상
```
/^[A-Za-z0-9._%+-]+@naver.com$/
/^[A-Za-z0-9._%+-]+@naver.com/g
```
https://www.regexpal.com

## React Hook Form (TypeScript)
React Hook Form은 TypeScript로 빌드되었으며, FormData 유형을 정의하여 form 값을 지원할 수 있습니다.
```
interface FormData = {
firstName: string;
lastName: string;
};

const { register, setValue, handleSubmit, formState: { errors } } = useForm< FormData >();
```
https://react-hook-form.com/get-started#TypeScript

## defaultValues: Record< string, any > = {}
input에 대한 defaultValues는 사용자가 component와 상호 작용하기 전에 component가 처음 렌더링될 때 초기 값으로 사용됩니다.   
모든 input에 대한 defaultValues를 빈 문자열이나 null과 같은 정의되지 않은 값으로 설정하는 것이 좋습니다.   
https://react-hook-form.com/api/useform#props   

## setError:(name: string, error: FieldError, { shouldFocus?: boolean }) => void
이 함수를 사용하면 하나 이상의 오류를 수동으로 설정할 수 있습니다.   
(수동으로 input 오류 설정)   
https://react-hook-form.com/api/useform/seterror   

## shouldFocus?: boolean
오류를 설정하는 동안 input에 focus을 맞춰야 합니다.   
input이 비활성화되면 shouldFocus가 작동하지 않습니다.   

validate: Function | Object   
```
validate: value => value === '1'
validate: {
positive: v => parseInt(v) > 0,
lessThanTen: v => parseInt(v) < 10,
checkUrl: async () => await fetch(),
}
```

## clearErrors: (name?: string | string[]) => void
이 함수는 form의 오류 메세지를 수동으로 지울 수 있습니다.   
setError()로 설정한 메세지를 삭제할 수 있습니다.   
```
clearErrors('username');
onClick={() => clearErrors(["firstName", "lastName"])}
```

### 라인 끝에 커서 포커싱하기 (VSCode단축키)
option(alt)+shift+i

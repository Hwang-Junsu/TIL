## Update or create records (upsert)

upsert()는 기존 데이터를 업데이트하거나 새 데이터베이스 레코드를 생성합니다.     
다음 쿼리는 upsert를 사용하여 특정 이메일 주소로 사용자 레코드를 업데이트하거나, 존재하지 않는 경우 해당 사용자 레코드를 생성합니다.   
```
const upsertUser = await prisma.user.upsert({
where: {
email: 'hello@gmail.com', // email이 존재하는지 찾고, 존재하면 update 실행
},
update: {
name: 'pizza',
},
create: {
email: 'hello@gmail.com', // email이 존재하지 않다면 생성
name: 'pizza',
},
})
```
https://www.prisma.io/docs/concepts/components/prisma-client/crud#update-or-create-records   
https://www.prisma.io/docs/reference/api-reference/prisma-client-reference#upsert   

PlanetScale 데이터베이스 연결
pscale connect [name]

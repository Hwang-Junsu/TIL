# Prisma

차세대 Node.js 및 TypeScript ORM(Object Relational Mapping)    
Prisma는 앱 개발자가 PostgreSQL, MySQL, SQL Server, SQLite 및 MongoDB(현재 프리뷰)용 오픈 소스 데이터베이스 도구를 사용하여 더 빠르게 빌드하고 오류를 줄이는 데 도움이 됩니다.

https://www.prisma.io/   

# Prisma 셋업 (Typescript + MySQL)

1. npm install prisma -D

2. npx prisma init
이 명령은 schema.prisma라는 파일과 프로젝트 루트에 .env 파일을 포함하는 prisma라는 새 디렉토리를 생성했습니다. schema.prisma는 데이터베이스 연결과 Prisma Client 생성기가 있는 Prisma 스키마를 포함합니다. .env는 환경 변수를 정의하기 위한 dotenv 파일입니다. (데이터베이스 연결에 사용됨)
https://www.prisma.io/docs/getting-started/setup-prisma/start-from-scratch/relational-databases-typescript-mysql

Prisma Model 예시   
https://www.prisma.io/docs/concepts/components/prisma-schema

VSCode Prisma Extension   
https://marketplace.visualstudio.com/items?itemName=Prisma.prisma

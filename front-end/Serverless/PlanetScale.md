# PlanetScale
MySQL과 호환되는 Serverless 데이터베이스 플랫폼   
https://planetscale.com/

# Vitess 
Vitess는 MySQL을 스케일링하기 위한 데이터베이스 클러스터링 시스템   
인터넷에서 가장 큰 사이트를 호스팅하는 강력한 오픈 소스 기술입니다.   
https://vitess.io/

## Vitess를 사용하는 이유
1. 수평 스케일   
2. 고가용성 (Vitess의 기본 복제본 구성은 예기치 않은 이벤트가 발생할 때 기본에서 복제본으로 원활한 장애 조치를 허용합니다.)   
3. MySQL 호환   
4. 쿠버네티스 네이티브   
5. 구체화된 뷰   
6. 온라인 스키마 마이그레이션   

## PlanetScale CLI
PlanetScale은 데이터베이스 이상이며 CLI는 복잡한 명령 이상입니다.    
pscale 커맨드 라인을 사용하면 branch, deploy 요청 및 기타 PlanetScale 개념을 손쉽게 사용할 수 있습니다.   
https://github.com/planetscale/cli

## Planet Scale cli 설치 (맥)
터미널에서 아래를 차례대로 실행   
1. brew install planetscale/tap/pscale
(pscale은 Homebrew Tap을 통해 사용할 수 있습니다.)
2. brew install mysql-client (mysql client설치)
3. brew upgrade pscale (최신 버전 업데이트)

## Planet Scale cli 설치 (윈도우)
1. Scoop 설치 (Windows용 커맨드 라인 설치 프로그램)
https://scoop.sh/
2. scoop bucket add pscale https://github.com/planetscale/scoop-bucket.git
3. scoop install pscale mysql
4. scoop update pscale

## PlanetScale CLI를 사용하여 데이터베이스를 생성
pscale database create carrot-market --region ap-northeast

## DATABASE_URL
mysql://127.0.0.1:3306/carrot-market   
IP 주소 127.0.0.1은 localhost 또는 루프백 주소 라고하는 특수 목적의 IPv4 주소 입니다.   

## Prisma를 통한 MySQL 데이터베이스 서버에 연결
ex) mysql://USER:PASSWORD@HOST:PORT/DATABASE   
https://www.prisma.io/docs/concepts/database-connectors/mysql

PlanetScale 프리티어 사용시 한 개의 데이터베이스만 이용 가능   
추가로 데이터베이스 생성할 때 Error: This organization is at its limit of 1 free database. 오류 발생   

## Prisma Client and schema preview features
Prisma Client 및 Prisma 스키마에 대해 Preview feature 플래그를 사용할 수 있습니다.   
https://www.prisma.io/docs/concepts/components/preview-features/client-preview-features   

## Referential integrity (참조 무결성)
(어떤 다른 모델을 참조하는 경우 해당 모델이 반드시 존재해야 함)   
참조 무결성은 모든 참조가 유효함을 나타내는 데이터 세트의 속성입니다.    
참조 무결성을 위해서는 한 레코드가 다른 레코드를 참조하는 경우 반드시 해당 참조하는 레코드가 존재해야 한다.    
예를 들어 Post 모델이 user필드를 정의하는 경우 User(모델)도 반드시 존재해야 합니다.    
참조 무결성은 참조를 손상시키는 변경을 방지하는 제약 조건과 레코드를 업데이트하거나 삭제할 때 실행되는 참조 작업을 정의함으로써 적용됩니다.    
https://www.prisma.io/docs/concepts/components/prisma-schema/relations/referential-integrity

## datasource에서 referential integrity 설정
referential integrity(참조 무결성)은 현재 previewFeatures입니다. 이를 활성화하려면 schema.prisma의 generator 블록에 있는 previewFeatures 목록에 추가합니다.  
```
// schema.prisma
generator client {
provider = "prisma-client-js"
previewFeatures = ["referentialIntegrity"]
}

datasource db {
provider = "mysql"
url = env("DATABASE_URL")
referentialIntegrity = "prisma"
}
```
https://www.prisma.io/docs/concepts/components/prisma-schema/relations/referential-integrity#setting-the-referential-integrity-in-the-datasource

## db push
db push는 Prisma Migrate와 동일한 엔진을 사용하여 Prisma 스키마를 데이터베이스 스키마와 동기화하며 스키마 프로토타이핑에 가장 적합합니다.   
npx prisma db push   
https://www.prisma.io/docs/concepts/components/prisma-migrate/db-push   

## Prisma Client

TypeScript 및 Node.js용 직관적인 데이터베이스 클라이언트   
Prisma Client는 생각하는 방식으로 구성하고 앱에 맞춤화된 유형으로 Prisma 스키마에서 자동 생성되는 쿼리 빌더입니다.   
npm install @prisma/client   
```
import { PrismaClient } from '@prisma/client'

const prisma = new PrismaClient()
```
https://www.prisma.io/docs/concepts/components/prisma-client

Prisma Studio   
npx prisma studio

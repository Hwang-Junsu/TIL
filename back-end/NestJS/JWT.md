# JWT(Json Web Token)
- json형식을 사용해서 사용자의 정보를 저장하는 웹 토큰
- 세션과 달리 서버가 아닌 클라이언트에 저장되기 때문에 메모리나 스토리지 등을 통해 세션을 관리했던 서버의 부담을 덜 수 있다.
- JWT는 Header, Payload, Signature로 구성됨.
> Header: 타입과 해시 알고리즘 종류   
> Payload: 서버에서 첨부한 사용자 권한 정보와 데이터   
> Signature: Header와 Payload를 Base64 url-safe encode를 한 이후 header에 명시된 해시함수를 적용하고, 개인키로 서명한 전자서명.   
   
ex) aaaaa.bbbbbb.ccccc

# JWT with NestJS
https://docs.nestjs.com/security/authentication#jwt-functionality   

## Authentication Logic

Login을 진행할 때   
Front에서 Login Request (email, password) => Back-end는 Login API를 secret key를 확인하여 JWT를 생성하고 Front로 발급해줌.

Front에서 auth가 필요한 api를 사용했을 때 (JWT) => Back   
Back-end 안에서는 JWT Guard => JWT Strategy => secret key 참조 => reqeust.user => api response

### npm install
```
$ npm install --save @nestjs/passport passport passport-local
$ npm install --save-dev @types/passport-local
$ npm install --save @nestjs/jwt passport-jwt
$ npm install --save-dev @types/passport-jwt
```

### Make Module
```
nest g module auth
nest g service auth
```

1. Authentication 관련 로직을 담당하는 폴더를 구성해준다.
```bash
├── auth
├────── jwt
│   ├── jwt.guart.ts
│   ├── jwt.payload.ts
│   └── jwt.strategy.ts
│ ├─ auth.module.ts
│ └─ auth.service.ts
``` 
2. jwt Guard를 설정해준다.
```
import { Injectable } from '@nestjs/common';
import { AuthGuard } from '@nestjs/passport';

//AuthGuard는 Strategy기능을 자동으로 실행해줌.

@Injectable()
export class JWTAuthGuard extends AuthGuard('jwt') {}
```

3. jwt Strategy Setting & Logic
```
import { UsersRepository } from './../../users/users.repository';
import { Payload } from './jwt.payload';
import { Injectable, UnauthorizedException } from '@nestjs/common';
import { PassportStrategy } from '@nestjs/passport';
import { ExtractJwt, Strategy } from 'passport-jwt';

// jwtFromRequest : 헤더에 토큰으로부터 추출
// secretKey는 환경변수로 저장
// ignoreExpiration 토큰의 만료시간을 설정.

@Injectable()
export class JwtStrategy extends PassportStrategy(Strategy) {
  constructor(private readonly userRepository: UsersRepository) {
    super({
      jwtFromRequest: ExtractJwt.fromAuthHeaderAsBearerToken(),
      secretOrKey: 'secret',
      ignoreExpiration: false,
    });
  }

  async validate(payload: Payload) {
    const user = await this.userRepository.findUserByIdWithoutPassword(
      payload.sub,
    );

    if (user) {
      return user; // request.user
    } else {
      throw new UnauthorizedException('Access Error');
    }
  }
}

```

4. auth.module.ts Setting & Logic
```
import { UsersModule } from './../users/users.module';
import { JwtStrategy } from './jwt/jwt.strategy';
import { AuthService } from './auth.service';
import { forwardRef, Module } from '@nestjs/common';
import { PassportModule } from '@nestjs/passport';
import { JwtModule } from '@nestjs/jwt';

// Passport모듈에는 strategy에 대한 설정을 할수 있음.
@Module({
  imports: [
    PassportModule.register({ defaultStrategy: 'jwt', session: false }),
    JwtModule.register({ secret: 'secret', signOptions: { expiresIn: '1y' } }),
    forwardRef(() => UsersModule),
  ],
  providers: [AuthService, JwtStrategy],
  exports: [AuthService],
})
export class AuthModule {}
```
5. auth.service.ts Setting & Logic
```
import { UsersRepository } from './../users/users.repository';
import { UserSignInDto } from './../users/dto/signin-user.dto';
import { Injectable, UnauthorizedException } from '@nestjs/common';
import * as bcrypt from 'bcrypt';
import { JwtService } from '@nestjs/jwt';

@Injectable()
export class AuthService {
  constructor(
    private readonly usersRepository: UsersRepository,
    private readonly jwtService: JwtService, // 의존성 주입을 해줌.
  ) {}
  async jwtLogIn(data: UserSignInDto) {
    const { email, password } = data;
    const user = await this.usersRepository.findUserByEmail(email);
    if (!user) {
      throw new UnauthorizedException('check email');
    }

    const isPasswordValidated: boolean = await bcrypt.compare(
      password,
      user.password,
    );

    if (!isPasswordValidated) {
      throw new UnauthorizedException('check password');
    }

    const payload = { email: email, sub: user.id };
    return {
      token: this.jwtService.sign(payload), // payload를 token으로 서명하여 리턴해줌.
    };
  }
}
```

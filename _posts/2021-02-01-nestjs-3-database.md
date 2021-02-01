---
layout: post
title: NestJS 블로그 만들기 - 데이터베이스 연결
categories: NestJS
---

# 2. NestJS 블로그 만들기 - 데이터베이스 연결 (Postgresql)과 User 모듈

---

> 저는 오늘 포스팅할 분량의 앱을 만든 후 블로그 포스팅하기 때문에 중간에 오류가 생길 수도 있습니다.
> 오류 내용과 함께 댓글을 달아주시면 저도 알아보겠습니다!!

## 👌 데이터 베이스 연결하기 !!

### PostgreSQL 설치!!

여러분 드디어 데이터베이스에 연결할 시간이 왔습니다!!.
실제 연습할 때는 배열 같은 임의 적인 놈을 만들고 나서 하긴하지만... 바로 연결해보죠!

저희는 Postgresql 을 사용할 겁니다!! 다른 데이터베이스를 사용하셔도 됩니다!!

> Postgresql 은 오픈소스 데이터베이스로 SQL 표준을 잘 지원합니다. 일단 무료입니다!!
> 설치하는 방법은 정식 문서나 타 블로그 포스트를 참조해주세요. [postgresql 설치방법](https://junlab.tistory.com/177)

편의를 위해 pgAdmin 툴을 이용하여 postgresql 을 제어하겠습니다.!!

기존의 서버 (PostgreSQL 13 이군요 저는) 를 우클릭하여 데이터베이스를 만듭시다!!
저는 데이터베이스 이름을 `nest_blog` 라고 했습니다!!

> 원하시는 서버를 만들고 데이터베이스를 생성하셔도 괜찮습니다.

데이터베이스의 스키마 구조에 대해서는 아직 정의하지 않겠습니다. NestJS가 해줄거거든요!!

### TypeORM !!

TypeORM 은 NodeJS 환경에서 사용할 수 있는 ORM (Object Relational Mapping) 라이브러리 입니다!!

> ORM 은 간단히 말해 Object 를 Database 스키마에 적절하게 적용시키게 해주는 기능이라 생각하면 편합니다.!!

설치 설치~ nestjs 루트 폴더에서 다음 명령어로 설치해주세요 !!

```sh
   $ npm install typeorm @nestjs/typeorm --save
```

설치가 됬으면 `ormconfig.json` 이라는 파일을 루트 폴더에 만들어 줍니다.
나중에 TypeORM 모듈이 이 파일을 참고해 데이터베이스에 연결을 시도합니다!!

다음과 같이 입력해주세요!!

```json
{
  "type": "postgres",
  "host": "localhost",
  "port": 5432,
  "username": "postgres",
  "password": 여러분이 설정했던 비밀번호!,
  "database": "nest_blog",
  "entities": ["dist/**/**.entity{.ts,.js}"],
  "synchronize": true
}
```

- `type` : 우리가 사용하게 될 데이터베이스 시스템을 나타냅니다.
- `host` : db 연결 주소입니다. 기본적으로 `localhost` 를 이용하고 db 를 다른 머신에서 실행한다면 그 머신에 접속하기 위한 주소로 변경해주시면 됩니다.
- `port` : db 연결 포트 입니다. 기본은 `5432` 입니다.
- `username` : 별 다른 설정을 안했다면 `postgres` 입니다
- `password` : 설치 과정에서 설정했던 비밀번호를 입력하세요.
- `database` : 위에서 만들었던 데이터베이스의 이름을 입력하시면 됩니다. 저는 `nest_blog` 라고 했습니다.
- `entities` : 반드시 `dist` 아래의 폴더로 지정해주세요. 안그러면 오류날 수도 있습니다. 이 설정의 경로에 있는 파일을 참고하여 DB 에서 스키마를 설정하게 됩니다.
- `synchronize` : 이 설정을 true 로 하시면 앱 작동시 DB 스키마가 자동으로 생성되게 됩니다.

> 자세한 내용은 [ormconfig 탐방하기!!](https://typeorm.io/#/using-ormconfig) 을 참조해주세요~

### app 모듈에서 import !! 그리고 실행!!

자 이제 `app.moudle.ts` 파일로 가서 TypeOrmMoudle 을 import 해줍시다!!

```typescript
@Module({
  imports: [UsersModule, TypeOrmModule.forRoot()],
  controllers: [AppController],
  providers: [AppService],
})
export class AppModule {}
```

`ormconfig.json` 파일을 생성하지 않았다면, forRoot 함수 안에 설정 내용을 적으셔야 합니다.!!
파일로 관리하는게 더 편하겠죠~?

자 이제 루트 폴더에서 다음과 같은 명령어를 수행해봅시다!

```sh
$ npm run start
```

별 다른 오류가 없다면 정상적으로 연결 된겁니다!! 우라하!!!
저희는 아직 Entity에 대해서 설정을 하지 않았기 때문에 테이블에 별 내용은 없습니다.

이후에 Entity 를 만든 후에는 DB 에서 테이블을 삭제하고 다시 연결해주시면 만든 내용이 적용됩니다!

## 🛴 User Entity 만들기.

톡.

DB 도 연결했겠다.

톡톡.

User Entity Template 도 생성했겠다.

톡톡.

내용만 넣으면 되네?

짝!

`src/users` 안의 구조를 다음과 같이 해주세요!!
spec 파일들은 지금 없어도 됩니다.

    users
    │  users.repository.ts
    │  users.controller.spec.ts
    │  users.controller.ts
    │  users.entity.ts
    │  users.module.ts
    │  users.service.spec.ts
    │  users.service.ts
    │
    └─dto
            create-user.dto.ts
            index.ts
            update-user.dto.ts

우리는 User 의 요구사항 맞게 적절히 Entity 를 설계해야 합니다. 왜냐면 이 안에 있는 내용이 데이터베이스 테이블 스키마로 적용될 녀석들이거든요!!

[요구사항보기](https://github.com/Tocktock/nest-practice)

바로 모든 요구사항을 만족시키기는 복잡하니 할 수 있는거 먼저 채워 나갑시다!!

`users.entity.ts` 안을 다음과 같이 채워주세요!!

```typescript
import { BeforeInsert, Column, Entity, PrimaryGeneratedColumn } from "typeorm";
import * as argon2 from "argon2";

@Entity("user")
export class UserEntity {
  @PrimaryGeneratedColumn()
  id: number;

  @Column({ length: 32 })
  username: string;

  @Column({ unique: true })
  email: string;

  @Column()
  password: string;

  @BeforeInsert()
  async hashPassword() {
    this.password = await argon2.hash(this.password);
  }

  @Column({ default: "" })
  imageLink: string;
}
```

- `@Entity` : 이 annotation 이 있으면 nestjs가 보고 있다가 DB 스키마 적용을 위해 참고하게 됩니다!! 이후 repository 클래스에서도 참고할 수 있는 클래스가 됩니다. 괄호안에 넣은 내용이 테이블의 이름이 됩니다.
- `PrimaryGeneratedColumn` : 이 annotion이 있다면 이 테이블은 해당 필드가 primary key 가 됩니다. 괄호 안에 아무런 내용을 넣지 않으면 id 는 auto increment 가 적용됩니다.
  > [uuid vs auto increment](https://velog.io/@qnfmtm666/series/DevTip)
- `Column` : 이 annotion 이 있으면 테이블의 필드로 만들어지게 됩니다. 괄호 안에 여러 옵션을 넣을 수 있습니다. [모든 괄호 안의 옵션 보기](https://typeorm.io/#/entities/column-options)
- `BeforeInsert` : 요 녀석은 데이터베이스에 insert 하기 전에 수행되는 녀석입니다. 비밀번호를 복호화 할 수 없게 hash 함수를 이용해 저장합시다.

아참 해쉬 함수를 쓰기 위해 argon2 를 설치해야 합니다.

```sh
$ npm install argon2 --save
```

## 🔨 Repository 와 Dto 변경하기!

### Repository

`Repository` 는 우리가 만든 Entity 를 관리(insert, update, delete, load, etc.)해줄 녀석이라고 보시면 됩니다.

`users.repository.ts` 안의 내용을 다음과 같이 채워주세요!!

```typescript
import { EntityRepository, Repository } from "typeorm";
import { UserEntity } from "./users.entity";

@EntityRepository(UserEntity)
export class UserRepository extends Repository<UserEntity> {}
```

엥? 이것만 해도 되는건가??

- 네!!

이렇게 Repository 를 만들어주시면 UserEntity에 대해 기본적인 쿼리를 그냥 쓸 수 있습니다.
복잡한 쿼리는 여기서 만들어주셔도 되고 이후 나올 query builder 로 해당 클래스에서 쓰셔도 됩니다!

### DTO

**DTO**(Data Transfer Object) 는 데이터가 어떤 구조로 전송되는지에 대한 정보를 담고 있는 클래스 입니다.

dto 폴더 안에
`create-user.dto.ts` 폴더에 다음과 같이 작성해주세요

```typescript
import { IsNotEmpty } from "class-validator";

export class CreateUserDto {
  @IsNotEmpty()
  readonly username: string;

  @IsNotEmpty()
  readonly email: string;

  @IsNotEmpty()
  readonly password: string;
}
```

`class-validator` 는 data 가 전송될 때 해당 필드가 적절한 유효성을 가지는지 검사해주는 라이브러리 입니다.

자 이제 Service 만 바꾸면 됩니다!!

## 🤗 User Service 변경하기!!

자 구조는 준비 되었습니다. 이제 로직만 잘 작성해주면 됩니다 화이팅!!

먼저 의존성 주입을 위해 UserService 생성자에 다음과 같이 적어줍시다!

```typescript
constructor(private readonly userRepository: UserRepository) {}
```

자 이것 만으로 객체가 주입됬습니드어어어!! 얼마나 좋아~!

### User create

`users.service.ts` 파일 내에 create 함수 안을 다음과 같이 바꿔주세요!

```typescript
  async create(createUserDto: CreateUserDto) {
    const { username, email, password } = createUserDto;
    const getByUserName = getRepository(UserEntity)
      .createQueryBuilder('user')
      .where('user.username = :username', { username });

    const byUserName = await getByUserName.getOne();
    if (byUserName) {
      const error = { username: 'UserName is already exists' };
      throw new HttpException(
        { message: 'Input data validation falied', error },
        HttpStatus.BAD_REQUEST,
      );
    }
    const getByEmail = getRepository(UserEntity)
      .createQueryBuilder('user')
      .where('user.email = :email', { email });

    const byEmail = await getByEmail.getOne();
    if (byEmail) {
      const error = { email: 'email is already exists' };
      throw new HttpException(
        { message: 'Input data validation falied', error },
        HttpStatus.BAD_REQUEST,
      );
    }
    // const thisUser = this.userRepository.findOne({ username: username });
    // const thisEmail = this.userRepository.findOne({ email: email });

    // create new user
    let newUser = new UserEntity();
    newUser.email = email;
    newUser.password = password;
    newUser.username = username;
    const validate_error = await validate(newUser);
    if (validate_error.length > 0) {
      const _error = { username: 'UserInput is not valid check type' };
      throw new HttpException(
        { message: 'Input data validation failed', _error },
        HttpStatus.BAD_REQUEST,
      );
    } else {
      return await this.userRepository.save(newUser);
    }
  }
```

먼저 username 과 email 은 유일해야 하기 때문에 이를 검사해보죠!!

먼저 살펴볼 것은 `createQueryBuilder` 입니다.
typeorm 은 `createQueryBuilder` 라는 함수를 통해 코드 안에서 SQL 문을 작성할 수 있게 해줍니다.
이 코드로 인해 작성된 sql 문은 바로 실행되는 것이 아니라 실질적으로 DB 와 데이터 교환이 일어나면 실행 됩니다.

맨 처음 만든 SQL 문은

```typescript
const byEmail = await getByEmail.getOne();
```

여기서 수행 됩니다. DB 의 쿼리 속도와 우리가 만든 백엔드 서버에서 코드를 실행하는 속도 차이가 많이 나기 때문에 비동기 식으로 수행했습니다.

마찬가지로 username 도 검사해줍시다!!

사실 이 기능은 createQueryBuilder 를 안써도 됩니다. Repository 를 작성했으므로 기본적인 기능은 이미 지원이 되기 때문입니다.
예들 들어 username 을 기준으로 가져오고 싶다면 다음과 같이 적으면 됩니다.

```typescript
const user = this.userRepository.findOne({ username: username });
```

이해를 돕고자 `createQueryBuilder` 를 사용했습니다

마찬가지로 findByEmail 함수를 다음과 같이 사용하시면

```typescript
  async findByEmail(email: string) {
    return await this.userRepository.findOne({ email });
  }
```

email 기준으로 유저를 찾을 수 있습니다!!

## 🔨 Module 에 import 해주기!!

자 거의 다 왔습니다!!

`users.module.ts` 파일 안에 imports 부분에 다음과 같이 모듈을 import 해줍시다!!

```typescript
@Module({
  imports: [TypeOrmModule.forFeature([UserRepository])],
  controllers: [UsersController],
  providers: [UsersService],
  exports: [UsersService],
})
export class UsersModule {}
```

## 😃 이제 실행된다!!

```sh
$ npm run start
```

위 명령어를 통해 어플리케이션을 실행을 합시다.
오류가 없다면 다음과 같이 로그가 뜹니다!!

    [Nest] 33080   - 2021-02-01 2:36:58 ├F10: PM┤   [NestFactory] Starting Nest application...
    [Nest] 33080   - 2021-02-01 2:36:58 ├F10: PM┤   [InstanceLoader] TypeOrmModule dependencies initialized +97ms
    [Nest] 33080   - 2021-02-01 2:36:58 ├F10: PM┤   [InstanceLoader] AppModule dependencies initialized +1ms
    [Nest] 33080   - 2021-02-01 2:36:58 ├F10: PM┤   [InstanceLoader] TypeOrmCoreModule dependencies initialized +213ms
    [Nest] 33080   - 2021-02-01 2:36:58 ├F10: PM┤   [InstanceLoader] TypeOrmModule dependencies initialized +1ms
    [Nest] 33080   - 2021-02-01 2:36:58 ├F10: PM┤   [InstanceLoader] UsersModule dependencies initialized +1ms
    [Nest] 33080   - 2021-02-01 2:36:58 ├F10: PM┤   [RoutesResolver] AppController {}: +14ms
    [Nest] 33080   - 2021-02-01 2:36:58 ├F10: PM┤   [RouterExplorer] Mapped {, GET} route +18ms
    [Nest] 33080   - 2021-02-01 2:36:58 ├F10: PM┤   [RoutesResolver] UsersController {/users}: +10ms
    [Nest] 33080   - 2021-02-01 2:36:58 ├F10: PM┤   [RouterExplorer] Mapped {/users, POST} route +7ms
    [Nest] 33080   - 2021-02-01 2:36:58 ├F10: PM┤   [RouterExplorer] Mapped {/users, GET} route +3ms
    [Nest] 33080   - 2021-02-01 2:36:58 ├F10: PM┤   [RouterExplorer] Mapped {/users/:email, GET} route +1ms
    [Nest] 33080   - 2021-02-01 2:36:58 ├F10: PM┤   [RouterExplorer] Mapped {/users/:id, PUT} route +11ms
    [Nest] 33080   - 2021-02-01 2:36:58 ├F10: PM┤   [RouterExplorer] Mapped {/users/:id, DELETE} route +1ms
    [Nest] 33080   - 2021-02-01 2:36:58 ├F10: PM┤   [NestApplication] Nest application successfully started +2ms

우후 우후~ 우후~ 우후~ 성공!!
고생하셨습니다.

## 🤣 아직 테스트가 남았다!!!

저는 Rest Client 라는 vscode extension 을 이용하여 테스트를 진행했습니다. postman, curl 여러분이 편하신 툴을 이용해주세요!!

자 다음과 같이 요청을 하면!

```http
    POST http://localhost:3000/users HTTP/1.1
    Content-Type: application/json

    {
        "username": "manynang",
        "email" : "nono@cat.co.kr",
        "password" : "manyang"
    }
```

다음과 같이 데이터가 출력이 됩니다!!

```http
    HTTP/1.1 201 Created
    X-Powered-By: Express
    Content-Type: application/json; charset=utf-8
    Content-Length: 179
    ETag: W/"b3-G/i5vHuN9KZDYAV9wTSwyMToetE"
    Date: Mon, 01 Feb 2021 05:41:10 GMT
    Connection: close

    {
    "email": "nono@cat.co.kr",
    "password": "$argon2i$v=19$m=4096,t=3,p=1$LthoEnjA4KlaeaE/8YhMPg$2bNUqzjlCqbomBtDTkcYzTHjibaSrjefgJDzJWTvGFQ",
    "username": "manynang",
    "id": 1,
    "imageLink": ""
    }
```

웁스 .. 비밀번호가 나오는군요... 이래서 테스트가 중요한겁니다.

저희는 유저 id만 가져오도록 하겠습니다.
UserCreate save 하는 부분을

```typescript
return await this.userRepository.save(newUser).then((v) => v.id);
```

이와 같이 바꿔줍시다.

```http
    HTTP/1.1 201 Created
    X-Powered-By: Express
    Content-Type: text/html; charset=utf-8
    Content-Length: 1
    ETag: W/"1-NWoZK3kTsExUV00Ywo1G5jlUKKs"
    Date: Mon, 01 Feb 2021 05:50:44 GMT
    Connection: close

    1
```

자 성공!

자 다시 위에 POST 관련 문을 다시 보내면?

```http
    HTTP/1.1 400 Bad Request
    X-Powered-By: Express
    Content-Type: application/json; charset=utf-8
    Content-Length: 92
    ETag: W/"5c-j/u2GjtMeXEpPJw+5WWgYELKwpM"
    Date: Mon, 01 Feb 2021 05:54:56 GMT
    Connection: close

    {
    "message": "Input data validation falied",
    "error": {
        "username": "UserName is already exists"
    }
    }
```

성공~~!!!!
중복된 username 을 걸렀습니다 ㅜㅜ!!

---

고생했습니다 ㅜㅜ!!!!

다음에는 위 코드를 Refactor 하는 과정으로 찾아뵙도록 하겠습니다!!
오늘도 즐거운 하루 보내세요!!

피드백은 항상 환영입니다.

# MongoDB

## 1. MongoDB 준비하기

- Document : MongoDB에 저장하는 데이터 (객체 같은 것)
- Collection : Document 모음

### 1-1. MongoDB Atlas
MongoDB 만드는 회사에서 운영하는 클라우드 서비스  
[MongoDB Atlas 사용법](https://www.codeit.kr/tutorials/70/mongodb-atlas)

### 1-2.Mongoose
MongoDB에서 공식적으로 제공하는 라이브러리는 npm의 mongodb 패키지이다.  
그러나 굉장히 로우 레벨로 구현되어 있어 번거롭다. 그래서 추상화된 라이브러리를 주로 사용한다.  
Mongoose 라이브러리는 쉽고 편리하기 때문에 JS 개발자들이 가장 많이 사용하는 라이브러리다.  

    # install
    $ npm install mongoose

### 1-3. Next.js에서 환경변수 사용하기

#### 환경변수
우리가 평소 사용하는 서비스는 보통 서버 하나, 데이터베이스 하나로 실행되지 않는다.  
수천 명, 수백만 명이 사용하기 때문에 서버와 데이터베이스도 그에 맞게 개수가 많다.  
그런데 하나의 코드로 실행하는데 수많은 서버와 데이터베이스를 어떻게 연결할까? 

이럴 때 사용하는게 환경변수다. 코드 상에는 **MONGODB_URI**와 같은 값으로  
데이터베이스 주소를 지정해 두고, 각 서버를 실행할 때마다 다른 데이터베이스 주소를 넣어 준다.  
환경 변수는 프로그램에서 실행 환경에 따라 다른 값을 지정할 수 있는 변수다.  

서버와 데이터베이스를 여러 개 쓰는 경우가 아니더라도 데이터베이스 주소와 같은 값을 소스코드에 그대로 쓰는 것은 위험하다.  
반드시 환경 변수로 사용하는 것이 좋다. Node.js환경에서는 이런 환경 변수들을 process.env라는 객체를 통해서 참조할 수 있다.

#### Next.js에서 환경 변수 추가하기
Next.js에서는 기본적으로 dotenv라는 라이브러리를 지원한다.  
이 라이브러리는 .env 같은 이름의 파일에서 환경 변수들을 저장해 두면, Node.js프로젝트를 실행할 때 환경 변수로 지정해주는 라이브러리이다.  
이때 주의할 점은 .env 파일 같은 건 소스코드에 포함시키면 안 된다.  
Next.js 프로젝트에서는 기본적으로 dotenv 설정이 되어 있어서, .env.local 같은 파일을 추가하면 손쉽게 환경 변수를 추가할 수 있다.  

    # @/.env.local
    MONGODB_URI=mongodb+srv://admin:blahblah@.clusterName.blahblah.mongodb.net/databaseName?retryWrites=true&w=majority

    // 추가한 값을 process.env.MONGODB_URI로 참조할 수 있게된다.
    # pages/api/short-links/index.js
    export default function handler(req, res) {
    const DB_URI = process.env.MONGODB_URI;
    // 데이터베이스 접속 ...
  }

#### Next.js에서 사용하는 특별한 환경 변수
위에서 추가한 데이터베이스 주소는 유저의 아이디와 비밀번호를 포함한 아주 민감한 정보이다.  
그런데 실수로 이 환경 변수가 웹 사이트에 노출되면 안된다.  
이를 방지하고자 Next.js에서는 클라이언트 사이드에서 사용하는 환경 변수에 특별한 접두사(prefix)를 사용한다.  
**NEXT_PUBLIC_** 이라고 이름을 붙이면 이 환경 변수는 클라이언트 사이드에서도 사용할 수 있다.  

    MONGODB_URI=mongodb+srv://admin:blahblah@cluster0.blahblah.mongodb.net/databaseName?retryWrites=true&w=majority
NEXT_PUBLIC_HOST=http://localhost:3000
        
    export default Home() {
      // 페이지 컴포넌트에서는 아래와 같이 사용
      return (
        <>호스트 주소: {process.env.NEXT_PUBLIC_HOST}</>
      );

## 2. Mongoose 문법 정리
[Mongoose의 Model 문서](https://mongoosejs.com/docs/api/model.html)

### 2-1 데이터베이스 연동하기

### 2-2. 모델 만들기

### 2-3. 모델 다루기

#### 생성 : Model.create()

#### 여러 개 조회 : Model.find()

#### 아이디로 하나만 조회 : Model.findById()

#### 아이디로 업데이트하기 : Model.findByIdAndUpdate()

#### 아이디로 삭제하기 : Model.findByIdAndDelete()

### 2-4. 기타

#### 조건으로 조회하기

#### 조건으로 업데이트하기

#### 조건으로 삭제하기

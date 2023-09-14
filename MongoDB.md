# MongoDB

## 1. MongoDB 설치

#### Linux
[ref]([https://jjeongil.tistory.com/2031](https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-ubuntu/#std-label-install-mdb-community-ubuntu)

    $ sudo apt-get install gnupg curl
    $ curl -fsSL https://pgp.mongodb.com/server-7.0.asc | \
   sudo gpg -o /usr/share/keyrings/mongodb-server-7.0.gpg \
   --dearmor
    $ echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-7.0.gpg ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/7.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-7.0.list
    $ sudo apt-get update
    # 최신버전 설치
    $ sudo apt-get install -y mongodb-org
    # 특정버전 설치
    $ sudo apt-get install -y mongodb-org=7.0.1 mongodb-org-database=7.0.1 mongodb-org-server=7.0.1 mongodb-mongosh=7.0.1 mongodb-org-mongos=7.0.1 mongodb-org-tools=7.0.1
    # 설치 확인
    $ mongod --version
    
    # 시작하기
    $ sudo systemctl start mongod
    $ sudo systemctl status mongod
    # 종료하기
    $ sudo systemctl stop mongod 

### 1-1. MongoDB 구성
- NoSQL : 미리 정의된 스키마가 필요하지 않으며, 시간이 지남에 따라 데이터 구조 변경 가능 
- Document : MongoDB에 저장하는 데이터 (객체 같은 것)
- Collection : Document 모음
######
MongoDB 구성 파일의 이름은 mongod.conf이며 형식은 YAML이고 /etc 디렉토리에 있다.  


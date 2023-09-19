# Migrate to Flask

## 목차

-   필수 라이브러리 설치
-   Flask 어플리케이션 설정
-   데이터 마이그레이션

<hr>

## 1. 필수 라이브러리 설치

#### proejectDirectory

    $ pip install Flask-PyMongo

## 2. Flask 어플리케이션 설정

#### app.py

아래 코드에서 'mongodb://localhost:27017/your_database_name'은  
MongoDB 서버의 주소 및 데이터베이스 이름에 맞게 수정

    from flask import Flask
    from flask_pymongo import PyMongo

    app = Flask(__name__)

    app.config['MONGO_URI'] = 'mongodb://localhost:27017/your_database_name'
    mongo = PyMongo(app)

## 3. 데이터 마이그레이션

필요한 데이터를 Python 코드로 로드하고 MongoDB에 삽입  
이 코드는 /migrate_data 엔드포인트로 접속하면 데이터를 MongoDB에 마이그레이션하는 코드

    from flask import Flask
    from flask_pymongo import PyMongo

    app = Flask(__name__)

    app.config['MONGO_URI'] = 'mongodb://localhost:27017/your_database_name'
    mongo = PyMongo(app)

    @app.route('/migrate_data')
    def migrate_data():
        data_to_migrate = [
            {
                "name": "John",
                "age": 30,
                "city": "New York"
            },
            {
                "name": "Alice",
                "age": 25,
                "city": "Los Angeles"
            },
            {
                "name": "Bob",
                "age": 35,
                "city": "Chicago"
            }
        ]

        # MongoDB 컬렉션에 데이터 삽입
        mongo.db.your_collection_name.insert_many(data_to_migrate)

        return 'Data migration complete'

    if __name__ == '__main__':
        app.run()

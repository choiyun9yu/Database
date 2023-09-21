# Migrate to Flask

## 1. 필수 라이브러리 설치

#### proejectDirectory

    % pip install Flask-PyMongo
    % pip install pipreqs
    % pipreqs [경로]

## 2. 레거시 프로젝트

### 2-1. Project Architecture

    kisa-prediction-service/
    ├── app/
    │   ├── __init__.py
    │   ├── routes.py
    │   └── models.py
    ├── config.py
    ├── run.py
    └── requirements.txt

### 2-2. Dependency management

    % pip freeze > requirements.txt

    % pip install -r requirements.txt

### 2-3. CODE

#### run.py

    from app import app

    if __name__ == '__main__':
        app.run(port=5000, debug=True)

#### config.py

    class Config:
    MONGO_URI = 'mongodb://localhost:27017/[DatabaseName]'

#### app/**init**.py

    from flask import Flask

    from config import Config
    from .models import mongo
    from .routes import api_blueprint

    def create_app():
        app = Flask(__name__)
        app.config.from_object(Config)
        mongo.init_app(app)
        app.register_blueprint(api_blueprint)

        return app

    app = create_app()

#### app/routes.py

    from flask import jsonify, Blueprint, request

    from .models import Data

    api_blueprint = Blueprint('api', __name__)

    @api_blueprint.route('/api/data', methods=['GET', 'POST'])
    def data_page():
        if request.method == 'GET':
            data = Data.get_drones()
            return jsonify({"ai_drones": drones})
        else:
            # post 로직

#### app/models.py

    from flask_pymongo import PyMongo

    mongo = PyMongo()

    class Data:
        @staticmethod
        def get_data():
            cursor = mongo.db.[collectionName].find() 
            find_list = list(ai_drones_cursor)
            # PyMongo를 사용할 경우 커서 따로 닫아줄 필요 없음
            return find_list

## 3. PyMongo 문법

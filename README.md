# SQL

## MariaDB 설치
  - brew install mariadb (안되면 arch -arm64 brew install mariadb)
  - 동작 : brew services start mariadb
  - 중지 : brew services stop mariadb 
  - 접속 : mariadb -h호스트명 -u계정명 -p패스워드 DB명
          (root 계정 접속 : mariadb -uroot -p)
  - 관리 : SHOW databases;
          CREAT database DB이름;
          DROP database DB이름;
          USE DB이름;
    

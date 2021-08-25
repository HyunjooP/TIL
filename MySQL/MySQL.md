# MySQL



## 설치



- 사전 준비

MobaXterm 설치 https://mobaxterm.mobatek.net/download-home-edition.html

하이디sqp 설치 https://www.heidisql.com/download.php

오라클 클라우드 계정 생성

mcuser Mysql11!

MySQL 참고 https://www.w3schools.com/mysql/mysql_limit.asp  

colab에서 사용 시 설치

```
!pip install pymysql > /dev/null
```



부팅 후 moba에 들어와서 ip4mysql 실행(HeidiSQL 접속이 가능해짐)

```
sudo ./ip4mysql
```



```
echo iptables -I INPUT 5 -i ens3 -p tcp --dport 3306 -m state --state NEW,ESTABLISHED -j ACCEPT > ip4mysql
```





## 데이터 조작

- 실행 시에 F9



- 기본 명령어 

| SHOW   | 테이블, 데이터 조회 |
| ------ | ------------------- |
| CREATE | 테이블 생성         |
| SELECT | 테이블, 데이터 조회 |
| INSERT | 레코드 삽입         |
| UPDATE | 데이터 업데이트     |
| DELETE | 레코드 삭제         |
| DROP   | 데이터 삭제         |
| ALTER  | 정보를 수정         |

- distinct 중복제외



- 데이터 조작

| WHERE        | 조건 설정<br />select * from city where countrycode='kor';   |
| ------------ | ------------------------------------------------------------ |
| 범위설정     | select * from city where district='kyonggi' and population>500000; |
| ORDER BY     | 정렬 조건 입력<br />ASC : 오름차순, DESC: 내림차순<br />select * from city where district='kyonggi' order by name desc; |
| COUNT        | 데이터의 개수<br />select count(*) from city where countrycode='kor'; |
| SUM          | 데이터의 합계<br />select sum(population) from city where countrycode='kor'; |
| AVG          | 데이터의 평균<br />select avg(population) from city where countrycode='kor'; |
| MAX          | 데이터의 MAX값<br />select max(population) from city;        |
| MIN          | 데이터의 MIN값<br />select min(population) from city;        |
| group_concat | 그룹으로 보기<br />select group_concat(name) from city where district='chungchongnam'; |
| group by     | <br />select * from city where countrycode='kor' group by district; |
| date_format  | date_format(dt, '%Y-%m-%d')                                  |
|              |                                                              |
|              |                                                              |
|              |                                                              |
|              |                                                              |





### 테이블 조작

```
create table if not exists address_book (
no int unsigned not null auto_increment,
`name` varchar(10) not null,
tel varchar(14),
nickname varchar(20) default ‘별명’,
primary key(no)
) auto_increment=10001;
desc address_book;
```

- if not exists : 없으면 만들기

- desc: 구조확인

| Field    | Type         | Null | Key  | Default | Extra          |
| -------- | ------------ | ---- | ---- | ------- | -------------- |
| no       | int unsigned | NO   | PRI  | (NULL)  | auto_increment |
| name     | varchar(20)  | NO   |      | (NULL)  |                |
| tel      | varchar(20)  | YES  |      | (NULL)  |                |
| nickname | varchar(20)  | YES  |      | 별명    |                |

- drop: 제거

- RENAME: 이름변경



- alter table: 테이블 변경
  - add: 컬럼 추가
  - drop: 컬럼 삭제
  - change: 컬럼명 변경, 컬럼 자료형 변경
  - modify: 컬럼 순서 바꾸기

- TRUNCATE: 테이블의 모든 row 삭제



### 데이터 타입

| CHAR( )    | 0 to 255 고정문자 길이   |
| ---------- | ------------------------ |
| VARCHAR( ) | 0~65535 가변 문자 길이   |
| TINYTEXT   | 최대 255 문자길이        |
| TEXT       | 최대 65535 문자길이      |
| BLOB       | 최대 65535 문자길이      |
| MEDIUMTEXT | 최대 16777215 문자길이   |
| MEDIUMBLOB | 최대 16777215 문자길이   |
| LONGTEXT   | 최대 4294967295 문자길이 |
| LONGBLOB   | 최대 4294967295 문자길이 |









### 파이썬에서 사용 시

```
{
	"host": "168.138.102.132", 
	"user": "mcuser", 
	"password": 
	"Mysql11!", 
	"database": 
	"mcdb", 
	"port": 3306 
}
```

json 파일로 생성하여 업로드하여 사용




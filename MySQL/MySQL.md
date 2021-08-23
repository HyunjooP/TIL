# MySQL



- 사전 준비

MobaXterm 설치 https://mobaxterm.mobatek.net/download-home-edition.html

하이디sqp 설치 https://www.heidisql.com/download.php

오라클 클라우드 계정 생성

mcuser Mysql11!



colab에서 사용 시 설치

```
!pip install pymysql > /dev/null
```



부팅 후 moba에 들어와서 

```
sudo ./ip4mysql
```



```
echo iptables -I INPUT 5 -i ens3 -p tcp --dport 3306 -m state --state NEW,ESTABLISHED -j ACCEPT > ip4mysql
```






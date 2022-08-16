# 2.Setting Up NGINX with Node.js

<br>

## Node.js & npm 설치

```
sudo apt-get install nodejs
sudo apt-get install npm
```

## 테스트환경 구성

```
npm install -g express-generator
express [디렉토리명]
cd [디렉토리명]
npm install
```

## NGINX 환경설정

```
sudo vi /etc/nginx/sites-available/[파일명]
```

### 코드입력

```
server {
    listen 80;
    server_name [도메인주소]; 
    
    #도메인이 없을때 '_' 로 대체한다. 
    #요청이 들어오면 아래의 proxy_pass [외부ip]로 포워딩한다.
    
    location / {
      proxy_set_header X-Real-IP $remote_addr;
      proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
      proxy_set_header Host $http_host;
      proxy_set_header X-NginX-Proxy true;
      proxy_pass [외부ip]; 
      proxy_redirect off;
    }
    gzip on;
    gzip_comp_level 2;
    gzip_proxied any;
    gzip_min_length 1000;
    gzip_disable "MSIE [1-6]\."
    gzip_types text/plain text/css application/json 
               application/x-javascript text/xml application/xml 
               application/xml+rss text/javascript;
 }
```

### 링크연결

```
ln -s /etc/nginx/sites-available/[파일명] /etc/nginx/sites-enabled/[파일명]
```

### nginx.conf 수정

```
sudo vi /etc/nginx/nginx.conf
```

```
##
# Virtual Host Configs
##

include /etc/nginx/conf.d/*.conf;
include /etc/nginx/sites-enabled/*; -> include /etc/nginx/sites-available/[파일명];

#다중도메인 활용시 *로 변경한다.
```

## NGINX 재시작

```
sudo service nginx reload
or
sudo /etc/init.d/nginx restart
```

## 테스트실행

```
cd ~/[디렉토리명]
npm start
```

## 브라우저에서 확인

```
[외부ip]
```

## +
https를 사용하여 연결시 ```Connection Refused```오류를 반환된다.

<p>

출처 ```https://deokisys.github.io/```

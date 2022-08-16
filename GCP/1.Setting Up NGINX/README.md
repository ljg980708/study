# 1. Setting Up NGINX
## 인스턴스 생성
Compute Engine에서 VM 인스턴스를 생성한다.

## NGINX 설치

```
sudo apt-get update
sudo apt-get install nginx

```
## NGINX 기동확인

```
systemctl status nginx
```

## 브라우저에서 확인

```
[외부ip]
```

## +
https를 사용하여 연결시 ```Connection Refused```오류를 반환된다.

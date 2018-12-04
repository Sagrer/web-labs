# Лабораторная работа №1.

## Запрос OPTIONS

Он нужен чтобы запросить у web-сервера его возможности (заголовок Allow), а также может использоваться для проверки вообще работоспособности сервера и для проверки поддержки HTTP 1.1.

Запросы на указанные в задании сервера дали следующие результаты:

### http://mail.ru​

Сервер ответил без тела, только заголовками:
```
HTTP/1.1 400
status: 400
Server: nginx/1.14.1
Date: Tue, 04 Dec 2018 16:43:46 GMT
Content-Type: text/html
Transfer-Encoding: chunked
Connection: keep-alive
X-XSS-Protection: 1; mode=block; report=https://cspreport.mail.ru/xxssprotection
X-Content-Type-Options: nosniff
```

### http://ya.ru
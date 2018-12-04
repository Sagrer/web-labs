# Лабораторная работа №1.

## Запрос OPTIONS

Он нужен чтобы запросить у web-сервера его возможности (заголовок Allow), а также может использоваться для проверки вообще работоспособности сервера и для проверки поддержки HTTP 1.1.

Запросы на указанные в задании сервера дали следующие результаты:

### mail.ru​

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

### ya.ru

Сервер ответил 403 ошибкой с web-страницей и вот такими заголовками:
```
HTTP/1.1 403
status: 403
Date: Tue, 04 Dec 2018 16:50:48 GMT
Content-Type: text/html; charset=utf-8
ETag: W/"5c056e6e-3077"
Content-Encoding: gzip
X-Content-Type-Options: nosniff
Transfer-Encoding: chunked
```

### www.rambler.ru

Сервер ответил 403 ошибкой с web-страницей, в которой из осмысленного текста было:
```
Доступ запрещен
Поздравляем, вы нашли тайную дверь.
Но дальше вы пройти не сможете.
```
Заголовки ответа:
```
HTTP/1.1 403
status: 403
Server: nginx
Date: Tue, 04 Dec 2018 16:55:07 GMT
Content-Type: text/html; charset=utf-8
Transfer-Encoding: chunked
Connection: keep-alive
Keep-Alive: timeout=50
Last-Modified: Tue, 02 Oct 2018 09:42:09 GMT
Vary: Accept-Encoding
ETag: W/"5bb33d71-2a20"
Content-Encoding: gzip
X-Cache: HIT
```

### www.google.ru

Ответил веб-страницей:
```
405. That’s an error.

The request method OPTIONS is inappropriate for the URL.
That’s all we know.
```
Заголовки ответа при этом содержат и Allow (в котором нет OPTIONS):
```
HTTP/1.1 405
status: 405
Allow: GET, HEAD
Date: Tue, 04 Dec 2018 16:59:40 GMT
Content-Type: text/html; charset=UTF-8
Server: gws
Content-Length: 1592
X-XSS-Protection: 1; mode=block
X-Frame-Options: SAMEORIGIN
Alt-Svc: quic=":443"; ma=2592000; v="44,43,39,35"
```

### github.com

Ответил пустой (только картинка и строка поиска) страницей с 404 ошибкой:
```
HTTP/1.1 404
status: 404
Server: GitHub.com
Date: Tue, 04 Dec 2018 17:03:22 GMT
Content-Type: text/html; charset=utf-8
Transfer-Encoding: chunked
Status: 404 Not Found
X-Request-Id: 892eb494-cc87-4fd4-87e4-4a107c28b643
Strict-Transport-Security: max-age=31536000; includeSubdomains; preload
X-Frame-Options: deny
X-Content-Type-Options: nosniff
X-XSS-Protection: 1; mode=block
Referrer-Policy: origin-when-cross-origin, strict-origin-when-cross-origin
Expect-CT: max-age=2592000, report-uri="https://api.github.com/_private/browser/errors"
Content-Security-Policy: default-src 'none'; base-uri 'self'; block-all-mixed-content; connect-src 'self' uploads.github.com status.github.com collector.githubapp.com api.github.com www.google-analytics.com github-cloud.s3.amazonaws.com github-production-repository-file-5c1aeb.s3.amazonaws.com github-production-upload-manifest-file-7fdce7.s3.amazonaws.com github-production-user-asset-6210df.s3.amazonaws.com; font-src assets-cdn.github.com; form-action 'self' github.com gist.github.com; frame-ancestors 'none'; frame-src render.githubusercontent.com; img-src 'self' data: assets-cdn.github.com media.githubusercontent.com camo.githubusercontent.com identicons.github.com collector.githubapp.com avatars0.githubusercontent.com avatars1.githubusercontent.com avatars2.githubusercontent.com avatars3.githubusercontent.com github-cloud.s3.amazonaws.com; manifest-src 'self'; media-src 'none'; script-src assets-cdn.github.com; style-src 'unsafe-inline' assets-cdn.github.com
Content-Encoding: gzip
X-GitHub-Request-Id: C4D7:39C7:3AFEFA8:68BAC0E:5C06B34A
```

### www.apple.com

Единственный из предложенных адресов, на котором сервер ответил кодом 200 и без web-страницы. Заголовки ответа (Allow присутствует):
```
HTTP/1.1 200
status: 200
Server: Apache
Content-Length: 0
Content-Type: text/html; charset=UTF-8
Set-Cookie: geo=RU; path=/; domain=.apple.com
Set-Cookie: ccl=dMpRkhZznRY80wWmdMTz9w==; path=/; domain=.apple.com
X-Frame-Options: SAMEORIGIN
X-Content-Type-Options: nosniff
Allow: GET,HEAD,POST,OPTIONS
X-Xss-Protection: 1; mode=block
Cache-Control: max-age=245
Expires: Tue, 04 Dec 2018 17:09:47 GMT
Date: Tue, 04 Dec 2018 17:05:42 GMT
Connection: keep-alive
```

## Запрос HEAD

Он делает то же самое, что и GET (т.е. пытается получить некий контент по некоему адресу), но при этом ожидается, что сервер ответит только HTTP-заголовками, без тела ответа.

Может использоваться например чтобы проверить существует ли контент по данному адресу и не менялся ли он.

### vk.com

Сервер ответил шуточным кодом 418 (сообщающим о том, что отправитель является чайником). Заголовки не совпадают с заголовками, которые были бы при запросе GET:
```
HTTP/1.1 418
status: 418
Server: Internet Information Services
Date: Tue, 04 Dec 2018 17:12:14 GMT
Content-Length: 0
Connection: keep-alive
X-Frontend: front623307
Access-Control-Expose-Headers: X-Frontend
```

### www.apple.com

Сервер отвечает примерно так же, как и при GET-запросе, но без тела ответа:
```
HTTP/1.1 200
status: 200
Server: Apache
X-Frame-Options: SAMEORIGIN
X-Xss-Protection: 1; mode=block
Accept-Ranges: bytes
X-Content-Type-Options: nosniff
Content-Type: text/html; charset=UTF-8
Vary: Accept-Encoding
Content-Encoding: gzip
Cache-Control: max-age=110
Expires: Tue, 04 Dec 2018 17:22:59 GMT
Date: Tue, 04 Dec 2018 17:21:09 GMT
Content-Length: 7782
Connection: keep-alive
```

### www.msn.com

Отвечает с множеством нестандартных X- заголовков, так же как и при GET-запросе, но без тела ответа:
```
HTTP/1.1 200
status: 200
Cache-Control: no-cache, no-store, no-transform
Pragma: no-cache
Content-Length: 15992
Content-Type: text/html; charset=utf-8
Content-Encoding: gzip
Expires: -1
Vary: User-Agent
Access-Control-Allow-Origin: *
X-AspNetMvc-Version: 5.2
X-AppVersion: 20181127_13106485
X-Activity-Id: fafebab0-2343-49c7-ac1b-81f44d6666c8
X-Az: {did:b24a0ea2b3ba45a59fc1d4d299c5ebc1, rid: 10, sn: neurope-prod-hp, dt: 2018-11-16T19:18:05.9146076Z, bt: 2018-11-28T00:44:45.7655816Z}
Content-Security-Policy: default-src 'self' data: 'unsafe-inline' 'unsafe-eval' https: blob:; media-src 'self' https: blob:; worker-src 'self' https: blob:; block-all-mixed-content; connect-src 'self' data: 'unsafe-inline' 'unsafe-eval' https: blob: https://*.trouter.io:443 https://*.trouter.skype.com:443 wss://*.trouter.io:443 wss://*.trouter.skype.com:443;
X-UA-Compatible: IE=Edge;chrome=1
X-Content-Type-Options: nosniff
X-FRAME-OPTIONS: SAMEORIGIN
X-Powered-By: ASP.NET
Access-Control-Allow-Methods: HEAD,GET,OPTIONS
X-XSS-Protection: 1
X-MSEdge-Ref: Ref A: FAFEBAB0234349C7AC1B81F44D6666C8 Ref B: AMBEDGE0422 Ref C: 2018-12-04T17:22:53Z
Date: Tue, 04 Dec 2018 17:22:53 GMT
```

## GET-запрос
Нужен для запроса у сервера содержимого, размещённого по данному адресу. Также может использоваться для передачи серверу каких-либо данных в параметрах запроса (после символа ?).

Запросы на google.com, yandex.ru, apple.com вернули код 200 и главные страницы этих сайтов.

## POST-запорос
Используется для передачи неких данных на сервер в теле запроса (после пустой строки после заголовков). Обычно используется для передачи каких-либо серьёзных по объёму данных, которые неудобно или невозможно передать через GET-запрос, например при загрузке файлов или при отправке сообщения на форум.

На сервера отсылался POST-запрос с телом "test". Вот что из этого вышло:

### apple.com
Ответил теми же заголовками (с кодом ответа 200) и web-страницей, что и при GET-запроса.

### vk.com
То же самое, отвечает как будто на GET-запрос.

### google.com
Тут уже пришёл ответ что я делаю что-то не то и что так нельзя (method not allowed):
```
HTTP/1.1 405
status: 405
Allow: GET, HEAD
Date: Tue, 04 Dec 2018 17:34:43 GMT
Content-Type: text/html; charset=UTF-8
Server: gws
Content-Length: 1589
X-XSS-Protection: 1; mode=block
X-Frame-Options: SAMEORIGIN
```

### yandex.ru
Тоже ошибка, на этот раз 403:
```
HTTP/1.1 403
status: 403
Date: Tue, 04 Dec 2018 17:35:24 GMT
Content-Type: text/html; charset=utf-8
ETag: W/"5c06a2a3-3077"
Content-Encoding: gzip
X-Content-Type-Options: nosniff
Transfer-Encoding: chunked
```

## Работа с API VK.

Было зарегистрировано приложение, получен token доступа.

Затем для получения идентификатора МГТУ выполнен примерно следующий запрос:
```
https://api.vk.com/method/database.getUniversities?v=5.92&access_token=TOKEN&q=МГТУ
```
Получен ответ, содержащий, в частности, вот это:
```
{
	"id": 250,
	"title": "МГТУ им. Н. Э. Баумана"
}
```
Затем выполнен такой запрос:
```
https://api.vk.com/method/database.getFaculties?v=5.92&access_token=TOKEN&university_id=250
```
Ответ:
```
{
    "response": {
        "count": 20,
        "items": [
            {
                "id": 1031,
                "title": "Аэрокосмический факультет"
            },
            {
                "id": 1032,
                "title": "Факультет инженерного бизнеса и менеджмента"
            },
            {
                "id": 1033,
                "title": "Факультет информатики и систем управления"
            },
            {
                "id": 1034,
                "title": "Факультет машиностроительных технологий"
            },
            {
                "id": 1035,
                "title": "Факультет оптико-электронного приборостроения"
            },
            {
                "id": 1036,
                "title": "Приборостроительный факультет"
            },
            {
                "id": 1037,
                "title": "Радиотехнический факультет"
            },
            {
                "id": 1038,
                "title": "Факультет радиоэлектроники и лазерной техники"
            },
            {
                "id": 1039,
                "title": "Факультет ракетно-космической техники"
            },
            {
                "id": 1040,
                "title": "Факультет робототехники и комплексной автоматизации"
            },
            {
                "id": 1041,
                "title": "Факультет специального машиностроения"
            },
            {
                "id": 1042,
                "title": "Факультет фундаментальных наук"
            },
            {
                "id": 1043,
                "title": "Факультет энергомашиностроения"
            },
            {
                "id": 1044,
                "title": "Кафедра юриспруденции, интеллектуальной собственности и судебной экспертизы"
            },
            {
                "id": 1803,
                "title": "Факультет биомедицинской техники"
            },
            {
                "id": 1804,
                "title": "Факультет социально-гуманитарных наук"
            },
            {
                "id": 56430,
                "title": "Факультет лингвистики"
            },
            {
                "id": 56431,
                "title": "Физкультурно-оздоровительный факультет"
            },
            {
                "id": 2071503,
                "title": "Головной учебно-исследовательский и методический центр (ГУИМЦ)"
            },
            {
                "id": 2183736,
                "title": "Факультет военного обучения (Военный институт)"
            }
        ]
    }
}
```
Для получения своей аватарки выполнен следующий запрос:
```
https://api.vk.com/method/users.get?v=5.92&access_token=TOKEN&fields=photo_50
```
Получен ответ:
```
{
    "response": [
        {
            "id": 47355401,
            "first_name": "Александр",
            "last_name": "Гриднев",
            "is_closed": false,
            "can_access_closed": true,
            "photo_50": "https://pp.userapi.com/c4132/u47355401/e_d2110c13.jpg?ava=1"
        }
    ]
}
```
В ответе есть ссылка на изображение.

## Ответы на вопросы про использование API:

#### "какой код ответа присылается от api?"
200 OK если запрос составлен корректно. Даже в случае ошибки при выполнении запроса (например токен не даёт необходимых прав) - возвращается код 200, а информация об ошибке содержится в возвращённом JSON.
#### "Что содержит тело ответа? В каком формате и какой кодировке содержаться данные?"
Ответ содержит текст в кодировке utf-8 и в формате JSON с некоторым количеством полей, из которых можно взять интересовавшую при выполнении запроса информацию.
#### "Какой веб-сервер отвечает на запросы?"
Если верить заголовкам, то это Internet Information Services, во что на самом деле слабо верится.
#### "Какая версия протокола HTTP используется?"
HTTP/1.1

## Отправка сообщения на стену через POST-запрос.

Выполнен запрос:
```
POST /method/wall.post
User-Agent: PostmanRuntime/7.4.0
Accept: */*
Host: api.vk.com
content-type: multipart/form-data; 
content-length: 512

v=5.92
access_token=TOKEN
message=Тестовое сообщение через API
```
Получен ответ:
```
{
    "response": {
        "post_id": 176
    }
}
```
Сообщение действительно появилось на стене моего аккаунта.
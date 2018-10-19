# Как работает WEB

- Что такое интернет
- Сервер и клиент
- Статические сайты VS Динамические

# HTTP protocol (Hypertext Transfer Protocol )

### Основной протокол Web

Стандартизирован в 1997 году - версия HTTP 1.1 - [текст стандарта](https://tools.ietf.org/html/rfc2068)

HTTP 2.0  - обновленная в 2015 году версия протокола (спасибо Google) -   [Текст стандарта](https://tools.ietf.org/html/rfc7540)



## URL
Uniform Resource Locator - унифицированный указатель [местонахождения информационного] ресурса. с его помощью определяется сервер и ресурс с которым мы хотим наладить обмен сообщениями.

*Более подробно читайте "Введение в изучение и использование DNS-записей" - ссылка в приложении*

### Структура URL


![](http1-url-structure.png)

```
http://google.com:80/search?q=facebook#result
```

- `google.comk` - хост
- `?q=facebook` - параметр
- `#bottom` - фрагмент

Типичные порты для протокола:  **80**/ **8080** - [http] и **443** - [https]

Но не всегда =)
```
php -S localhost:8000
```

# Основные методы:

- [Документация](https://tools.ietf.org/html/rfc2068#section-5.1.1)

Наиболее часто используемый - **GET**
Запрашивает данные с сервера. По сути *ReadOnly*

```
GET / HTTP /1.1
Host: yandex.ru
```

Типичный запрос браузера:

```
GET / HTTP /1.1
Host: yandex.ru
User-Agent: Mozilla/5.0 (Windows; U; Windows NT 6.1; en-US; rv:1.9.1.5) Gecko/20091102 Firefox/3.5.5 (.NET CLR 3.5.30729)
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
```

`Практика - открыть Chrome Dev Tools -  открыть Github.`


Может использоваться в формах для отправки данных

*например фильтр товаров на сайте*

```
<form method="GET" action="foo.php">

First Name: <input type="text" name="first_name" /> <br />
Last Name: <input type="text" name="last_name" /> <br />

<input type="submit" name="action" value="Submit" />

</form>
```
В таком случае запрос будет выглядеть:
```
GET /foo.php?first_name=John&last_name=Doe&action=Submit HTTP/1.1
```


---

Метод POST

основной метод для отправки данных на сервер (формы)

Наиболее часто используется в формах
данные отправляются на сервер, где его принимает обработчик
множественный POST может создать множество обьектов

```
POST /foo.php HTTP/1.1
Host: localhost
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Referer: http://localhost/test.php
Content-Type: application/x-www-form-urlencoded
Content-Length: 43

foo=bar
```

---

Метод PUT
для *обновления* существующего ресурса. В теле находятся данные для ресурса.

Обновляет/переписывает данные по указанному URL
не создает множество обьектов

---

DELETE: для удаления существующего ресурса.
Пример - **Httpie**

## Заголовки:
[Заголовки запроса HTTP 1 - Стандарт](https://www.w3.org/Protocols/rfc2616/rfc2616-sec5.html#sec5.3)

Request
- Accept
```
Accept: text/*, text/html, text/html;level=1, */*
```
- Accept-Charset
- Accept-Encoding
- Accept-Language
- Authorization
- From
- Host
- If-Modified-Since
- If-Match
- If-None-Match
- If-Range
- If-Unmodified-Since
- Max-Forwards
- Proxy-Authorization
- Range
- Referer
- User-Agent


# Коды ответов:

указывает клиенту, как интерпретировать ответ сервера.

- 200 ОК - ВСЕ НОРМ
- 301 Redirect - URL переехал
- 404 Error - ошибка на стороне клиента (неверный адрес)
- 504 Server error -> смотри логи

access.log

error.log

# Ответ сервера

```
HTTP/1.x 200 OK
Transfer-Encoding: chunked
Date: Sat, 28 Nov 2009 04:36:25 GMT
Server: LiteSpeed
Connection: close
X-Powered-By: W3 Total Cache/0.8
Pragma: public
Expires: Sat, 28 Nov 2009 05:36:25 GMT
Etag: "pub1259380237;gz"
Cache-Control: max-age=3600, public
Content-Type: text/html; charset=UTF-8
Last-Modified: Sat, 28 Nov 2009 03:50:37 GMT
Content-Encoding: gzip
Vary: Accept-Encoding, Cookie, User-Agent

<!DOCTYPE html>
<html lang="ru">
<head>
.................
```





# Additions

## GET

Полный запрос
```
http https://ecstatic-jones-729032.netlify.com/
```
Request GET
```
http --print=HB GET https://ecstatic-jones-729032.netlify.com/
```
Response only headers
```
http --print=h GET https://ecstatic-jones-729032.netlify.com/
```
Response headers + body
```
http --print=hb GET https://ecstatic-jones-729032.netlify.com/
```
---
Заголовки запроса и ответа
```
http --print=Hh https://ecstatic-jones-729032.netlify.com/
```
---

## POST
POST 1
```
http --print=HB --form post https://ecstatic-jones-729032.netlify.com/ foo=bar
```
POST 2
```
http --print=HB --form post https://ecstatic-jones-729032.netlify.com/ foo=bar
```
POST 2 - JSON данные
```
http --print=HB --json post https://ecstatic-jones-729032.netlify.com/ foo=bar
```


# Resources [самостоятельное изучение]
- [HTTP протокол - справка MDN](https://developer.mozilla.org/ru/docs/Web/HTTP)
- HTTP: The Protocol Every Web Developer Must Know [Part 1](https://code.tutsplus.com/ru/tutorials/http-the-protocol-every-web-developer-must-know-part-1--net-31177) и [Part 2](https://code.tutsplus.com/ru/tutorials/http-the-protocol-every-web-developer-must-know-part-2--net-31155)

- [HTTP Status Codes in 60 Seconds](https://webdesign.tutsplus.com/tutorials/http-status-codes-in-60-seconds--cms-24317)

- [HTTP Headers  для "чайников"](https://code.tutsplus.com/ru/tutorials/http-headers-for-dummies--net-8039)

- [Введение в изучение и использование DNS-записей](http://prgssr.ru/development/vvedenie-v-izuchenie-i-ispolzovanie-dns-zapisej.html)

- [Httpie - консольная утилита](https://httpie.org/)
- [Httpbin](http://httpbin.org/)


- https://stackoverflow.com/questions/107390/whats-the-difference-between-a-post-and-a-put-http-request
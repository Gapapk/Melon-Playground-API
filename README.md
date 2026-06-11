# 🔘 Melon Playground API
***API мелона*** *- для регистрации взаимодействия с серверами и прочем. через playmelonpg.com.
Сами сервера склона находится на амозон, с под доменом pg, хоть есть и другие 2 типа API.
Половину всех запросов на сервера через POST или GET, и заголовок для запросов лучше использовать такой:*

``
{"Content-Type": "application/json",
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36",
    "Origin": "https://pg.melonsandbox.com",
    "Referer": "https://pg.melonsandbox.com/"}
``

<hr>

# 🧠 Вход в аккаунт (Все POST.)
**Ссылка:**
``https://pg.playmelonpg.com/api/auth/by-login-password``

**Тело:**
```json
{
  "login": "Логин",
  "password": "Пароль"
}
```
**Ответ:**
```json
{
  "jwt": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZGVudGl0eVR5cGUiOiJ1c2VyIiwiaWRlbnRpdHlJZCI6ImUwODY0MDFhLTk2NWQtNDMwMy1iNGM5LTRlNWM1NjExMDM4MyIsImlkZW50aXR5Um9sZSI6InBsYXllciIsImV4cCI6MTc4MjM3ODY0MywiaWRlbnRpdHlLaW5kIjoidmVyaWZpZWRQbGF5ZXIiLCJ2ZXJzaW9uIjoidjEiLCJpYXQiOjE3ODExNjkwNDMsImlzcyI6ImF1dGgtc2VydmljZSJ9.dN1E_-DCJP1gdOcThlZht9BCvXR7zJDC-_BiN4ZaWAo",
  "jwtExpiredAt": 1782378643000,
  "userId": "e086401a-965d-4303-b4c9-4e5c56110383",
  "userKind": "verifiedPlayer",
  "userRole": "player",
  "tokenTtlSeconds": 1209600,
  "eventJwt": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZGVudGl0eVR5cGUiOiJ1c2VyLWV2ZW50IiwiaWRlbnRpdHlJZCI6ImUwODY0MDFhLTk2NWQtNDMwMy1iNGM5LTRlNWM1NjExMDM4MyIsImlkZW50aXR5Um9sZSI6IiIsImV4cCI6MTkzODg0OTA0MywiaWF0IjoxNzgxMTY5MDQzLCJpc3MiOiJhdXRoLXNlcnZpY2UifQ.qcSnAnjNBDuzN51_09yhHn0ay1g_H8oYLBKP8rAkEIA"
}
```

*Вход в аккаунт мелона по логину и паролю если раскопилировать jwt 
то получим:*

```json
{"alg":"HS256","typ":"JWT"}{"identityType":"user","identityId":"e086401a-965d-4303-b4c9-4e5c56110383","identityRole":"player","exp":1782378643,"identityKind":"verifiedPlayer","version":"v1","iat":1781169043,"iss":"auth-service"}
```
``userKind`` *- показывает подверждёна ли почта или нет.*

``userRole`` *- ваша роль* ``player`` *или* ``moderator``

*eventJwt - токен от ивентов если расшифровать из base64:*
```json
{"alg":"HS256","typ":"JWT"}{"identityType":"user-event","identityId":"e086401a-965d-4303-b4c9-4e5c56110383","identityRole":"","exp":1938849043,"iat":1781169043,"iss":"auth-service"}
```

***Важно - токены появляются только при регистрации и больше нигде.
Все следующие ответы будет такии же.***

<hr>

**Ссылка:**
``https://pg.playmelonpg.com/api/auth/by-email-password``

**Тело:**
```json
{
  "email": "Email",
  "password": "Пароль"
}
```
*Вход через почту.*

<hr>

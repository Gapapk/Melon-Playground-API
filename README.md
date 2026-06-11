<img src="Assets/logo.png" alt="Логотип.">

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

# 🧠 Вход в аккаунт
**Ссылка:** (POST)
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

**Ссылка:** (POST)
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

**Ссылка:** (POST)
``https://pg.playmelonpg.com/api/auth/by-social/web``

**Тело:**
```json
{
  "socialProviderKind": "google" | "apple",
  "socialToken": "Токен сессии"
}
```
*Вход тоже через гугл или эпл, если надо создать авторизацию через гугл илм эпл, то используйте Google Cloud Console или Apple Developer Account*

<hr>

**Ссылка:** (POST)
``https://pg.playmelonpg.com/api/auth/by-social/web``

**Тело:**
```json
{
  "externalDeviceId": "externalDeviceId",
  "deviceName": "deviceName" // необязательно
}
```
*Вход через ID устройство. (Анонимно.)*

<hr>

**Ссылка:** (POST)
``https://pg.playmelonpg.com/api/user/webhook-verify-login``

**Тело:**
```json
{
  "user": {
    "id": "Ник пользователя"
  },
  "projectId": 226733,
  "merchantId": 418104
}
```

**Ответ:**
```json
{
  "user": {
    "id": "123456l",
    "name": "123456l"
  }
}
```
*Вход через Xsolla по логину, но вы* ***никак НЕ можете*** *взаимодействовать с аком мелона, не зная его логин и пароль*

<hr>

**Ссылка:** (POST)
``https://pg.playmelonpg.com/api/auth/admin/by-login-password``

**Тело:**
```json
{
  "login": "Логин",
  "password": "Пароль"
}
```

*Вход в аккаунт админа по логину, но у вас скорее всего ничего не получится.*

# 🦾 Информация о аккаунте
**Ссылка:** (GET)
``https://pg.playmelonpg.com/api/user/me``

**Ответ:**
```json
{
  "id": "e086401a-965d-4303-b4c9-4e5c56110383",
  "login": "123456l",
  "kind": "verifiedPlayer",
  "role": "player",
  "withPassword": true,
  "device": {
    "id": "c067bb7b-ee60-40c7-addc-cb727d26858c",
    "platform": "IPhonePlayer",
    "externalDeviceId": "8180D8EF-B389-4EF8-AB9E-E1CEE002BF73",
    "name": "iPad",
    "systemName": "iPad7,5",
    "systemVersion": "iPadOS 17.5.1",
    "appAccountToken": "",
    "appsFlyerId": "1766619637876-1633812356075774279"
  },
  "socials": [],
  "blocked": false,
  "deleted": false,
  "createdAt": 1723877306491,
  "updatedAt": 1781175532891,
  "userEmail": {
    "notActiveEmail": "robtonnn@gmail.com",
    "consentToReceive": false
  },
  "lastActiveAt": 1781176925386,
  "avatarFileId": "95c3c925-7e29-4d9a-9f72-40285a483326",
  "referralCode": "XVJR-GLWZ-XMUA",
  "language": "en",
  "country": "FR"
}
```
*Информация о аккаунте и телефоне пользователя, и да ваш аккаунт* ***могут забанить или удалить.***
*Самое интересное что на сервере есть ещё реферальные коды, но их не используют.*

<hr>

**Ссылка:** (GET)
``https://pg.playmelonpg.com/api/account-preview/wallet/me``

**Ответ:**
```json
{
  "walletId": "f9e5e093-7595-476c-9902-1d5b1a2bf9d6",
  "userId": "e086401a-965d-4303-b4c9-4e5c56110383",
  "coins": 8,
  "availableWithdrawFiatCoins": 0,
  "hasActiveOperations": false
}
```

*Показывает ваш баланс в мелсах и прочее.*

<hr>

**Ссылка:** (GET)
``https://pg.playmelonpg.com/api/fiat/order/me``

**Ответ:**
```json
{ }
```
```json
[
  {
    "createdAt": "2024-01-13T10:32:00Z",
    "usdAmount": 190,
    "state": "waitRefundCoins",
    "orderId": "ORD-1452"
  }
]
```

*Показывает историю и статусы заявок на вывод средств, если нет, то по молчанию пустое.*

<hr>

**Ссылка:** (POST)
``https://pg.playmelonpg.com/api/fiat/order/create``

**Тело:**
```json
{
  "coinsAmount": 75000
}
```
*Создание заявок на вывод средств. Минум 75000 мелсов, и вряд-ли это получится сделать в России.*

<hr>

**Ссылка:** (GET)
``https://pg.playmelonpg.com/api/internal-notice/filter?limit={limit}&offset={offset}``

**Ответ:**
```json
{
  "objects": [
    {
      "id": "id",
      "receiverId": "receiverId",
      "status": "read" | "unread",
      "createdAt": 44,
      "updatedAt": 2,
      "notificationContent": {
        "body": "body",
        "meta": {
          "kind": "content_status" | "store_item_status" | "store_item_status",
          "contentId": "content,
          "itemId": "item"
        }
      }
    }
  ],
  "filterMeta": {
    "totalItems": 4,
    "offset": 2
  }
}
```
*Показывает ваши уведомления, надо указывать лимит и offset.*

<hr>

**Ссылка:** (GET)
``https://pg.playmelonpg.com/api/internal-notice/count-unread``

**Ответ:**
```json
{
  "unreadCount": 0
}
```
*Показывает количество непрочитанных уведомлений*

<hr>

**Ссылка:** (POST)
``https://pg.playmelonpg.com/api/internal-notice/read``

**Тело:**
```json
{
  "internalNoticeIds": ["id", "id"]
}
```
*Прочивает сообщение по ID.*

<hr>

**Ссылка:** (POST)
``https://pg.playmelonpg.com/api/internal-notice/read-all``

*Прочитывает все уведомления, и не имеет тела и ответ пустой.*

<hr>

**Ссылка:** (POST)
``https://pg.playmelonpg.com/api/internal-notice/archive``

**Тело:**
```json
{
  "internalNoticeIds": ["id", "id"]
}
```

*Архивирует/Удаляет сообщения, ответ тоже пустой.*

# 🌀 Настройка акаунта
**Ссылка:** (POST)
``https://pg.playmelonpg.com/api/user/set-email``

**Тело:**
```json
{
  "email": "user@gmail.com"
}
```

*Отправляет сообщение с добавлением почты на ак на ваш email.*

<hr>

**Ссылка:** (POST)
``https://pg.playmelonpg.com/api/user/confirm-email``

**Тело:**
```json
{
  "tokenValue": "123456"
}
```
*Вводите туда свой код и подтверждаете свой email. Код действует плоть до 1 минуты.*

<hr>

**Ссылка:** (POST)
``https://pg.playmelonpg.com/api/user/init-password``

**Тело:**
```json
{
  password: Новый пароль
}
```
*Просто меняет сразу пароль.*

<hr>

**Ссылка:**
``https://pg.playmelonpg.com/api/user/change-password``

**Тело:***
```json
{
  currentPassword: Старый пароль,
  newPassword: Новый пароль
}
```
*Меняет пароль, но нужно знать старый пароль.*

<hr>

**Ссылка:** (POST)
``https://pg.playmelonpg.com/api/user/reset-password/init``

**Тело:**
```json
{
  "email": "user@gmail.com"
}
```

*Отправка на email сброс пароля.*

<hr>

**Ссылка:** (POST)
``https://pg.playmelonpg.com/api/user/reset-password/confirm``

**Тело:**
```json
{
  "email": "user@gmail.com",
  "proofTokenValue": "123456",
  "newPlainTextPassword": "Новый пароль."
}
```

*Сбрасывает пароль, нужно знать код, email и потом устанавливаете новый пароль. (от 5 до 50 символов и нужна хотя-бы 1 англ буква, и только англ. буквы, цифры и _ после первого символа.*

<hr>

**Ссылка:** (POST)
``https://pg.playmelonpg.com/api/user/set-login``

**Тело:**
```json
{
  login: Новый логин.
}
````
*Устанавливает новый логин пользователя от 2 до 50 символов, и только англ. буквы, цифры и _ после первого символа.*

<hr>

**Ссылка:** (POST)
``https://pg.playmelonpg.com/api/user/remove/issue/create-without-user``

**Тело:**
```json
{
  "name": "Имя",
  "description": "Причина",
  "email": "Тут он принимает gmail."
}
```

*Запрос на удаление аккаунта, дальше на вашу почту может прити сообщение о удаление ака.*

<hr>

**Ссылка:**
``https://pg.playmelonpg.com/api/auth/logout``

*Не имеет тела и ответа, просто выходит из аккаунта, правда смысл если можно зайти сразу в другой.*

# 🧱 Другое

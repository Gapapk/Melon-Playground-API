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

```

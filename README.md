* Тестовое задание на позицию Junior Backend Developer

**Используемые технологии:**

- Go
- JWT
- MongoDB

**Задание:**

Написать часть сервиса аутентификации.

Два REST маршрута:

- Первый маршрут выдает пару Access, Refresh токенов для пользователя с идентификатором (GUID) указанным в параметре запроса
- Второй маршрут выполняет Refresh операцию на пару Access, Refreshтокенов

**Требования:**

Access токен тип JWT, алгоритм SHA512, хранить в базе строго запрещено.

Refresh токен тип произвольный, формат передачи base64, хранится в базеисключительно в виде bcrypt хеша, должен быть защищен от изменения настороне клиента и попыток повторного использования.

Access, Refresh токены обоюдно связаны, Refresh операцию для Access токена можно выполнить только тем Refresh токеном который был выдан вместе с ним.

**Результат:**

Результат выполнения задания нужно предоставить в виде исходного кода на Github.

Сервер генерирует пару токенов и отсылает на клиент (клиент может их хранить как угодно(желательно в Cookie)).
Клиент мониторит состояние access токена по его времени жизни, как только он истек клиент отправляет запрос на обновление ключей.
Сервер принимает Refresh токен, проверяет все сессии пользователя (их может быть много). Если не находит такого Refresh, то делает logout и возваращает ошибку,
если находит, то обновляет токены и отсылает обратно на клиент.

Чтобы защититься от хакеров refresh токен зифруется и валидируется. Даже если на клиенте данный токен изменят, то он банально не пройдет проверку и произойдет logout.
Если хакер украдет access токен, то это не страшно, т.к. access токен имеет время жизни 60 минут.

![Генерация](https://github.com/NetworkPy/TestTaskJuniorBackDev/blob/master/img/generate.jpg)
![Обновление](https://github.com/NetworkPy/TestTaskJuniorBackDev/blob/master/img/refresh.jpg)
![Результаты в БД](https://github.com/NetworkPy/TestTaskJuniorBackDev/blob/master/img/result.jpg)



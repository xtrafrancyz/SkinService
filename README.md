VimeWorld SkinService
====================
Высокопроизводительный сервис для аватарок из скинов проекта [VimeWorld.ru](http://vimeworld.ru). Его также можно подключить к любой другой системе скинов, как к локальной (файлы на том же хосте), так и к удалённой (через http запросы).

Для полноценной работы рекомендуется использовать CloudFlare поверх сервиса. Он позволяет кешировать все сгенерированные аватарки, тем самым значительно снижая нагрузку на сам сервис. При изменении скина или плаща можно удалить весь кеш с помощью приватных методов очистки.

Рабочая версия запущена здесь: [http://skin.vimeworld.ru](http://skin.vimeworld.ru)

## Публичное API ##
#### Скин ####
Всё тело целиком без второго слоя:
```
GET /body/{username}.png
GET /body/{username}/{size}.png
```
Голова без второго слоя:
```
GET /head/{username}.png
GET /head/{username}/{size}.png
```
Голова со вторым слоем (со шлемом):
```
GET /helm/{username}.png
GET /helm/{username}/{size}.png
```
Оригинальный скин:
```
GET /raw/skin/{username}.png
```

#### Плащ ####
Задняя сторона плаща (которая чаще всего видна игрокам):
```
GET /cape/{username}.png
```
Оригинальный плащ:
```
GET /raw/cape/{username}.png
```

#### Скины и плащи для игры ####
Для версий до 1.8:
```
GET /game/v1/skin/{username}.png
GET /game/v1/cape/{username}.png
```
Для версий после 1.8:
```
GET /game/v2/skin/{username}.png
GET /game/v2/cape/{username}.png
```


## Приватное API ##
Для доступа к приватному API необходимо иметь токен авторизации, который указывается в конфиге. Все приватные методы начинаются с `/private/{token}/`.
#### Очистка кеша ####
Удаление плаща из кеша сервиса и CloudFlare:
```
DELETE /private/{token}/cache/cape/{username}
```
Удаление скина и всех вытекающих из кеша сервиса и CloudFlare:
```
DELETE /private/{token}/cache/skin/{username}
```

## Описание

Яндекс Практикум. API для Yatube.
Проект api_yatube представляет из себя API для блога.

## Функционал

- Подписка и отписка от авторизованного пользователя;
- Авторизованный пользователь просматривает посты, создавёт новые, удаляет и изменяет их;
- Просмотр сообществ;
- Комментирование, просмотр, удаление и обновление комментариев;
- Фльтрация по полям.
##
## Полная документация по api_yatube находится по адресу http://127.0.0.1:8000/redoc/
## Установка


### Как запустить проект:

Клонировать репозиторий и перейти в него в командной строке:

```
git clone https://github.com/kirillcray/api_final_yatube
```

```
cd api_final_yatube
```

Cоздать и активировать виртуальное окружение:

```
python -m venv venv
```

* Если у вас Linux/macOS

    ```
    source venv/bin/activate
    ```

* Если у вас windows

    ```
    source venv/scripts/activate
    ```

```
python -m pip install --upgrade pip
```

Установить зависимости из файла requirements.txt:

```
pip install -r requirements.txt
```

Выполнить миграции:

```
python yatube_api/manage.py migrate
```

Запустить проект:

```
python yatube_api/manage.py runserver
```


### Примеры запросов:

POST-запрос для получения всех постов.

`GET http://127.0.0.1:8000/api/posts/`

Ответ:

```
[
    {
        "id": 1,
        "author": 1,
        "text": "Мой первый пост!",
        "pub_date": "2023-10-01T12:00:00Z",
        "group": null
    },
    {
        "id": 2,
        "author": 2,
        "text": "Второй пост в группе",
        "pub_date": "2023-10-02T14:30:00Z",
        "group": 1
    }
]
```


POST-запрос, создание группы.

`POST http://127.0.0.1:8000/api/groups/`
"Content-Type: application/json"
'{"title": "Новая группа", "slug": "newgroup", "description": "Описание"}'

Ответ:

```
{
    "id": 2,
    "title": "Новая группа",
    "slug": "newgroup",
    "description": "Описание"
}
```

GET-запрос, все комментарии к посту с id =1.

`GET http://127.0.0.1:8000/api/posts/1/comments/`

```
[
    {
        "id": 1,
        "post": 1,
        "author": 2,
        "text": "Отличный пост!",
        "created": "2023-10-01T12:30:00Z"
    }
]
```

POST-запрос, подписка на пользователя

`POST http://127.0.0.1:8000/api/follow/`
"Content-Type: application/json"
'{"following": 2}'
"Authorization: Token ваш_токен"

Ответ:

```
{
    "user": 1,
    "following": 3
}


# api_yamdb
## Описание проекта api_yamdb:
Проект **YaMDb** собирает отзывы пользователей на произведения. Сами произведения в **YaMDb** не хранятся, здесь нельзя посмотреть фильм или послушать музыку.
Произведения делятся на ***категории***, такие как «Книги», «Фильмы», «Музыка».
Произведению может быть присвоен ***жанр*** из списка предустановленных (например, «Сказка», «Рок» или «Артхаус»). 
Добавлять произведения, категории и жанры может _только администратор_.
Благодарные или возмущённые пользователи оставляют к произведениям текстовые ***отзывы*** и ставят произведению оценку в диапазоне от одного до десяти (целое число); из пользовательских оценок формируется усреднённая оценка произведения — ***рейтинг*** (целое число).
На одно произведение пользователь может оставить _только один отзыв_.
Пользователи могут оставлять ***комментарии*** к отзывам.
Добавлять отзывы, комментарии и ставить оценки могут только _аутентифицированные пользователи_.

## Примеры некоторых запросов к API:
### Регистрация нового пользователя
Получить код подтверждения на переданный email. Права доступа: Доступно без токена. Использовать имя 'me' в качестве username запрещено. Поля email и username должны быть уникальными.
```
POST http://127.0.0.1:8000/api/v1/auth/signup/
```
```
{
  "email": "user@example.com",
  "username": "string"
}
```
### Получение JWT-токена
Получение JWT-токена в обмен на username и confirmation code. Права доступа: Доступно без токена.
```
POST http://127.0.0.1:8000/api/v1/auth/token/
```
```
{
  "username": "string",
  "confirmation_code": "string"
}
```
### Получение списка всех произведений
Получить список всех объектов. Права доступа: Доступно без токена
```
GET http://127.0.0.1:8000/api/v1/titles/
```
```
{
  "count": 0,
  "next": "string",
  "previous": "string",
  "results": [
    {
      "id": 0,
      "name": "string",
      "year": 0,
      "rating": 0,
      "description": "string",
      "genre": [
        {
          "name": "string",
          "slug": "string"
        }
      ],
      "category": {
        "name": "string",
        "slug": "string"
      }
    }
  ]
}
```
### Добавление нового отзыва
Добавить новый отзыв. Пользователь может оставить только один отзыв на произведение. Права доступа: Аутентифицированные пользователи.
```
POST http://127.0.0.1:8000/api/v1/titles/{title_id}/reviews/
```
```
{
  "text": "string",
  "score": 1
}
```
### Добавление комментария к отзыву
Добавить новый комментарий для отзыва. Права доступа: Аутентифицированные пользователи.
```
POST http://127.0.0.1:8000/api/v1/titles/{title_id}/reviews/{review_id}/comments/
```
```
{
  "text": "string"
}
```
### Получение данных своей учетной записи
Получить данные своей учетной записи Права доступа: Любой авторизованный пользователь
```
GET http://127.0.0.1:8000/api/v1/users/me/
```
```
{
  "username": "string",
  "email": "user@example.com",
  "first_name": "string",
  "last_name": "string",
  "bio": "string",
  "role": "user"
}
```
## Как запустить проект:

**Клонировать репозиторий и перейти в него в командной строке:**
```
git@github.com:Hottys/api_yamdb.git
```
```
cd api_yamdb
```
**Cоздать и активировать виртуальное окружение:**
```
py -m venv env
```
```
source venv/Scripts/activate
```
**Установить зависимости из файла requirements.txt:**
```
python3 -m pip install --upgrade pip
```
```
pip install -r requirements.txt
```
**Выполнить миграции:**
```
python3 manage.py migrate
```
**Запустить проект:**
```
python3 manage.py runserver
```
## Запуск с помощью docker-compose

Для запуска контейнера из папки "infra" с помощью docker-compose, используйте команду:
```
cd infra
docker-compose up -d --build
```
Для выполнения миграций внутри контейнера, используйте команды:
```
docker-compose exec web python manage.py makemigrations
docker-compose exec web python manage.py migrate
```
Для создания суперпользователя внутри контейнера, используйте команду:
```
docker-compose exec web python manage.py createsuperuser
```
Для сборки статических файлов внутри контейнера, используйте команду:
```
docker-compose exec web python manage.py collectstatic --no-input
```

## Об авторах

- https://github.com/Denis-Krapp - Денис 
  - Модели, views, serializers и эндпоинты для произведений, категорий и жанров
  - Импорт данных из csv файлов
  - README файл
- https://github.com/Hottys - Михаил
  - Система регистрации и аутентификации
  - Система подтвержения через e-mail
  - Модель, views, serializers и эндпоинты для пользователя
  - Права досупа
  - Токены
- https://github.com/EvgenyMi - Евгений
  - Модели, views, serializers и эндпоинты для отзывов и комментариев
  - Рейтинг произведений
## Технологии
Много сил и времени ушло на содание данного проекта, который является для нас первым групповым проектом. Мы тщательно изучали теорию и документации.

Приложения, которые были использованы при создани  проекта:
  - Python
  - Django
  - Django Rest Framework

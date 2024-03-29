## YaMDb API

#### API для  проекта "YaMDb" 

YaMDb собирает отзывы (Reviews) пользователей на произведения (Titles). Произведения делятся на категории: «Книги», «Фильмы», «Музыка». Список категорий (Categories) может быть расширен Администратором. 

Произведению может быть присвоен жанр (Genre) из списка предустановленных (например, «Сказка», «Рок» или «Артхаус»). Новые жанры может создавать только Администратор. 

Пользователи оставляют к произведениям текстовые отзывы (Review) и ставят произведению оценку (Score) в диапазоне от 1 до 10; из пользовательских оценок формируется усреднённая оценка произведения — рейтинг (Raiting). На одно произведение пользователь может оставить только один отзыв. 

Для авторизации пользователей используется код подтверждения высылаемый на email. Для аутентификации пользователей используются JWT-токены. 

### Технологии: 

Python, Django, Django Rest Framework, Simple JWT 

### Запуск проекта: 

- Клонировать репозиторий и перейти в него в командной строке: 
``` 
git clone https://github.com/mikhailsoldatkin/api_yamdb.git 
cd api_yamdb 
``` 

- Создать и активировать виртуальное окружение: 

``` 
python -m venv venv  
source venv/bin/activate (Mac, Linux) 
source venv/scripts/activate (Windows) 
``` 

- Установить зависимости из файла requirements.txt: 

``` 
python -m pip install --upgrade pip  
pip install -r requirements.txt 
``` 

- Перейти в рабочую папку и выполнить миграции: 

``` 
cd api_yamdb 
python manage.py migrate 
``` 

- Запустить сервер: 

``` 
python manage.py runserver 
``` 

### Документация к проекту: 

После запуска проекта документация доступна по адресу: [http://127.0.0.1:8000/redoc/](http://127.0.0.1:8000/redoc/). В ней описаны возможные запросы к API и структура ожидаемых ответов. Для каждого запроса указаны уровни прав доступа: пользовательские роли, которым разрешён запрос. 

### Примеры запросов к API: 

- Получение списка всех произведений: доступно без токена. 

*Запрос:* 

``` 
GET yamdb.com/api/v1/titles/ 
``` 

*Пример ответа:* 

 ``` 
[ 
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
] 
``` 

- Добавление нового отзыва к произведению: доступно аутентифицированным пользователям. 

*Запрос:* 

``` 
POST yamdb.com/api/v1/titles/{title_id}/reviews/ 
``` 

*Содержимое запроса:* 

``` 
{ 
  "text": "string", 
  "score": 1 
} 
``` 

*Пример ответа:* 

``` 
{ 
  "id": 0, 
  "text": "string", 
  "author": "string", 
  "score": 10, 
  "pub_date": "2019-08-24T14:15:22Z" 
} 
``` 

- Добавление комментария к отзыву: доступно аутентифицированным пользователям. 

*Запрос:* 

``` 
POST yamdb.com/api/v1/titles/{title_id}/reviews/{review_id}/comments/ 
``` 

*Содержимое запроса:* 

``` 
{ 
  "text": "string" 
} 
``` 

*Пример ответа:* 

``` 
{ 
  "id": 0, 
  "text": "string", 
  "author": "string", 
  "pub_date": "2019-08-24T14:15:22Z" 
} 
``` 

- Удаление пользователя по имени пользователя (username): доступно Администратору. 

*Запрос:* 

``` 
DELETE yamdb.com/api/v1/users/{username}/ 
``` 

### Авторы: 

Михаил Солдаткин, Александр Жбаков, Дмитрий Коротеев (c) 2022

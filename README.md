# API_YamDB

REST API для сервиса YaMDb — базы отзывов о фильмах, книгах и музыке.

Проект YaMDb собирает отзывы пользователей на произведения. Произведения делятся на категории: «Книги», «Фильмы», «Музыка».
Произведению может быть присвоен жанр. Новые жанры может создавать только администратор.
Читатели оставляют к произведениям текстовые отзывы и выставляют произведению рейтинг (оценку в диапазоне от одного до десяти).
Из множества оценок автоматически высчитывается средняя оценка произведения.

Аутентификация по JWT-токену

Поддерживает методы GET, POST, PUT, PATCH, DELETE

Предоставляет данные в формате JSON

Cоздан в команде из трёх человек с использованим Git в рамках учебного курса Яндекс.Практикум.

## Стек технологий
- проект написан на Python с использованием Django REST Framework
- библиотека Simple JWT - работа с JWT-токеном
- библиотека django-filter - фильтрация запросов
- база данных - SQLite3
- система управления версиями - git

## Как запустить проект:

1) Клонируйте репозитроий с проектом:
```
git clone git@github.com:NBN879/api_yamdb_final.git
```
2) В созданной директории установите виртуальное окружение, активируйте его и установите необходимые зависимости:
```
python3 -m venv venv

. venv/bin/activate

pip install -r requirements.txt
```
3) Выполните миграции:
```
python manage.py migrate
```
4) Cоздайте суперпользователя:
```
python manage.py createsuperuser
```
5) Загрузите тестовые данные:
```
python manage.py load_data
```
6) Запустите сервер:
```
python manage.py runserver
```
__________________________________

Ваш проект запустился на http://127.0.0.1:8000/

Полная документация доступна по адресу http://127.0.0.1:8000/redoc/

С помощью команды *pytest* вы можете запустить тесты и проверить работу модулей

## Алгоритм регистрации пользователей
- Пользователь отправляет POST-запрос на добавление нового пользователя с параметрами *email* и *username* на эндпоинт /api/v1/auth/signup/.
- **YaMDB** отправляет письмо с кодом подтверждения (*confirmation_code*) на адрес *email*.
- Пользователь отправляет POST-запрос с параметрами *username* и *confirmation_code* на эндпоинт /api/v1/auth/token/, в ответе на запрос ему приходит token (JWT-токен).
- При желании пользователь отправляет PATCH-запрос на эндпоинт /api/v1/users/me/ и заполняет поля в своём профайле (описание полей — в документации).

## Пользовательские роли
- **Аноним** — может просматривать описания произведений, читать отзывы и комментарии.
- **Аутентифицированный пользователь** (*user*) — может, как и **Аноним**, читать всё, дополнительно он может публиковать отзывы и ставить оценку произведениям (фильмам/книгам/песенкам), может комментировать чужие отзывы; может редактировать и удалять свои отзывы и комментарии. Эта роль присваивается по умолчанию каждому новому пользователю.
- **Модератор** (*moderator*) — те же права, что и у А**утентифицированного пользователя** плюс право удалять любые отзывы и комментарии.
- **Администратор** (*admin*) — полные права на управление всем контентом проекта. Может создавать и удалять произведения, категории и жанры. Может назначать роли пользователям.
- **Суперюзер Django** — обладает правами администратора (*admin*)

## Ресурсы API YaMDb

- Ресурс AUTH: аутентификация.
- Ресурс USERS: пользователи.
- Ресурс TITLES: произведения, к которым пишут отзывы (определённый фильм, книга или песня).
- Ресурс CATEGORIES: категории (типы) произведений («Фильмы», «Книги», «Музыка»).
- Ресурс GENRES: жанры произведений. Одно произведение может быть привязано к нескольким жанрам.
- Ресурс REVIEWS: отзывы на произведения. Отзыв привязан к определённому произведению.
- Ресурс COMMENTS: комментарии к отзывам. Комментарий привязан к определённому отзыву.
______________________________________________________________________

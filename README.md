![Django-app workflow](https://github.com/kontarevakate/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)

# Публичный IP-адрес
Проект доступен по адресу: http://158.160.0.121/redoc/

# Описание:

Проект YaMDb собирает отзывы пользователей на различные произведения.

# Пользовательские роли:
**Аноним** — может просматривать описания произведений, читать отзывы и комментарии.

**Аутентифицированный пользователь (user)** — может, как и Аноним, читать всё, дополнительно он может публиковать отзывы и ставить оценку произведениям (фильмам/книгам/песенкам), может комментировать чужие отзывы; может редактировать и удалять свои отзывы и комментарии. Эта роль присваивается по умолчанию каждому новому пользователю.

**Модератор (moderator)** — те же права, что и у Аутентифицированного пользователя плюс право удалять любые отзывы и комментарии.

**Администратор (admin)** — полные права на управление всем контентом проекта. Может создавать и удалять произведения, категории и жанры. Может назначать роли пользователям.

**Суперюзер Django** — обладет правами администратора (admin)

Для аутентификации используйте JWT-токены.

# Доступные адресса запросов:

1. .../api/v1/auth/signup/ (POST)
2. .../api/v1/auth/token/ (POST)
3. .../api/v1/categories/ (GET, POST, DEL)
4. .../api/v1/genres/ (GET, POST, DEL)
5. .../api/v1/titles (GET, POST)
6. .../api/v1/titles/{titles_id} (GET, PATCH, DEL)
7. .../api/v1/titles/{title_id}/reviews/ (GET, POST)
8. .../api/v1/titles/{title_id}/reviews/{review_id}/ (GET, PATCH, DEL)
9. .../api/v1/titles/{title_id}/reviews/{review_id}/comments/ (GET, POST)
10. .../api/v1/titles/{title_id}/reviews/{review_id}/comments/{comment_id}/ (GET, PATCH, DEL)
11. .../api/v1/users/ (GET, POST)
12. .../api/v1/users/{username}/ (GET, PATCH, DEL)
13. .../api/v1/users/me/ (GET, PATCH)

# Шаблон наполнения .env файла:

DB_ENGINE=...
DB_NAME=...
POSTGRES_USER=...
POSTGRES_PASSWORD=...
DB_HOST=...
DB_PORT=...

# Установка:

Клонировать репозиторий и перейти в него в командной строке:

```
git clone https://github.com/kontarevakate/infra_sp2.git
```

```
cd infra_sp2
```

Запустить docker-compose:

```
docker-compose up -d --build
```

Выполнить миграции:

```
docker-compose exec web python manage.py migrate
```

Создать суперпользователя:

```
docker-compose exec web python manage.py createsuperuser
```
Подгрузить статику:

```
docker-compose exec web python manage.py collectstatic --no-input
```

Заполнить базу данными:

```
docker-compose exec web python manage.py loaddata fixtures.json
```

# Самостоятельная регистрация:

Для самостоятельной регистрации нужно отправить POST запрос на адресс .../api/v1/auth/signup/:

```
{
  "email": "string",
  "username": "string"
}
```

В ответе будет придёт **confirmation_code** он понадобиться для получения JWT токена.
Для того чтобы получить JWT токен нужно отправить POST запрос на адресс .../api/v1/auth/token/:
```
{
  "username": "string",
  "confirmation_code": "string"
}
```

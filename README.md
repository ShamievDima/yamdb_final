# Учебный проект: yamdb_final

# Проект YaMDb
Проект YaMDb собирает отзывы (Review) пользователей на произведения (Title). Произведения делятся на категории: «Книги», «Фильмы», «Музыка». Список категорий (Category) может быть расширен (например, можно добавить категорию «Спорт» или «Видеоигры»).
 
Читатели могут оставить к произведениям текстовые отзывы (Review) и выставить произведению рейтинг (оценку в диапазоне от 1 до 10). Из множества оценок автоматически высчитывается средняя оценка произведения.
​
# Бейдж о статусе работы workflow

![example workflow](https://github.com/ShamievDima/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)


# Пользовательские роли
 
* **Аноним** — может просматривать описания произведений, читать отзывы и комментарии.
* **Аутентифицированный пользователь (user)**— может читать всё, как и Аноним, дополнительно может публиковать отзывы и ставить рейтинг произведениям, может комментировать чужие отзывы и ставить им оценки; может редактировать и удалять свои отзывы и комментарии.
* **Модератор (moderator)** — те же права, что и у Аутентифицированного пользователя плюс право удалять любые отзывы и комментарии.
* **Администратор (admin)** — полные права на управление проектом и всем его содержимым. Может создавать и удалять произведения, категории и жанры. Может назначать роли пользователям.
* **Администратор Django** — те же права, что и у роли Администратор.

## Установка

Установка зависимостей из файла requirements и линтера flake8:

```
python -m pip install --upgrade pip
pip install flake8 pep8-naming flake8-broken-line flake8-return
flake8-isort
pip install -r requirements.txt
```

Проверка кода на PEP8 и запуск pytest:

```
python -m flake8
pytest
```


Остановить службу: 

```sudo systemd stop nginx```

​
Установить докер:

```sudo apt install docker.io```


Установить docker-compose

```
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker-compose --version
```

Скопируйте файлы docker-compose.yaml и nginx/default.conf из вашего проекта на сервер в home/<ваш_username>/docker-compose.yaml и home/<ваш_username>/nginx/default.conf соответственно:

```
scp docker-compose.yaml <USER>@<HOST>
scp default.conf <USER>@<HOST>:/nginx/
```

Остановка docker-compose, создание и наполнение файла .env на сервере:

```
sudo docker-compose stop
sudo docker-compose rm web
​touch .env
echo DB_ENGINE=${{ secrets.DB_ENGINE }} >> .env
echo DB_NAME=${{ secrets.DB_NAME }} >> .env
echo POSTGRES_USER=${{ secrets.POSTGRES_USER }} >> .env
echo POSTGRES_PASSWORD=${{ secrets.POSTGRES_PASSWORD }} >> .env
echo DB_HOST=${{ secrets.DB_HOST }} >> .env
echo DB_PORT=${{ secrets.DB_PORT }} >> .env
sudo docker-compose up -d
```

## Развертывание приложения

1. При пуше в ветку main приложение пройдет тесты, обновит образ на DockerHub и сделает деплой на сервер. Дальше необходимо подлкючиться к серверу.
```
ssh <USER>@<HOST>
```
2. Перейдите в запущенный контейнер приложения командой:
```
docker container exec -it <CONTAINER ID> bash
```
3. Внутри контейнера необходимо выполнить миграции и собрать статику приложения:
```
python manage.py collectstatic --no-input
python manage.py migrate
```
4. Для использования панели администратора по адресу http://178.154.194.4/admin/ необходимо создать суперпользователя.
```
python manage.py createsuperuser.
```

Сайт можно найти [здесь](http://178.154.194.4/admin/)


# Технологии применяемые в работе

- django
- djangorestframework
- Docker
- docker-compose
- YandexCloud
- nginx

# Автор

* **Дмитрий Шамиев** - [ShamievDima](https://https://github.com/ShamievDima)

# Облачное хранилище

## Описание проекта

Задача — разработать REST-сервис. Сервис должен предоставить REST-интерфейс для загрузки файлов и вывода списка уже загруженных файлов пользователя. 

Все запросы к сервису должны быть авторизованы. Заранее подготовленное веб-приложение (FRONT) должно подключаться к разработанному сервису без доработок, 
а также использовать функционал FRONT для авторизации, загрузки и вывода списка файлов пользователя.

## Требования к приложению

- Сервис должен предоставлять REST-интерфейс для интеграции с FRONT.
- Сервис должен реализовывать все методы, описанные в [yaml-файле](./CloudServiceSpecification.yaml):
  1. Вывод списка файлов.
  2. Добавление файла.
  3. Удаление файла.
  4. Авторизация.
- Все настройки должны вычитываться из файла настроек (yml).
- Информация о пользователях сервиса (логины для авторизации) и данные должны храниться в базе данных (на выбор студента).

## Требования к реализации

- Приложение разработано с использованием Spring Boot.
- Использован сборщик пакетов gradle/maven.
- Для запуска используется docker, docker-compose.
- Код размещён на Github.
- Код покрыт unit-тестами с использованием mockito.
- Добавлены интеграционные тесты с использованием testcontainers.

## Шаги реализации

- Изучите протокол получения и отправки сообщений между FRONT и BACKEND.
- Нарисуйте схему приложений.
- Опишите архитектуру приложения, где хранятся настройки и большие файлы, структуры таблиц/коллекций базы данных.
- Создайте репозиторий проекта на Github.
- Напишите приложение с использованием Spring Boot.
- Протестируйте приложение с помощью curl/postman.
- Протестируйте приложение с FRONT.
- Напишите README.md к проекту.
- Отправьте на проверку.

## Описание и запуск FRONT

1. Установите nodejs (версия не ниже 14.15.0) на компьютер, следуя [инструкции](https://nodejs.org/ru/download/).
2. Скачайте [FRONT](./netology-diplom-frontend) (JavaScript).
3. Перейдите в папку FRONT приложения и все команды для запуска выполняйте из неё.
4. Следуя описанию README.md FRONT проекта, запустите nodejs-приложение (npm install...).
5. Можно задать url для вызова своего backend-сервиса.
    1. В файле `.env` FRONT (находится в корне проекта) приложения нужно изменить url до backend, например: `VUE_APP_BASE_URL=http://localhost:8080`.
    2. Пересоберите и запустите FRONT снова: `npm run build`.
    3. Изменённый `url` сохранится для следующих запусков.
6. По умолчанию FRONT запускается на порту 8080 и доступен по url в браузере `http://localhost:8080`.

## Авторизация приложения

FRONT-приложение использует header `auth-token`, в котором отправляет токен (ключ-строка) для идентификации пользователя на BACKEND.
Для получения токена нужно пройти авторизацию на BACKEND и отправить на метод /login логин и пароль. В случае успешной проверки в ответ BACKEND должен вернуть json-объект
с полем `auth-token` и значением токена. Все дальейшие запросы с FRONTEND, кроме метода /login, отправляются с этим header.
Для выхода из приложения нужно вызвать метод BACKEND /logout, который удалит/деактивирует токен. Последующие запросы с этим токеном будут не авторизованы и вернут код 401.

> Для запуска FRONT-приложения с расширенным логированием нужно использовать команду: npm run serve.

____________

# Опис проблемної області

Веб-застосунок призначений для надання сервісу підбору авто для потреб ЗСУ. Для кожного оголошення передбачено оцінку за дискретною шкалою (0-10) з урахуванням критеріїв:

- Ціна
- Пробіг
- Рік випуску
- Тип кузова

Застосунок містить функціонал динамічної фільтрації оголошень авто за фільтрами:

- Марка
- Модель
- Ціна
- Рік випуску
- Пробіг

Функціонал аутентифікації передбачає можливість реєстрації нового облікового запису, або логін до існуючого. Система використовує JWT-токени для забезпечення валідності сесії з динамічною інвалідацією у випадку прострочення токену.

Функціонал аутентифікації та система ролей, таких як користувач або адміністратор, надають можливість обмеження доступу до функціоналу в залежності від ролі користувача. Авторизований користувач може переглядати оголошення, а також, зберігати їх до вподобаних. В ролі адміністратора доступний функціонал редагування або видалення існуючих оголошень.

# Інфраструктура для розгортання

## Dependencies

Для керування залежностями використовується пакетний менеджер pnpm. Для встановлення залежностей використовується команда:

```bash
pnpm install
```

## Environment variables

### Server

- DATABASE_URL - URL для підключення до бази даних
- JWT_SECRET - Секретний ключ для підпису JWT-токенів

### Client

- NEXT_PUBLIC_BASE_URL - URL, за яким розгорнуто веб-застосунок
- NEXT_PUBLIC_API_URL - URL, за яким розгорнуто сервер
- JWT_SECRET - Секретний ключ для підпису JWT-токенів

## Postgres

Для роботи з базою даних використовується СУБД Postgres. Для локального розгортання бази даних може використовуватись Docker, або ПЗ для хостингу Postgres-серверу на локальній машині.
Docker-команда для розгортання контейнера з Postgres:

```bash
docker run --name my-postgres -e POSTGRES_USER=postgres -e POSTGRES_PASSWORD=postgres -p 543212:5432 -d postgres:latest
```

## Development

Для запуску сервера в режимі розробки необхідно виконати команди:

### Server

```bash
pnpm install
pnpm run migrate:reset
pnpm run seed
pnpm run dev
```

### Client

```bash
pnpm run dev
```

Після запуску сервера та клієнта в режимі розробки, веб-застосунок буде доступний за адресою http://localhost:3000.
Для заповнення БД оголошеннями з сайту https://auto.ria.com, потрібно зайти на ендпоїнт сервера: `/crawler`. Після цього, в БД буде збережено близько 100 оголошень авто.

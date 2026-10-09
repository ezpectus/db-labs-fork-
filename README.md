# Лабораторні роботи з БД — VideoHub

**Студент:** Степаненко Денис
**Група:** ІМ-051, ФІОТ, НТУУ «КПІ ім. Ігоря Сікорського»
**Проєкт:** [VideoHub](https://github.com/ezpectus/VideoHub) — відеохостинг-платформа (аналог YouTube)
**СУБД:** PostgreSQL (+ Prisma ORM у Lab 6)

Форк репозиторію курсу з моїми виконаними лабораторними у папці **[MyWork/](MyWork/)**.

---

## 📂 Мої лабораторні

| Лаба | Тема | Статус | Ключове |
|------|------|--------|---------|
| [Lab_1](MyWork/Lab_1/) | Концептуальна модель (ER-діаграма) | ✅ | 5 сутностей, 7 зв'язків, самореференс Subscription |
| [Lab_2](MyWork/Lab_2/) | DDL: CREATE TABLE, INSERT | ✅ | композитні PK у junction-таблицях, CHECK-и |
| [Lab_3](MyWork/Lab_3/) | OLTP: CRUD-операції | 🔄 | SELECT/INSERT/UPDATE/DELETE |
| Lab_4 | OLAP: JOIN, агрегації | — | — |
| Lab_5 | Нормалізація 1NF–3NF | — | — |
| Lab_6 | Міграції (Prisma) | — | — |

## 🗄️ Схема БД коротко

5 таблиць: `User`, `Video`, `Comment`, `Like`, `Subscription`.

- **Сурогатні ключі** `UUID` у User/Video/Comment — на них посилаються ззовні.
- **Композитні ключі** у таблиць-зв'язок: `Like` → `PRIMARY KEY (user_id, video_id)`, `Subscription` → `PRIMARY KEY (subscriber_id, channel_id)` — унікальність пари гарантує сам ключ, без «мертвого» id.
- **CHECK-и:** спосіб входу у User (`password` АБО `google_id`), `views >= 0` у Video, заборона самопідписки `subscriber_id <> channel_id`.
- Усі FK з `ON DELETE CASCADE`; самореференс User↔User через Subscription.

## 📖 Матеріали курсу (з оригінального репо)

Форк репозиторію [ZheniaTrochun/db-intro-course](https://github.com/ZheniaTrochun/db-intro-course):

- `labs/` — завдання лабораторних (lab_1.md … lab_6.md)
- `lectures/` — нотатки лекцій
- `exercises/` — вправи з SQL
- `sql-cheat-sheet.md`, `glossary.md` — шпаргалки

---

<details>
<summary><b>Оригінальний README курсу</b></summary>

Цей репозиторій містить ресурси та налаштування середовища для курсу по базах даних.

## Матеріали лекцій

Матеріали лекцій доступні в директорії [lectures](lectures/):

- [Лекція 1 - Вступ](lectures/01%20-%20intro)
- [Лекція 2 - ER діаграми](lectures/02%20-%20ER%20diagrams)
- [Лекція 3 - Таблиці, рядки, колонки](lectures/03%20-%20Tables,%20rows,%20columns)
- [Лекція 4 - SQL частина 1](lectures/04%20-%20DML%20basics)
- [Лекція 5 - SQL частина 2 - JOIN та операції над множинами](lectures/05%20-%20JOINs%20and%20set%20operations)
- [Лекція 6 - SQL частина 3 - GROUP BY та віконні функції](lectures/06%20-%20GROUP%20BY%20and%20window%20functions)
- [Лекція 7 - SQL частина 4 - Підзапити та CTE](lectures/07%20-%20Subqueries%20and%20CTE)
- [Лекція 8 - Нормалізація](lectures/08%20-%20Normalisation)
- [Лекція 9 - Міграції](lectures/09%20-%20Migrations)
- [Лекція 10 - Транзакції](lectures/10%20-%20Transactions)
- [Лекція 11-12 - Індекси](lectures/11-12%20-%20Indices)
- [Лекція 13 - Денормалізація](lectures/13%20-%20Denormalisation)
- [Лекція 14 - Фізична організація даних на диску](lectures/14%20-%20Data%20storage%20on%20disk)
- [Лекція 15 - Нереляційні бази даних (NoSQL)](lectures/15%20-%20Non-relational%20DBMS)

## Підключення до бази даних (курс)

```bash
docker compose up -d
docker exec -it db-intro-course_postgres_1 psql -U postgres
```

pgAdmin: http://localhost:8080 (root@kpi.edu / password123)

</details>

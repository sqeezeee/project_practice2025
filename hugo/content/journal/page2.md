+++
date = 2025-06-26T00:00:00+03:00
draft = true
title = 'Создание графического интерфейса'
description = "Последние обновления и прогресс в разработке проекта"
weight = 2
+++

# 📌 Разработка графического интерфейса

## Выбор технологий
Для создания удобного десктоп-приложения был выбран Python с библиотекой psycopg2 — это позволило совместить мощь SQL-запросов к нашей базе данных PostgreSQL с интуитивным интерфейсом.
### Так было реализовано подключение к БД:
``` py
def connect_to_db(self):
        try:
            conn = psycopg2.connect(
                dbname="Database of countrys economy",
                user="postgres",
                password="Art1972#",
                host="localhost",
                port="5432"
            )
            return conn
        except Exception as e:
            messagebox.showerror("Connection Error", f"Failed to connect to database:\n{str(e)}")
            return None
```

## Внешний вид
Нарисовали макеты, продумав как будет выглядеть наше приложение и как сделать расположение всех окон максимально удобным и эффективным для пользователя.

## Создали ключевые экраны
Возможность выбрать нужную таблицу для просмотра, а также окно для выполнения SQL-запросов.
### Код для отрисовки таблиц:
``` py
    def show_table(self, table_name):
        try:
            cur = self.conn.cursor()
            cur.execute(f"SELECT * FROM \"{table_name}\" LIMIT 1000")
            rows = cur.fetchall()
            columns = [desc[0] for desc in cur.description]
            cur.close()

            self.display_results(table_name, columns, rows)

        except Exception as e:
            messagebox.showerror("Error", f"Failed to load table {table_name}:\n{str(e)}")

```
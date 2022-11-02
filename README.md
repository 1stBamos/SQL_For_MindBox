# Задание по SQL

## ТЗ

В базе данных MS SQL Server есть продукты и категории. Одному продукту может соответствовать много категорий, в одной категории может быть много продуктов. Напишите SQL запрос для выбора всех пар «Имя продукта – Имя категории». Если у продукта нет категорий, то его имя все равно должно выводиться.

## Решение

### Создаю таблицы категорий и продуктов

<p align="center">
      <img src="https://github.com/1stBamos/SQL_For_MindBox/blob/main/DBscheme.png" width="400">
</p>

<p>
  Создаю 2 таблицы. Первая с категориями, вторая с продуктами. Обе имеют колонки id и name. Заполняю их тестовыми значениями.
  
  DROP TABLE IF EXISTS category;
  CREATE TABLE IF NOT EXISTS category (
  id serial PRIMARY KEY, 
  name VARCHAR(25));
  INSERT INTO category (name) VALUES ('Молочная продукция'), ('Мясо'), ('Мучное'), ('Рыба'), ('Полуфабрикат'), ('Кондитерское изделие');
  
  DROP TABLE IF EXISTS product;
  CREATE TABLE IF NOT EXISTS product (
  id serial PRIMARY KEY, 
  name VARCHAR(25));
  INSERT INTO product (name) VALUES ('Колбаса молочная'), ('Колбаса копченая'), ('Сосиска в тесте'), ('Сэндвич с тунцом'), ('Наггетсы'), ('Торт'), ('Рис');
</p>

### Вспомогательная таблица

<p align="center">
</p>

<p>
  Т.к. необходимо реализовать связь "многие-ко-многим" необходима третья "вспомогательная" таблица. Она создается для того, чтобы база данных соответствовала первой нормальной форме (нельзя в одной ячейке перечислить несколько значений) Имеет колонки id, id_product, id_category.
  
  DROP TABLE IF EXISTS product_category;
  CREATE TABLE IF NOT EXISTS product_category (
  id serial PRIMARY KEY, 
  id_product INT,
  id_category INT);
  INSERT INTO product_category (id_product, id_category) VALUES (1,2), (2,2),(3,2),(3,3),(4,3),(4,4),(5,2),(5,5),(6,6);
</p>

### Запрос

Select product.name, category.name from product_category Join product on product_category.id_product=product.id left Join category on product_category.id_category=category.id;


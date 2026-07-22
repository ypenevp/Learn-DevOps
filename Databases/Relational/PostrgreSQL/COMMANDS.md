psql -U <username> -d <database_name>

CREATE DATABASE my_database;

\c my_database

CREATE TABLE products (
  id SERIAL,
  name VARCHAR(255)
);

CREATE TABLE table_name(
  column1 data_type column_constraint,
  column2 data_type column_constraint,
  column3 data_type column_constraint,
  ... etc
);

units_sold INTEGER

id SERIAL - automatically increment when rows are added.

name VARCHAR(50) - max size - 50

event_date DATE

long_text TEXT

start_time TIME

event_timestamp TIMESTAMP - both the date and time

event_timestamp TIMESTAMP WITH TIME ZONE

is_active BOOLEAN

--------------------------

CREATE TABLE dogs(
  id SERIAL,
  name VARCHAR(100),
  age INTEGER
);

NSERT INTO dogs (name, age)  -- more save
VALUES ('Gino', 3); - single quotes !!!

INSERT INTO dogs  -- more dangerous -> error id
VALUES ('Gino', 3);

INSERT INTO dogs (name, age) -- inser 2 values 
VALUES
  ('Gino', 3),
  ('Nora', 2);

SELECT * ---view all data
FROM dogs;

SELECT name, age  =>  name | age 
                     ------+-----
                      Gino |   3
                      Nora |   2
                      FROM dogs;

SELECT *   ---dogs whose age is less than 3
FROM dogs
WHERE age < 3;


SELECT age  ---find the age of 'Gino'
FROM dogs
WHERE name = 'Gino';
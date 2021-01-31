<h1 align=center>MongoDB Cheat Sheet | Шпаргалка</h1> 

### [0. Основи.](#0)
### [1. Створення бази даних.](#1)
### [2. Додавання даних в колекцію.](#2)
### [3. Вибірка даних з колекції.](#3)
### [4. Оновлення та видалення даних.](#4)
### [5. Об'єднання запитів.](#5)
### [6. Пошук вмісту.](#6)
### [7. Опрацювання даних в колекції.](#7)
### [8. Фільтри + Оператори.](#8)

##
##

## <a name="0" id="0" align="center">Основи</a>
```javascript
show dbs    // Всі БД
db  // Поточна БД
```

## <a name="1" align="center">Створення бази даних</a>
```javascript
use itseasy     // Створення|Вибір БД
db.dropDatabase()   // Видалення БД
db.createCollection('users')    // Створення нової колекції
show collections    // Відображення колекцій
```

## <a name="2" align=center>Додавання даних в колекцію</a>
```javascript


```

## <a name="3" align=center>Вибірка даних з колекції</a>
```javascript
db.posts.find()
db.find().pretty()
db.posts.find({ category: 'News' })
```

## <a name="4" align=center>Оновлення та видалення даних</a>
```javascript
# ASC 
db.posts.find().sort({ title: 1 }).pretty()
# desc
db.posts.find().sort({ title: -1 }).pretty()
```

## <a name="5" align=center>Об'єднання запитів</a>
```javascript

```

## <a name="6" align=center>Пошук вмісту.</a>
```javascript

```

## <a name="7" align=center>Опрацювання даних в колекції.</a>
```javascript

```

## <a name="8" align=center>Опрацювання даних в колекції.</a>
```javascript

```
![](./mandalorian.jpg)
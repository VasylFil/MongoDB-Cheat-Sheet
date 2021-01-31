<h1 align=center>MongoDB Cheat Sheet | Шпаргалка</h1> 

#### [0. Основи.](#0)
#### [1. Створення бази даних.](#1)
#### [2. Додавання даних в колекцію.](#2)
#### [3. Вибірка даних з колекції.](#3)
#### [4. Оновлення та видалення даних.](#4)
#### [5. Об'єднання запитів.](#5)
#### [6. Пошук вмісту.](#6)
#### [7. Опрацювання даних в колекції.](#7)
#### [8. Фільтри + Оператори.](#8)

##
##

## <a name="0" id="0" align="center">Основи</a>
#### Усі БД
```javascript
show dbs
```
#### Поточна БД
```javascript
db
```

## <a name="1" align="center">Створення бази даних</a>
#### Створення | Вибір БД
```javascript
use kyiv     
```
#### Видалення БД
```javascript
db.dropDatabase()
```
#### Створення нової колекції
```javascript
db.createCollection('famous')
```
#### Видалення колекції
```javascript
db.famous.drop()
```
#### Відображення усіх колекцій БД
```javascript
show collections  
```

## <a name="2" >Додавання даних до колекції</a>
#### Додавання одного запису до колекції
```javascript
db.famous.insertOne(
    {
        name: 'Taras Hryhorovych Shevchenko',
        age: 47,
        city: 'Moryntsi, Kyiv',
        occupation: ['poet', 'writer', 'artist',],
        married: false,
        works:[
            {
                name: 'Kobzar',
                type: 'book',
                date: new Date('1840')
            },
        ]
    },
)
```
#### Додавання множини записів до колекції
```javascript
db.famous.insertMany(
    [
        {
            name: 'I. I. Sikorsky',
            age: 83,
            city: 'Kyiv',
            occupation: 'Aircraft designer'
        },
        {
            name: 'K. S. Malevich',
            age: 56,
            city: 'Kyiv',
            occupation: 'Artist'
        },
        {
            name: 'M. A. Bulgakov',
            age: 48,
            city: 'Kyiv',
            occupation: 'Novelist'
        },
    ]
)
```



## <a name="3" >Вибірка даних з колекції</a>
```javascript
db.famous.find()
db.find().pretty()
db.famous.find({ category: 'News' })
```

## <a name="4">Оновлення та видалення даних</a>
```javascript 

```

## <a name="5">Об'єднання запитів</a>
```javascript

```

## <a name="6">Пошук вмісту.</a>
```javascript

```

## <a name="7">Опрацювання даних в колекції.</a>
```javascript

```

## <a name="8">Фільтри та Оператори.</a>
```javascript

```
![](./mandalorian.jpg)
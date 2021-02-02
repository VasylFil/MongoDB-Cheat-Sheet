<h1 align=center>MongoDB Cheat Sheet | Шпаргалка</h1> 

#### [0. Основи.](#0)
#### [1. Створення бази даних.](#1)
#### [2. Додавання даних в колекцію.](#2)
#### [3. Вибірка даних з колекції.](#3)
#### [4. Оновлення та видалення даних.](#4)
#### [5. Об'єднання запитів.](#5)
#### [6. Індексовані поля. Пошук вмісту.](#6)
#### [7. Обробка даних.](#7)
#### [8. Оператори.](#8)

##
##
##

## <a name="0" id="0" align="center">Основи</a>
#### `Batch file` для зручної роботи на ОС Windows
```
start /min cmd /K ""C:\Program Files\MongoDB\Server\4.4\bin\mongod.exe" "--dbpath=c:\data\db""
cmd /K "C:\Program Files\MongoDB\Server\4.4\bin\mongo.exe"
```
###### Вміст зберігаємо як `MongoDB.bat` => створюємо ярлик

#### Відобразити усі БД
```javascript
show dbs
```
#### Поточна БД
```javascript
db
```


###
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


###
## <a name="2" >Додавання даних до колекції</a>
#### Додавання одного запису до колекції
```javascript
db.famous.insertOne(
    {
        name: 'T. H. Shevchenko',
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


###
## <a name="3">Вибірка даних із колекції</a>
```javascript
db.famous.find()
```
#### Форматований вивід
```javascript
db.find().pretty()
```
#### Вибірка за фільтром
```javascript
db.famous.find(
    { occupation: 'Aircraft designer' }
)
```
#### Розширений фільр
```javascript
db.famous.find(
    {   },       // параметри пошуку
    { _id: 0 }   // параметри ігрнорування
).pretty()
```
#### Обмеження виводу
```javascript
db.famous.find(
    {   },   
    { _id: 0 }
).pretty().limit(1)
```
#### Сортування по зростанню `ASC`
```javascript
db.famous.find(
    {   },
    { _id: 0 }
).sort({ age: 1})
```
#### Сортування по спаданню `DESC`
```javascript
db.famous.find(
    {   },
    { _id: 0 }
).sort({ age: -1})
```
#### Параметри пошуку: `І`
```javascript
db.famous.find(
    { age: 56, occupation: 'Artist' },
    { _id: 0 }
).pretty()
// 
db.famous.find(
    { $and: [ {age: 56}, {occupation: 'Artist'} ] },
    { _id: 0 }
).pretty()
```
#### Параметри пошуку: `АБО`
```javascript
db.famous.find(
    { $or: [ {age: 48}, {occupation: 'Artist'} ] },
    { _id: 0 }
).pretty()
```
#### Параметри пошуку: індекси та поля
```javascript
db.famous.find(
    { 'works.0.name': 'Kobzar' }
).pretty()
```


###
## <a name="4">Оновлення та видалення даних</a>
```javascript
db.famous.updateOne(
    { age: 48 }, 
    { $set: { age:45 } }
)
```
#### Оновлення багатьох елементів
```javascript
db.famous.updateMany(
    { age: {$in: [47, 83]} }, 
    { $set: { age: 32 } }
)
```
#### Заміна елементів
```javascript
db.famous.replaceOne(
    { name: 'T. H. Shevchenko' }, 
    { 
        name: 'Taras Shevchenko',
        age: 13,
        writes: 'I Was Thirteen'
    }
)
```
#### Видалення даних
```javascript
db.famous.deleteMany(
    { age: { $lt: 45 } },
)
```


###
## <a name="5">Об'єднання запитів</a>
#### Доступні оператори:
+ #### `insertOne`
+ #### `updateOne`
+ #### `updateMany`
+ #### `deleteOne`
+ #### `deleteMany`
+ #### `replaceOne`
```javascript
db.famous.bulkWrite(
    [
        {
            insertOne: { 
                'document': {
                    name: 'Borys Yevhenovych Paton',
                    age: 101,
                    occupation: 'Scientist'
                }
            }
        },
        {
            deleteOne: {
                filter: {
                    age: 45
                }
            }
        },
        {
            updateOne: {
                filter: { ... },
                update: {
                    $set: { ... }
                }
            }
        },
        {
            replaceOne: {
                filter: { ... },
                replacement: { ... }
            }
        }
    ]
)
```


###
## <a name="6">Індексовані поля. Пошук вмісту.</a>
#### Нова колекція
```javascript
db.comments.insertMany(
    [
        {
            "name": "id labore ex et quam laborum",
            "email": "Eliseo@gardner.biz",
            "body": "laudantium enim quasi est quidem magnam voluptate ipsam eos\ntempora quo necessitatibus\ndolor quam autem quasi\nreiciendis et nam sapiente accusantium"
        },
        {
            "name": "quo vero reiciendis velit similique earum",
            "email": "Jayne_Kuhic@sydney.com",
            "body": "est natus enim nihil est dolore omnis voluptatem numquam\net omnis occaecati quod ullam at\nvoluptatem error expedita pariatur\nnihil sint nostrum voluptatem reiciendis et"
        },
        {
            "name": "odio adipisci rerum aut animi",
            "email": "Nikita@garfield.biz",
            "body": "quia molestiae reprehenderit quasi aspernatur\naut expedita occaecati aliquam eveniet laudantium\nomnis quibusdam delectus saepe quia accusamus maiores nam est\ncum et ducimus et vero voluptates excepturi deleniti ratione"
        },
        {
            "name": "alias odio sit",
            "email": "Lew@alysha.tv",
            "body": "non et atque\noccaecati deserunt quas accusantium unde odit nobis qui voluptatem\nquia voluptas consequuntur itaque dolor\net qui rerum deleniti ut occaecati"
        },
        {
            "name": "vero eaque aliquid doloribus et culpa",
            "email": "Hayden@althea.biz",
            "body": "harum non quasi et ratione\ntempore iure ex voluptates in ratione\nharum architecto fugit inventore cupiditate\nvoluptates magni quo et"
        }
    ]
)
```
#### Створення індексів
```javascript
db.comments.createIndex(
    {
        name: 'text',
        email: 'text',
        body: 'text'
    }
)
```
#### Пошук по індексованих полях
```javascript
db.comments.find({
    $text: {
        $search: 'quidem'
    }
})
```

#### Відображення релевантного вмісту
```javascript
db.comments.find(
    { $text: { $search: 'ex' } },
    { score: { $meta: 'textScore' }}
).sort({ score: { $meta: 'textScore' }})
```

###
## <a name="7">Обробка даних.</a>
#### Кількість відповідних записів
```javascript
db.famous.count({
    age: 32
})
```
#### Унікальні записи
```javascript
db.famous.distinct({
    age: 32
})
```
#### Агрегація полів
```javascript
// Щорічні внески на банківський рахунок
db.deposit.insertMany([
    {
        name: 'Kai',
        amount: 1000,
        date: new Date(2019)
    },
    {
        name: 'Kai',
        amount: 1100,
        date: new Date(2020)
    },
    {
        name: 'Mike',
        amount: 880,
        date: new Date(2020)
    },
    {
        name: 'Kai',
        amount: 1210,
        date: new Date(2021)
    },
])
```
```javascript
// Сума щорічних внесків користувава 'Kai'
db.deposit.aggregate([
    { $match: { name: 'Kai' } },
    { $group: { _id: '$name', total: {$sum: '$amount'}}}
])
```
###
## <a name="8">Оператори</a>
### Логічні оператори
#### `$and` - логічне `І`
#### `$not` - логічне `НЕ`
#### `$or` - логічне `АБО`
#### `$nor` - логічне `АБО-НЕ`
|A | B |АБО-НЕ|
|---|---|---|
|0	| 0 |	1|
|0	| 1 |	0|
|1	| 0 |	0|
|1	| 1 |	0|
##
### Оператори порівняння 
#### `$gt` - `greater than` еквівалентний `>`
#### `$lt` - `less than` еквівалентний `<`
#### `$gte` - `greater than or equal to` еквівалентний `>=`
#### `$lte` - `less than or equal to` еквівалентний `<=`
#### `$eq` - `equal` еквівалентний `==`
#### `$ne` - `not equal` еквівалентний `!=`

#### `$in` - для значень наявних у масиві
#### `$nin` - для значень наявних у масиві відсутніх у масиві

### Елементи
#### `$type` - тип елемента (Array, Object, Boolean)
#### `$exists` -  елемент (не)існує

### Масиви
#### `$all` -  відповідає усім значенням у масиві
#### `$elemMatch` -  відповідає переданій множині умов
#### `$size` -  розмірність масиву

#### Застосування:
```javascript
db.famous.find(
    { age: { $gt: 64 } }
)

db.famous.find(
    { $or: [ {age: 48}, {occupation: 'Artist'} ] },
)

db.famous.find(
    {
        age: { $in: [32, 64, 48, 83, 100] },
        occupation: { $nin: ['Novelist', 'Artist'] }
    }
)

db.famous.find(
    { works: { $exists: true } } // true || 1, false || 0
)

db.famous.find(
    { works: { $size: 1 } }
)
```

#
```
 _____ _                _          _ _ 
|_   _| |__   ___      | | ___  __| (_)
  | | | '_ \ / _ \  _  | |/ _ \/ _` | |
  | | | | | |  __/ | |_| |  __/ (_| | |
  |_| |_| |_|\___|  \___/ \___|\__,_|_|
```
![](./mandalorian.jpg)